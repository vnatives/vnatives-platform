VNatives Platform

An Event-Driven, Microservices-Based Commerce System (Production-Grade Learning Project)

🚀 Overview

VNatives is a distributed e-commerce backend platform designed using microservices, event-driven architecture, and domain-driven design principles.

The platform is built to simulate real-world, large-scale backend systems where:

Services are independently deployable

Data ownership is strictly enforced

Communication happens asynchronously via events

Read and write workloads are intentionally separated

This repository represents the platform-level view of VNatives and acts as the system entry point for understanding architecture, services, and workflows.

🎯 Purpose of This Project

This project is built to demonstrate MAANG-level backend engineering thinking, not just feature implementation.

It focuses on:

Designing scalable microservices

Handling distributed workflows

Event-based communication using Kafka

Data consistency and isolation

Cloud-ready, containerized systems

VNatives is a learning-to-production bridge project that reflects how real backend systems are designed, not just how APIs are written.

🧠 Core Engineering Principles

Microservices Architecture

Event-Driven Communication

Domain-Driven Design (DDD)

Database per Service

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
Async Consumers (Search, Analytics-ready)

Each service:

Owns its database

Publishes domain events

Consumes only required events

Can scale independently

🧩 Current Service Landscape
🛒 Commerce Domain
Service	Responsibility
vnatives-commerce-shop-service	Seller shop onboarding & management
vnatives-commerce-product-catalog-service	Product & category management
vnatives-commerce-inventory-service	Inventory & stock tracking
vnatives-commerce-pricing-discount-service	Pricing rules & discounts
📦 Order Domain
Service	Responsibility
vnatives-order-core-service	Order creation & lifecycle management
vnatives-payment-service	Payment processing & transactions
vnatives-review-rating-service	Product reviews & ratings
🔍 Search Domain
Service	Responsibility
vnatives-search-consumer	Kafka consumer for indexing product events
vnatives-search-service	Product search APIs (ElasticSearch)
👤 User Domain
Service	Responsibility
vnatives-user-profile-service	User & seller profile management
🔐 Platform & Infrastructure
Component	Responsibility
vnatives-security-gateway	API Gateway & request security
vnatives-common-sdk	Shared DTOs, events, and constants
vnatives-infra	Infrastructure configs (Docker, Kafka, DBs)
🔁 Core Workflows
🧑‍🌾 Seller (Native) Flow

Seller profile created

Shop created

Products added

Inventory & pricing configured

Product events published to Kafka

Search consumer indexes products asynchronously

Key Idea:
Commerce services never directly call Search — events drive the system.

🛍️ Customer Flow

User searches products via Search Service

Views product details & reviews

Places an order

Payment processed

Order lifecycle updated

Read-heavy operations optimized separately

🗄️ Data Storage Strategy
Use Case	Technology	Reason
Orders & Payments	MySQL	ACID consistency
Product Catalog	MongoDB	Flexible schema
Inventory	MySQL	Strong consistency
Search	ElasticSearch	Fast full-text search
Caching (future)	Redis	Low-latency reads
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
