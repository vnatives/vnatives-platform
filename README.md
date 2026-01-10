# VNatives Platform

## 🌱 What is VNatives?

VNatives is a domain-driven, event-based e-commerce platform built to empower **native people** to sell their native products while preserving authenticity, transparency, and scalability.

The platform follows a **pure microservices architecture**, where each service is independently deployable, versioned, and scalable. Communication between services is primarily **event-driven using Kafka**.

This repository (`vnatives-platform`) acts as the **central entry point** for understanding the system architecture, workflows, and local setup.

---

## 🧭 High-Level Architecture

**Architecture Style**

* Microservices
* Event-driven (Kafka)
* Domain-driven design
* Cloud-native (AWS-ready)

**Core Principles**

* Independent deployability
* Loose coupling via events
* Strong consistency where required (Orders, Payments)
* Scalability for read-heavy workloads (Search, Analytics)

---

## 🧩 Service Landscape

### 👤 User Domain

* **vnatives-user-auth-service** – Authentication, JWT, roles
* **vnatives-user-profile-service** – Native & customer profiles

### 🛒 Commerce Domain

* **vnatives-commerce-shop-service** – Shop creation & management
* **vnatives-commerce-product-catalog-service** – Products & categories
* **vnatives-commerce-pricing-discount-service** – Pricing & offers

### 📦 Order Domain

* **vnatives-order-core-service** – Order lifecycle
* **vnatives-order-management-service** – Order tracking (Redis)
* **vnatives-order-review-rating-service** – Reviews & ratings

### 🔧 Supporting Services

* **vnatives-payment-service** – Payments & transactions
* **vnatives-search-service** – Product search (ElasticSearch)
* **vnatives-notification-service** – Email / SMS notifications
* **vnatives-media-service** – Image & video uploads (S3)
* **vnatives-analytics-archive-service** – Analytics & reporting

### 🧩 Shared Libraries

* **vnatives-common-entity-sdk** – Shared DTOs & event models
* **vnatives-kafka-retry-sdk** – Retry & DLQ handling

---

## 🔁 Core Workflows

### Native (Seller) Flow

1. Native registers using User Profile Service
2. Creates shop and products
3. Uploads media via Media Service
4. Configures pricing & discounts
5. Product and shop events published to Kafka
6. Search and Analytics services consume events asynchronously

### User (Customer) Flow

1. User authenticates via Auth Service
2. Searches products via Search Service
3. Views product details, reviews, and media
4. Places order
5. Completes payment (Saga-based flow)
6. Receives notifications
7. Tracks order status
8. User interactions published to Analytics

---

## 🗄️ Data Storage Strategy

| Service Type         | Technology                 | Reason                  |
| -------------------- | -------------------------- | ----------------------- |
| User, Order, Payment | MySQL (RDS)                | ACID compliance         |
| Product Catalog      | MongoDB                    | Schema flexibility      |
| Search               | ElasticSearch / OpenSearch | Full-text search        |
| Order Tracking       | Redis                      | Fast reads              |
| Media                | S3                         | Scalable object storage |

---

## 🧰 Tech Stack

* **Backend:** Java, Spring Boot
* **Messaging:** Kafka
* **Databases:** MySQL, MongoDB, Redis
* **Search:** ElasticSearch
* **Containerization:** Docker
* **Cloud:** AWS (ECS / EKS)
* **Monitoring:** Prometheus, Grafana

---

## 🏗️ Local Development (Planned)

A shared Docker Compose setup will provide:

* Kafka + Zookeeper
* MySQL
* MongoDB
* ElasticSearch
* Redis

This enables developers to run multiple services locally with minimal setup.

---

## 📌 Repository Purpose

This repository is intentionally **code-light** and **documentation-heavy**.

It serves as:

* Architectural reference
* Onboarding guide
* Interview walkthrough
* Single source of truth for VNatives

---

## 🚀 Next Milestones

* Finalize local Docker Compose
* Implement first vertical slice (Auth → User → Shop → Product → Search)
* Add architecture diagrams
* Document Kafka event schemas

---

## 👨‍💻 Author

**VNatives Platform** – Designed and implemented as a learning-focused, production-grade backend system.
