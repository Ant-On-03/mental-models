# Mental Models

A showcase of draw.io diagrams created over time to understand concepts further, create UMLs, or define architecture decisions.

---

## Diagrams

### 0. Esquema Sapiencial

![Esquema Sapiencial](esquemaSapiencial.png)

A high-level knowledge map (*esquema sapiencial*) that connects domains of learning and reasoning. It serves as a meta mental model for organizing ideas before moving into concrete software and architecture patterns.

---

### 1. Design Patterns for Dummies

![Design Patterns For Dummies](PatronesDeDiseñoParaTontos.drawio.svg)

A quick visual reference of core software design patterns and how they relate. It works as an entry point for pattern vocabulary used in the rest of the diagrams.

---

### 2. Strategy Pattern + Jackson Serialization Pattern

![Strategy Pattern + Jackson Serialization Pattern](StrategyPattern+JacksonSerializationPattern.drawio.svg)

A focused model of combining behavioral design (Strategy) with robust JSON serialization/deserialization using Jackson. It highlights how runtime behavior selection and data mapping can coexist cleanly in the same design.

---

### 3. Puerto-Adaptador (DDD / Hexagonal)

![Puerto Adaptador DDD](PuertoAdaptador-DDD.drawio.svg)

A domain-driven architecture view using Port-Adapter (Hexagonal) principles. It emphasizes separation between domain logic and infrastructure adapters so business rules stay isolated, testable, and technology-agnostic.

---

### 4. Asynchronous to Linear Process

![Async to Linear Process](AsyncronousToLinearProcess.drawio.svg)

A conceptual diagram showing how to transform a **Python asynchronous process into a non-concurrent (linear) one** using concurrency and parallelism primitives. An `ENDPOINT` receives requests on the main thread, pushes them into a `Queue`, and a dedicated `WORKER` on a second thread processes them sequentially. The `WITH` block acts as a safety net, ensuring `__enter__` and `__exit__` are always called to acquire and release a lock — making it safe to connect to resources like DuckDB.

---

### 5. Asynchronous Queue Flow → DuckDB

![Async Queue Flow to DuckDB](AsyncronousQueueFlow-%3EDuckDB.drawio.svg)

A concrete implementation strategy for converting an **asynchronous flow into a linear (serialized) process** when writing to DuckDB. Because DuckDB does not support concurrent writes, this diagram illustrates a Singleton `QueueManager` pattern where async handlers submit work and then await a lock before writing. A session wrapper handles `__enter__` / `__exit__` for safe context-managed access.

---

### 6. Demand Forecast Ingestion Flow

![Demand Forecast Ingestion Flow](flow_ingesta_demand_forecast.drawio.svg)

An end-to-end process flow for ingesting demand data into a forecasting pipeline. It organizes the stages from data intake and validation to transformation and delivery into downstream prediction/optimization components.

---

### 7. Optimization & Forecast UML

![Optimization Forecast UML](Optimization_Forecast_UML.drawio.svg)

A UML class diagram for a **supply chain optimization and demand forecasting** system. Key components:

- **`DemandPredictor`** – loads a time-series model (e.g. ARIMA) to forecast future demand.
- **`Optimizer`** – wraps a MIP solver (e.g. CBC) with configurable time limits and MIP gap to produce replenishment policies.
- **`SupplyChainService`** – orchestrates the predictor and optimizer, exposing a single `generate_politics(OptimizationInput) → OptimizationPolitics` entry point.
- **`OptimizationInput`** / **`OptimizationPolitics`** – data transfer objects carrying constraints + predicted demand in, and reorder point `R` / order quantity `Q` out.

---

### 8. Rocket UML

![Rocket UML](Rocket_UML.drawio.svg)

A UML class diagram for a **file-processing pipeline** (internally named *Rocket*). It models the lifecycle of files through a schema-versioning workflow:

- **`FilesModel`** – core entity holding file metadata (owner, playbook, path, size, dates, description) and a `FileStatusType`.
- **`FileStatusType`** (enum) – `QUEUED → IN_PROGRESS → COMPLETED / FAILED / CANCELED`.
- **`SchemaState`** / **`SchemaId`** – track which schema version a file is associated with and whether it has been processed.
- **`NewSchemaInfo`** – carries the old and new schema UIDs during a schema migration event.
