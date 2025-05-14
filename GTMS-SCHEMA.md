# RFC: Graph Type Metadata Schema (GTMS)

The Graph Type Metadata Schema (GTMS) defines a standard format for expressing metadata describing the structural and topological characteristics of graphs. GTMS enables tools and systems to quickly inspect and validate essential properties of graphs, facilitating interoperability, algorithm selection, query optimization, and data exchange across diverse environments.

## Overview

GTMS describes graphs independently from their detailed structural representation (such as edge lists, adjacency matrices, or node-link formats). It captures high-level properties, including the general graph structure, directionality, cyclicity, connectivity, and degree constraints.

## JSON Schema Specification

The GTMS schema conforms to JSON Schema (Draft 2020-12):

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://raw.githubusercontent.com/zackiles/ia-for-ai/main/schemas/gtms.schema.json",
  "title": "Graph Type Metadata Schema (GTMS)",
  "type": "object",
  "required": [
    "structure",
    "capabilities",
    "nodeCount",
    "edgeCount",
    "minInDegree",
    "maxInDegree",
    "minOutDegree",
    "maxOutDegree"
  ],
  "properties": {
    "structure": {
      "type": "string",
      "enum": [
        "graph",
        "dag",
        "tree",
        "forest",
        "hypergraph",
        "multigraph"
      ],
      "description": "Broad topological class of the graph"
    },
    "variant": {
      "type": "array",
      "items": {
        "type": "string",
        "enum": [
          "rooted",
          "binary",
          "nary",
          "complete",
          "strongly_connected"
        ]
      },
      "uniqueItems": true,
      "description": "Optional tags refining the graph structure"
    },
    "capabilities": {
      "type": "integer",
      "minimum": 0,
      "maximum": 15,
      "description": "Bit-flag encoding of graph capabilities: 1=directed, 2=cyclic, 4=multi_edges, 8=shared_children"
    },
    "nodeCount": { 
      "type": "integer", 
      "minimum": 0,
      "description": "Total number of nodes in the graph"
    },
    "edgeCount": { 
      "type": "integer", 
      "minimum": 0,
      "description": "Total number of edges in the graph"
    },
    "maxDepth": { 
      "type": "integer", 
      "minimum": 0,
      "description": "Maximum depth of the graph if applicable (such as in trees or DAGs)"
    },
    "rootNodes": {
      "type": "array",
      "items": { "type": "string" },
      "description": "List of identifiers for root nodes, if applicable"
    },
    "minInDegree": { 
      "type": "integer", 
      "minimum": 0,
      "description": "Minimum number of incoming edges per node"
    },
    "maxInDegree": { 
      "type": "integer", 
      "minimum": 0,
      "description": "Maximum number of incoming edges per node"
    },
    "minOutDegree": { 
      "type": "integer", 
      "minimum": 0,
      "description": "Minimum number of outgoing edges per node"
    },
    "maxOutDegree": { 
      "type": "integer", 
      "minimum": 0,
      "description": "Maximum number of outgoing edges per node"
    },
    "connectedComponents": { 
      "type": "integer", 
      "minimum": 1,
      "description": "Number of disconnected subgraphs in the overall graph"
    }
  },
  "additionalProperties": false
}
```

## Example Usage

### Rooted Tree

```json
{
  "structure": "tree",
  "variant": ["rooted", "nary"],
  "capabilities": 1,
  "nodeCount": 41,
  "edgeCount": 40,
  "maxDepth": 2,
  "rootNodes": ["linguistic_system"],
  "connectedComponents": 1,
  "minInDegree": 0,
  "maxInDegree": 1,
  "minOutDegree": 0,
  "maxOutDegree": 10
}
```

### Directed Acyclic Graph (DAG) with Shared Children

```json
{
  "structure": "dag",
  "variant": ["rooted"],
  "capabilities": 9,
  "nodeCount": 5,
  "edgeCount": 6,
  "maxDepth": 3,
  "rootNodes": ["node_a"],
  "connectedComponents": 1,
  "minInDegree": 0,
  "maxInDegree": 2,
  "minOutDegree": 0,
  "maxOutDegree": 3
}
```

## Schema Properties Explained

### Structure and Variants

The `structure` field defines the high-level topological classification:

* `graph`: General-purpose graphs without specific constraints.
* `dag`: Directed acyclic graphs.
* `tree`: Connected acyclic graphs with hierarchical structure.
* `forest`: Collection of disconnected trees.
* `hypergraph`: Graphs whose edges connect multiple nodes.
* `multigraph`: Graphs allowing multiple edges between nodes.

The optional `variant` field refines the structure, providing additional context or constraints such as:

* `rooted`: Has clearly defined root nodes.
* `binary`: Nodes have at most two children.
* `nary`: Nodes have multiple children.
* `complete`: Fully connected graph.
* `strongly_connected`: All nodes reachable from every other node.

### Capabilities Bit-Flags

The `capabilities` integer encodes key graph properties:

| Bit | Capability       | Description                                  |
| --- | ---------------- | -------------------------------------------- |
| 1   | directed         | Edges have directionality.                   |
| 2   | cyclic           | Graph contains cycles.                       |
| 4   | multi\_edges     | Graph supports multiple edges between nodes. |
| 8   | shared\_children | Nodes have more than one incoming edge.      |

For example, a directed cyclic graph with multi-edges would have capabilities value `7` (`0111` binary).

## Intended Use and Application

GTMS is designed for scenarios where quick introspection of graph properties is required without loading or traversing entire datasets. Common applications include:

* Pre-validating graphs against structural constraints before loading.
* Algorithm selection and optimization (e.g., cycle detection, shortest path algorithms).
* Efficient query planning and resource allocation.
* Cross-tool and cross-system interoperability of graph data.

## Implementation Guidance

When producing GTMS metadata:

* Compute degree statistics and properties at export time to ensure accuracy.
* Store metadata alongside graph data consistently.
* Validate regularly to prevent drift between metadata and actual graph structure.

When consuming GTMS metadata:

* Decode capabilities using bitwise operations.
* Verify metadata against sampled edges for large external graphs.
* Use provided metadata to select optimized traversal and analysis strategies.

## Related Standards and Formats

GTMS complements existing graph standards, including:

* GraphML (structure-focused representation).
* RDF/OWL (semantic web ontologies and typed relationships).
* JSONL/NDJSON (structured data streaming and interchange).

## Summary
GTMS delivers a unified vocabulary for graph structure that bridges a critical gap in how metadata is communicated across platforms, models, and storage layers—supporting reasoning, automation, and integration in diverse ecosystems.
