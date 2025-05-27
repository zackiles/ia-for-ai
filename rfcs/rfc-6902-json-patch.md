# JSON Patch – Specification Summary (RFC 6902)

JSON Patch defines a format for describing changes to a JSON document. A JSON Patch document is a JSON array of **operation objects**, each defining a single atomic modification.

---

## Structure of a JSON Patch Document

A JSON Patch document is an array of **operation objects**. Each operation object must include:

- `"op"` (string, **required**) — the operation to perform: `"add"`, `"remove"`, `"replace"`, `"move"`, `"copy"`, or `"test"`.
- `"path"` (string, **required**) — a [JSON Pointer](https://datatracker.ietf.org/doc/html/rfc6901) that indicates the location in the target document.
- `"from"` (string, **required** for `"move"` and `"copy"` only) — a JSON Pointer that identifies the source location.
- `"value"` (any JSON type, **required** for `"add"`, `"replace"`, and `"test"`) — the value to apply.

The operations are executed **in order**, and if any operation fails, the patch is considered to have failed and **no changes should be applied**.

---

## Operations

### 1. `add`

Adds a value to the target location.

- If the `path` specifies an object key, it adds or replaces the value.
- If the `path` refers to an array index:
  - An integer ≤ array length inserts at that position.
  - `"-"` appends to the end.
- If the path is the empty string (`""`), it replaces the entire document.

#### Example

```json
{ "op": "add", "path": "/a/b/c", "value": "foo" }
````

---

### 2. `remove`

Removes the value at the target location.

* The target **must exist**.
* If the path refers to an array element, the removal causes subsequent elements to shift left.

#### Example

```json
{ "op": "remove", "path": "/a/b/c" }
```

---

### 3. `replace`

Replaces the value at the target location with a new value.

* The target **must exist**.
* Semantically equivalent to a `remove` followed by an `add`.

#### Example

```json
{ "op": "replace", "path": "/a/b/c", "value": 42 }
```

---

### 4. `move`

Removes the value at the `from` path and adds it at the `path` location.

* Both `from` and `path` must exist unless `path` is a new key in an object.
* The operation is atomic: nothing is done if the remove fails.
* The `from` path must not be a proper prefix of the `path` (cannot move a parent into its child).

#### Example

```json
{ "op": "move", "from": "/a/b/c", "path": "/a/b/d" }
```

---

### 5. `copy`

Copies the value at `from` to `path`.

* The source location must exist.
* The destination may be a new key or array index.

#### Example

```json
{ "op": "copy", "from": "/a/b/c", "path": "/a/b/e" }
```

---

### 6. `test`

Tests that the value at the target location is equal to the provided value.

* If the test fails, the entire patch fails.
* Equality is checked using type-aware comparison:

  * Strings must match exactly.
  * Numbers must be numerically equal.
  * Arrays and objects must match recursively and order must be preserved.

#### Example

```json
{ "op": "test", "path": "/a/b/c", "value": "foo" }
```

---

## Error Semantics

* Any operation that fails (missing key, invalid path, test failure, etc.) **invalidates the entire patch**.
* Patch must not be applied partially.
* Invalid JSON Pointers result in an error.

---

## Additional Notes

* Paths use JSON Pointer syntax (RFC 6901): `/foo/0` means the key `"foo"`, then index `0`.
* Pointers are **URI fragment–encoded** when embedded in URLs (e.g., `#/foo/0`).
* Patch is purely declarative — does not define how changes are transmitted or logged.
