🌱 VNatives Platform
Event-Driven Microservices Commerce System

(Production-Grade Learning Project)

🚀 Overview

VNatives is a distributed e-commerce backend platform designed using:

Microservices architecture

Event-driven communication

Domain-Driven Design (DDD)

The goal is to simulate real-world, large-scale backend systems, not just CRUD APIs.

What this platform demonstrates

✔ Independent service deployment
✔ Strict data ownership
✔ Asynchronous communication via events
✔ Clear separation of read & write workloads

This repository provides a platform-level view of the system architecture, services, and workflows.

🎯 Why This Project Exists

This project is intentionally built to showcase MAANG-level backend engineering thinking.

It focuses on:

Designing scalable microservices

Handling distributed workflows

Event-based communication using Kafka

Data consistency & isolation

Cloud-ready, containerized systems

VNatives bridges the gap between learning projects and production-grade backend systems.

🧠 Core Engineering Principles

Microservices Architecture

Event-Driven Communication

Domain-Driven Design (DDD)

Database-per-Service

Asynchronous Processing

Loose Coupling via Kafka

Cloud-Native & Container-Ready

🏗️ High-Level Architecture
Clients
   ↓
Security Gateway
   ↓
Domain Microservices
   ↓
Kafka (Event Backbone)
   ↓
Async Consumers (Search, Read Models)
Design Characteristics

Each service owns its database

Services publish domain events

Services consume only required events

Every service scales independently

🧩 Current Service Landscape
🛒 Commerce Domain
Service	Responsibility
vnatives-commerce-shop-service	Seller shop onboarding & management
vnatives-commerce-product-catalog-service	Product & category management
vnatives-commerce-inventory-service	Inventory & stock tracking
vnatives-commerce-pricing-discount-service	Pricing rules & discounts
📦 Order Domain
Service	Responsibility
vnatives-order-core-service	Order creation & lifecycle
vnatives-payment-service	Payment processing
vnatives-review-rating-service	Product reviews & ratings
🔍 Search Domain
Service	Responsibility
vnatives-search-consumer	Kafka consumer for indexing
vnatives-search-service	Product search APIs (ElasticSearch)
👤 User Domain
Service	Responsibility
vnatives-user-profile-service	User & seller profile management
🔐 Platform & Infrastructure
Component	Responsibility
vnatives-security-gateway	API Gateway & request security
vnatives-common-sdk	Shared DTOs & event contracts
vnatives-infra	Docker, Kafka & DB infrastructure
🔁 Core Workflows
🧑‍🌾 Seller (Native) Flow

Seller profile created

Shop created

Products added

Inventory & pricing configured

Domain events published to Kafka

Search consumer indexes products asynchronously

Key Design Insight

Commerce services never directly call Search — events drive the system.

🛍️ Customer Flow

User searches products via Search Service

Views product details & reviews

Places an order

Payment is processed

Order lifecycle is updated

Read-heavy operations are optimized separately from write workflows.

🗄️ Data Storage Strategy
Use Case	Technology	Reason
Orders & Payments	MySQL	ACID consistency
Product Catalog	MongoDB	Flexible schema
Inventory	MySQL	Strong consistency
Search	ElasticSearch	Full-text search
Caching (planned)	Redis	Low-latency reads
🧰 Tech Stack

Language: Java

Framework: Spring Boot

Messaging: Apache Kafka

Databases: MySQL, MongoDB

Search Engine: ElasticSearch

Containerization: Docker

Build Tool: Maven

Cloud Target: AWS (ECS / EKS ready)

🧪 Local Development

Infrastructure is managed via vnatives-infra and includes:

Kafka & Zookeeper

MySQL

MongoDB

ElasticSearch

Each service can be run independently or together using Docker Compose.

👨‍💻 Author

Sundar Pirabu Raj R
Backend Engineer | Java | Spring Boot | Distributed Systems
📍 Chennai, India

📜 License

Apache License 2.0
