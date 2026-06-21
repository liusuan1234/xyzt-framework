# 🌌 XYZT: Universal Cognitive Coordinate Framework

Elevate chaotic semantic spaces into precise, structured coordinates.

![Status](https://img.shields.io/badge/Status-Specification_v4.0_Full-orange) ![License](https://img.shields.io/badge/license-Apache_2.0-blue.svg) ![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)

# ⚠️ Project Status:

This project is currently in the Specification phase. This repository contains the complete core theory, mathematical models, data modeling specifications, full-scenario application architectures, and evaluation systems of XYZT.

👉 Looking for code implementations? Please check the `/reference-implementation` directory (under development) or view our Roadmap.

## 📖 1. Introduction

Current AI systems based on Large Language Models (LLMs) heavily rely on "semantic distance" in high-dimensional vector spaces for information retrieval and association. This single paradigm has inherent structural defects when dealing with complex, dynamic, and multi-dimensional real-world knowledge: it lacks clear boundaries, struggles to handle state evolution, and easily loses macro-context (resulting in "semantic traps" and "temporal blindness").

XYZT is not a specific database or RAG middleware, but a foundational cognitive computing paradigm and data modeling specification. It defines how to map arbitrary information entities into multi-dimensional orthogonal coordinates (Context, Entity, Observation, Evolution), providing a theoretical foundation and architectural guidance for building next-generation AI applications with precise positioning, state tracing, and logical reasoning capabilities.

## 🎯 2. Motivation

| Pain Points of Traditional Dense Retrieval | XYZT Framework Solutions |
| :--- | :--- |
| Semantic Pollution: Recalls semantically similar but contextually/domain-wise completely irrelevant content. | X-Dimension Hard Isolation: Performs  $ O(1) $  complexity pre-filtering via context boundaries. |
| Entity Divergence: Different expressions of the same entity are fragmented, lacking aggregation. | Y-Dimension Anchor: Enforces entity resolution, achieving entity-level information aggregation across documents. |
| Temporal Blindness: Cannot distinguish between historical states and the latest current state of the same entity. | T-Dimension Temporal Overriding: Natively supports state machine sequences and time intervals, automatically filtering out obsolete facts. |
| Prompt Drift: In multi-turn conversations, LLMs easily forget initial roles and macro-constraints. | XYZT-Prompt: Locks X/Y as global coordinates for dynamic context inheritance. |



## 🧠 3. Core Concepts: XYZT Coordinate Space & Boundary Audits

XYZT abstracts the information space into four foundational orthogonal dimensions. During data modeling, the logical boundaries of each dimension must be strictly followed.

### 3.1 X Dimension: Context & Boundary

Definition: Defines the macro-environment, applicable domain, or system boundary where the information exists (the "stage").

Boundary Audit (Relativity & Nesting): The distinction between X and Y is relative. The same concept can switch roles at different granularities (e.g., "Finance Dept" is an entity Y in company structure, but context X in "Finance Dept Reimbursement Policy"). Thus, X is typically a hierarchical taxonomy supporting nesting and inheritance ( 
X
c
h
i
l
d
⊂
X
p
a
r
e
n
t
X 
child
​
 ⊂X 
parent
​
  ).
  
Core Function: Provides the highest priority hard isolation to prevent cross-domain logical fallacies.

### 3.2 Y Dimension: Entity & Anchor

Definition: The core subject being observed or operated within a specific X (the "actor").

Boundary Audit (Uniqueness & Disambiguation): Y must possess global or local unique identifiers. Aliases of the same physical entity in different expressions must be normalized (Entity Resolution) within the Y dimension.

Core Function: Achieves entity-level aggregation; all attributes and time slices are mounted onto Y.

### 3.3 Z Dimension: Attribute, Feature & Observation

Definition: Specific descriptions, parameters, or micro-observations of entity Y under specific X and T.

Boundary Audit (Decoupling from T): The Z dimension only records the "observation value" (e.g., "Temp=80℃"), not the sequence of when the state occurred. State evolution is handled by T. Z is highly heterogeneous (numerical/textual/vector).

Core Function: Provides the foundation for fine-grained conditional matching and computation.

### 3.4 T Dimension: Evolution, Sequence & Lifecycle

Definition: Identifies the position of information on the timeline or the sequence of state transitions.

Boundary Audit (Beyond Absolute Time): T includes not only physical timestamps but also partial orders or state machine sequences (e.g., 
T
v
1
→
T
v
2
T 
v1
​
 →T 
v2
​
  ) in logical reasoning. T is responsible for recording the effective interval of Z-dimension observations.
  
Core Function: Empowers the system with dynamic evolution awareness and Temporal Overriding capabilities.

## 📐 4. Mathematical Model & Computing Paradigm

### 4.1 Composite Tuple Representation of Coordinate Points

Due to the heterogeneous data types across dimensions, any information node 
i
i in the knowledge base is mathematically represented as a Composite Tuple, rather than a single tensor:

K 
i
​
 =⟨X 
i
​
 ,Y 
i
​
 ,Z 
i
​
 ,T 
i
​
 ⟩
 
Where 
X
i
X 
i
​
  is a set of tags, 
Y
i
Y 
i
​
  is a scalar ID, 
Z
i
Z 
i
​
  is a heterogeneous key-value pair or vector space, and 
T
i
T 
i
​
  is a scalar or interval.
  
### 4.2 Heterogeneous Similarity Metric

Given a target coordinate Q=⟨X 
q
​
 ,Y 
q
​
 ,Z 
q
​
 ,T 
q
​
 ⟩ extracted from query intent, the system adopts a Multi-path Recall & Fusion paradigm:
 
Exact Matching for Discrete Dimensions (Hard Filtering): Uses Boolean logic or set operations on X and T for precise filtering.

Graph Traversal for Identifier Dimensions (Relational Query): Uses graph structures to calculate topological distances for Y.

Vector Metrics for Continuous Dimensions (Semantic Retrieval): Calculates cosine similarity in high-dimensional vector space for Z.

Score Fusion: Uses statistical algorithms like Reciprocal Rank Fusion (RRF) to normalize and fuse multi-path recall results.

## 🧩 5. XYZT+ Orthogonal Extensibility Design

XYZT possesses strict orthogonality. Information in extended dimensions cannot be deduced simply by combining X, Y, Z, and T.

### +R (Relation / Topology): 

Explicitly defines directed/undirected relationships (causal, inclusive, mutually exclusive) between Y dimensions, compensating for the lack of complex multi-hop reasoning in pure coordinate spaces.

### +P (Priority & Provenance): 

Assigns confidence weights or data lineage pointers to coordinate points, providing automatic arbitration during information conflicts.

### +C (Constraint & Clearance): 

Maps access control policies to the C dimension, implementing data isolation at the retrieval layer to prevent unauthorized recalls.

### +M (Modality / Features): 

Visual or audio feature tensors independent of textual semantics, supporting cross-modal joint retrieval.

## 💻 6. Engineering Data Schema Mapping

To implement XYZT in engineering, we designed a flattened JSON Schema. This design perfectly aligns with the best practices of mainstream hybrid-search vector databases (e.g., Qdrant, Milvus, Weaviate) regarding the separation of Payload and Vector.

```json

编辑



{
  "id": "node_8f3a2b",
  "vector": [0.012, -0.045, 0.882, "...(1024 dims)"], 
  "payload": {
    "X_context": {
      "domain": "finance",
      "doc_type": "policy",
      "hierarchy_path": "company/hr/reimbursement" 
    },
    "Y_entity": {
      "id": "entity:reimbursement_standard",
      "type": "policy_rule",
      "aliases": ["reimbursement_standard", "travel_reimbursement"]
    },
    "Z_observation": {
      "structured": { "max_limit": 500.00, "currency": "CNY" },
      "text_chunk": "The maximum accommodation standard for domestic business trips is 500 CNY/night..."
    },
    "T_evolution": {
      "effective_from": 1672531200, 
      "effective_to": null, 
      "version_seq": 3,
      "state": "active"
    },
    "ext_P_provenance": { "source": "hr_manual_2023.pdf", "page": 12 },
    "ext_C_clearance": ["role:employee", "role:manager"]
  }
}
```

## 🏗️ 7. Core Application Architectures & API Abstractions

The value of XYZT lies in its incremental reconstruction of existing AI application architectures.

### 7.1 XYZT-RAG (High-SNR Retrieval-Augmented Generation)

Incremental Value: Elevates metadata filtering to an inevitable prerequisite of cognitive coordinates. The core lies in T-dimension Temporal Overriding: 

automatically shielding historical Z values and precisely restoring time slices.

Execution Flow Architecture:



```
graph TD
    A[Natural Language Query] --> B(XYZT Coordinate Parser)
    B -->|LLM/Few-shot NER| C{Extracted Intent}
    C -->|X & T| D[Hard Filter / Pre-filtering]
    C -->|Y| E[Graph Traversal]
    C -->|Z vector| F[Vector Search]
    D -->|Candidate IDs| E
    D -->|Candidate IDs| F
    E --> G[Score Fusion RRF]
    F --> G
    G --> H[Temporal Resolver]
    H -->|Deduplicate by Y & T| I[Final High-SNR Context]
```

### 7.2 XYZT-Prompt (Drift-Proof Prompt Engineering)

Incremental Value: Deconstructs prompts into coordinates. X (Role/Background) and Y (Core Object) are "locked" and "inherited" as global coordinates across multi-turn conversations, while Z and T update dynamically, completely solving instruction forgetting and role drifting in long conversations.

### 7.3 XYZT-Agent (Long-horizon Episodic Memory)

Incremental Value: Provides a structured memory bank for Agents. Instead of stuffing massive history into the Context Window, Agents extract precisely on demand via coordinate queries: Search(X=project, Y=module, T < step_10), reducing Token consumption by orders of magnitude.

### 7.4 XYZT-KG/DT (Complex System Digital Twin & Dynamic Graph)

Incremental Value: Fuses static graphs with IoT time-series data. Builds a 4D graph with Y as the core, X as the hierarchy, Z as the payload, and T as the lifecycle. Supports Time-Travel Queries, completely restoring the topology and attribute states of the system at any past point in time.

💡 API Pseudocode Abstraction (Taking RAG Retriever as an example)
```
python

编辑



class XYZTRetriever:
    def retrieve(self, query: str) -> List[CoordinateNode]:
        # 1. Intent Parsing (Challenge: Requires LLM Router or Few-shot NER)
        intent = self.query_parser.parse(query) 
        
        # 2. Hard Filtering: O(1) scalar filtering using X and T
        candidate_ids = self.metadata_index.filter(
            X_domain=intent.X, T_state='active', T_effective_to=None
        )
        
        # 3. Hybrid Recall: Graph traversal for Y and vector search for Z within candidates
        graph_results = self.graph_db.traverse(anchor=intent.Y, filter_ids=candidate_ids)
        vector_results = self.vector_db.search(vector=intent.Z_vector, filter_ids=candidate_ids)
        
        # 4. Score Fusion and Temporal Deduplication
        fused_nodes = self.fusion_engine.rrf(graph_results, vector_results)
        return self.temporal_resolver.deduplicate_by_Y_and_T(fused_nodes)
```

## ⚙️ 8. Engine Requirements for Underlying Compute

XYZT is not bound to specific databases, but requires the underlying supporting engines to possess the following core capabilities:

### Polymorphic Storage & Federated Query: 

Must efficiently handle discrete scalars (X, T), graph structures (Y), and high-dimensional vectors (Z) simultaneously, or provide ultra-low latency cross-database federated query interfaces.

### Native Time-Series & State Management: 

Natively supports time-range queries or version snapshots to implement T-dimension temporal overriding, rather than merely recording data creation times.

### Pre-filtering & Scalar Indexing: 

Vector engines must possess robust scalar pre-filtering capabilities, ensuring that before executing high-cost vector computations, X and T are used to drastically reduce the search space.

## 📊 9. System Evaluation Metrics

Evaluating systems built on XYZT requires introducing specific evaluation dimensions targeting coordinate characteristics:

Coordinate Precision: The proportion of recalled results where (X, Y, T) coordinates perfectly match the standard intent. Measures the ability to "find the right place".

Context SNR (Signal-to-Noise Ratio): The proportion of coordinate nodes directly relevant to the query intent within the context fed to the LLM. Measures the ability to remove irrelevant noise and save Tokens.

Temporal/State Consistency: Ensures no logical contradictions exist in the recalled set regarding the same entity at the same time/state. Measures the effectiveness of handling T-dimension conflicts.

Boundary Rejection Rate: The proportion of times the system accurately identifies and refuses to answer when the query intent exceeds the system's defined X (context boundary).

## 🤝 10. Contributing

XYZT is an open cognitive paradigm. We welcome AI researchers, database kernel developers, and LLM application engineers to participate.

Theoretical Discussion: If you believe dimension definitions are ambiguous or new orthogonal extensions (XYZT+) are needed, please submit an [Issue].

Code Contribution: If you have implemented efficient Coordinate Parsers or Temporal Resolvers, feel free to submit a [PR].

Case Sharing: Applied the XYZT paradigm in your business? Welcome to share your architectural practices in [Discussions].

(Please refer to CONTRIBUTING.md for detailed contribution guidelines.)

## 📄 11. License

The documentation and theoretical specifications of this project are open-sourced under the Apache 2.0 License. You are encouraged to freely use the XYZT paradigm in commercial and academic projects.

"Information is not just a vector; it has coordinates."
