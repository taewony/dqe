# Knowledge Query Engine (KQE)

> A Semantic Knowledge Operating System for Structured Data, Documents, and Agentic Query Execution

## Vision

KQE는 자연어 질문을 Knowledge Catalog, Query Planner, SQL/RAG 실행을 통해 처리하는 Knowledge Operating System이다.

---

# System Architecture

```mermaid
flowchart TD

subgraph Client
    UI["Web Dashboard"]
    CLI["CLI Client"]
end

subgraph AgentCore
    ORCH["Agent Orchestrator"]
    PLAN["Query Planner"]
    SYN["Response Synthesizer"]
    MEM["Session Memory"]
end

subgraph KnowledgeLayer
    CAT["Knowledge Catalog"]
    RULE["Business Rules"]
    GLOSS["Domain Glossary"]
end

subgraph DataServices
    SQL["Text-to-SQL Agent"]
    RAG["RAG Agent"]
end

subgraph Storage
    DB[("SQLite")]
    VDB[("Vector Database")]
    OKF[("OKF Repository")]
end

UI --> ORCH
CLI --> ORCH
ORCH --> PLAN
ORCH --> MEM
PLAN --> CAT
PLAN --> SQL
PLAN --> RAG
CAT --> OKF
RULE --> OKF
GLOSS --> OKF
SQL --> DB
RAG --> VDB
SQL --> SYN
RAG --> SYN
SYN --> UI
```

---

# Knowledge Flow Architecture

```mermaid
flowchart LR

Q["User Question"]
I["Intent Analysis"]
C["Knowledge Catalog"]
P["Query Plan"]
SQL["SQL Retrieval"]
RAG["Document Retrieval"]
M["Result Merge"]
A["Final Answer"]

Q --> I
I --> C
C --> P
P --> SQL
P --> RAG
SQL --> M
RAG --> M
M --> A
```

---

# Query Execution Sequence

```mermaid
sequenceDiagram

actor User

participant Orchestrator
participant Planner
participant Catalog
participant SQLAgent
participant RAGAgent
participant Synthesizer

User->>Orchestrator: Ask Question
Orchestrator->>Planner: Analyze Intent
Planner->>Catalog: Semantic Lookup
Catalog-->>Planner: Return Metadata
Planner->>SQLAgent: Execute SQL
Planner->>RAGAgent: Retrieve Documents
SQLAgent-->>Planner: Data Result
RAGAgent-->>Planner: Context Result
Planner->>Synthesizer: Merge Results
Synthesizer-->>User: Final Answer
```

---

# Multi-Hop Query Planning

```mermaid
flowchart TD

Q["Question"]
D["Load Definitions"]
S["Generate SQL"]
E["Execute Query"]
R["Retrieve Documents"]
C["Compute Metrics"]
A["Generate Answer"]

Q --> D
D --> S
S --> E
E --> R
R --> C
C --> A
```

---

# Knowledge Repository Structure

```mermaid
flowchart TD

K["Knowledge Repository"]

K --> CAT["Catalog"]
K --> MET["Metrics"]
K --> BR["Business Rules"]
K --> GLO["Glossary"]
K --> PRO["Prompts"]

CAT --> CUS["customer.okf"]
CAT --> ORD["order.okf"]

MET --> SALES["sales.okf"]
MET --> RET["retention.okf"]

BR --> VIP["vip_customer.okf"]
BR --> REF["refund_policy.okf"]

GLO --> TERMS["domain_terms.okf"]

PRO --> SQLP["sql_generation.okf"]
PRO --> ANS["answer_style.okf"]
```
