---
layout: post
title: "The Evolution of MLOps: A Six-Year Journey at AstrumU"
date: 2025-05-01
categories: [MLOps, Machine Learning, Architecture]
tags: [MLOps, AzureML, Databricks, Kubernetes, FastAPI, Ray]
---

Productionizing Machine Learning (ML) models effectively and at scale remains a significant challenge for many organizations. This article traces the architectural evolution of the MLOps platform at AstrumU over six years, highlighting the technical decisions, trade-offs, and lessons learned while building a sophisticated system for distributed data processing and ML inference. 

The journey reflects a common progression from initial, often ad-hoc solutions to a mature, scalable, and flexible end-to-end platform.

Initially, the team's focus was on developing models for single use cases. However, scaling these models into production reliably and efficiently quickly emerged as a major bottleneck. The primary technical hurdle lay in the disparate technology stacks and data storage systems used by data scientists and software engineers.

## Phase 1: Initial Production - AzureML Endpoints with JavaScript/TypeScript Translation

The early architecture involved developing ML models and data processing logic primarily in Python, while the core applications were built using JavaScript/TypeScript. To expose the ML capabilities, models were deployed via managed AzureML endpoints.

### Architecture

- Python-based ML models and data processing pipelines
- AzureML endpoints serving the trained models
- Core applications written in JavaScript/TypeScript consumed these endpoints
- Data for ML was managed in Databricks by the Data Science team, while the Engineering team maintained a separate Postgres backend for application data
- Data needed for production features was periodically moved from Databricks to Postgres, introducing duplication and potential for inconsistency

### Core Components
* **AzureML:** Managed service for deploying and serving ML models as endpoints.
* **Databricks:** Primary data storage and processing platform for Data Science and Data Engineering teams.
* **JavaScript/TypeScript Applications:** Used by Software Engineering for building production applications and integrating with ML endpoints.
* **Postgres:** Backend data store for production applications, managed by the Engineering team.

### Process Flow

Application code would call an AzureML endpoint. However, significant data pre-processing (preparing features for the model) and post-processing (interpreting model outputs) was required. This vital logic resided within the Python development environment.  

### Technical Challenge
Software engineers building the applications were tasked with translating the complex Python data processing logic into JavaScript/TypeScript. This involved replicating intricate data transformations, feature engineering steps, and output parsing in a completely separate codebase. 

### Consequences
* **Code Duplication:** Two separate codebases implementing the same complex logic (Python for data science, JavaScript/TypeScript for production).  
* **High Maintenance Overhead:** Any change or iteration on the Python data pipeline or model required a corresponding, often complex, update to the JavaScript/TypeScript codebase.  
* **Inconsistent Batch vs. Online Inference:** Logic implemented differently in batch processing (often in Python) versus online inference (in JavaScript/TypeScript calling the endpoint) led to discrepancies and difficult-to-debug issues.  
* **Data Duplication:** Data Science and Engineering teams managed separate data stores (Databricks and Postgres), requiring periodic data transfers and risking inconsistency.

### Lesson Learned

Duplicating complex business/data processing logic across different language stacks is unsustainable, error-prone, and a major source of inconsistency in MLOps. Similarly, duplicating data storage between teams increases operational overhead and the risk of inconsistency. The boundary between ML/data logic and application logic needs to be carefully managed, ideally keeping ML-dependent data transformations and data management within the ML domain.

## Phase 2: Unifying Logic - MLflow on Databricks

Recognizing the critical issues with the translation approach, the team pivoted to a strategy of encapsulating *all* necessary data processing (both ML-specific and stable non-ML procedures) within the model endpoint itself.

### Architecture

- All data processing and ML inference logic unified in Python
- Models, wrapped with their pre/post-processing, were packaged using MLflow and deployed as endpoints hosted on Databricks
- Databricks was chosen as much of the batch data processing already occurred there
- The separation of data storage persisted: Data Engineers managed data pipelines and ML features in Databricks, while Software Engineers continued to build applications on top of their own Postgres backend
- Data was routinely transferred from Databricks to Postgres for use in production systems

### Core Components
* **MLflow:** For model packaging, versioning, and artifact management.
* **Databricks:** A unified platform supporting exploratory data analysis, data pipeline orchestration, ML model training workflows, and serving both online inference endpoints and batch processing jobs.
* **Spark:** Used for batch processing and integrating MLflow models as UDFs.
* **JavaScript/TypeScript Applications:** Production applications built and maintained by Software Engineering, consuming ML endpoints.
* **Postgres:** Backend data store for production applications, managed by the Engineering team.

### Process Flow

Applications would call these new, self-contained Python endpoints. The endpoints handled receiving raw data, performing all necessary transformations, running inference, and formatting the output, standardizing communication via versioned interfaces. MLflow facilitated packaging these as Spark UDFs, allowing reuse in batch pipelines for consistency. However, the data required for production applications still needed to be moved from Databricks to Postgres, maintaining the duplication and synchronization challenges.

### Benefits
* **Unified Logic:** A single source of truth in Python for inference-time data processing.  
* **Improved Batch/Online Consistency:** Reusing the same MLflow-packaged logic as Spark UDFs in batch jobs ensured alignment with online inference.  
* **Standardized Interface:** Versioned endpoints provided clear contracts for software engineers.  
* **Leveraged Existing Infrastructure:** Utilizing Databricks aligned with current data pipeline operations.

### New Challenges
* **Developer Experience:** MLflow/Databricks endpoints often had less flexible or developer-friendly input/output interface definitions compared to standard API frameworks.  
* **Inefficient Scaling:** Each endpoint was typically managed as a separate, isolated containerized application by Databricks. While simple for individual services, managing and scaling a large number of these independent, often heterogeneous, services became inefficient in terms of resource utilization and operational oversight.  
* **Cumbersome Cross-Endpoint Dependencies:** Implementing workflows where one ML service depended on the output of another required complex and inefficient cross-endpoint calls, often involving external network hops rather than efficient internal service communication.  
* **Ongoing Data Synchronization:** Software Engineers preferred Postgres for its transactional integrity, operational familiarity, and seamless integration with application frameworks, but this led to duplicated data management and increased maintenance overhead as data had to be routinely synchronized from Databricks to Postgres.

### Lesson Learned

While unifying logic within the ML domain is critical, the underlying deployment platform must provide flexibility for managing inter-service dependencies, efficient resource utilization for diverse workloads, and granular operational control beyond simply hosting individual models. A platform forcing strict isolation per model/endpoint can create new integration and scaling bottlenecks. Likewise, maintaining separate data stores for ML and application workloads increases operational complexity and the risk of inconsistency.

## Phase 3: Flexible & Scalable MLOps - FastAPI on Kubernetes

Motivated by the limitations of the Databricks-managed endpoints, the need for greater flexibility, and the emergence of new complex use cases like Large Language Models (LLMs), the team transitioned to a third-generation architecture built on microservices orchestrated by Kubernetes.

### Architecture

- Endpoints were refactored into lightweight, performant microservices using FastAPI
- These services, incorporating Ray for distributed computing needs, were deployed on a self-managed Kubernetes cluster
- A major advancement in this phase was the unification of data storage: Data Engineers and Data Scientists now manage the production Postgres database directly, eliminating the need for data duplication and ensuring a single source of truth for both ML and application workloads

### Core Components
* **FastAPI Microservices:** Chosen for its high performance (leveraging Starlette and Pydantic), asynchronous capabilities, and automatic generation of API documentation (OpenAPI/Swagger UI). Services handle specific inference tasks, data-driven business logic, or complex hybrid workflows. Pydantic models enforce clear input/output schemas.  
* **Kubernetes Orchestration:** Provides a robust platform for deploying, scaling (Horizontal Pod Autoscalers based on CPU/memory or custom metrics), and managing the lifecycle of the FastAPI services. Offers fine-grained control over networking, resource allocation, and deployment strategies (e.g., rolling updates, blue/green).  
* **Ray for Distributed Computing:** Integrated within FastAPI services, Ray is used for parallelizing inference tasks (e.g., batching requests, multi-part processing for LLMs), managing distributed state, and enabling efficient data processing (ray.data) that can share the same compute substrate as the serving layer. Ray Serve specifically is leveraged for complex model serving patterns or model composition.  
* **PostgreSQL:** Now serves as the unified, reliable production data store for both structured application data and ML workloads, managed directly by Data Engineers and Data Scientists.  
* **MLflow:** Retained for its core strength in tracking experiments, logging parameters/metrics, and managing model artifacts (files, dependencies). Model binaries and metadata stored here are retrieved by the FastAPI/Ray services at runtime.  
* **Dagster for Workflow Orchestration:** Replaced Databricks orchestration. Dagster provides a more robust, data-aware approach to defining and running data pipelines (ETL, feature engineering) and ML training workflows. Its concept of "assets" and a clear dependency graph enhances visibility and maintainability of complex multi-step processes.  
* **Kafka with SCD/CDC:** An in-house service built on Kafka implements Slowly Changing Dimensions (SCD) and Change Data Capture (CDC) patterns. CDC captures database changes as a stream of events, pushed to Kafka topics. Consumers of these topics can then apply SCD logic to maintain historical views of data or trigger downstream processes like model retraining or feature store updates. This provides data integrity, traceability, and enables truly event-driven pipelines.  

### Impact and Benefits of V3
* **High Flexibility & Control:** Self-managed Kubernetes allows complete control over the deployment environment, enabling optimization for specific workloads and complex dependencies.  
* **Scalable & Efficient:** Microservices can be scaled independently, and Kubernetes/Ray provide efficient resource utilization compared to managing discrete, potentially heavyweight, endpoint instances. Inter-service communication within the cluster is more efficient.  
* **Unified, Reusable Models:** Ray Data ensures that the *same* production models served by the FastAPI/Ray services are easily accessible and usable within batch data pipelines, guaranteeing batch/online consistency at a fundamental level.  
* **Event-Driven, Robust Pipelines:** The integration of Kafka, SCD/CDC, and Dagster enables pipelines to react automatically to data changes or other events (e.g., new model versions, package updates), leading to more automated and robust MLOps workflows. Model retraining pipelines are triggered by these events, with MLflow tracking details and facilitating informed deployment decisions.  
* **Decoupled Development:** Standardized FastAPI endpoints provide a clear, stable contract for application developers, decoupling the iteration speed of data/ML model development from user-facing feature delivery.  
* **Unified Data Storage:** By merging data management into a single Postgres backend, operational overhead and data duplication were eliminated, improving data consistency and enabling more efficient cross-team collaboration between Data Science and Engineering.

## Summary of Architectural Evolution

| Architecture Version | Main Characteristics | Key Problem Solved | New Challenges Introduced | Lesson(s) Learned |
| :---- | :---- | :---- | :---- | :---- |
| **1. AzureML Endpoints + JavaScript/TypeScript** | - ML models via AzureML<br>- Python ML/Data, JavaScript/TypeScript App<br>- SWEs translate Python logic<br>- Separate data storage: Databricks (DS), Postgres (Eng); periodic data transfer | Initial model deployment | Code duplication, high maintenance, batch/online inconsistency, data duplication | Duplicating logic and data across language stacks and storage systems is unsustainable and causes inconsistency. |
| **2. MLflow on Databricks** | - All logic encapsulated in Python endpoints<br>- Hosted on Databricks<br>- Spark UDF integration<br>- MLflow model versioning<br>- Still separate: Databricks (DS), Postgres (Eng); ongoing data sync | Unifying logic, batch/online consistency | Developer-unfriendly interfaces, inefficient per-endpoint scaling, cumbersome inter-service calls, ongoing data sync | Platform must offer flexibility for dependencies & efficient scaling beyond isolated endpoints. Maintaining separate data stores increases operational complexity. |
| **3. FastAPI on Kubernetes** | - FastAPI microservices<br>- Self-managed Kubernetes<br>- Ray (Distributed Compute/Serve/Data)<br>- PostgreSQL, MLflow, Dagster, Kafka (CDC/SCD)<br>- Unified data storage: Data Engineers manage production Postgres directly | Flexibility, efficiency, control, LLM support, robust ops, eliminated data duplication | Higher initial/ongoing operational complexity (requires K8s/DevOps expertise, managing more parts) | Microservices on a flexible platform like K8s enable scalable, integrated MLOps but require significant operational capability. Unifying data storage is key for collaboration and consistency. |
