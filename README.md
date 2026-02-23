# 🌱 VNatives  
## Event-Driven Microservices Commerce Platform  
### Production-Grade Backend Engineering Project

VNatives is a large-scale, distributed e-commerce backend platform built to demonstrate **real-world backend engineering** — not CRUD tutorials.

This project showcases how modern commerce systems are designed using **microservices**, **event-driven architecture**, and **domain-driven design (DDD)**, similar to production systems used at scale.

---

## 🚀 Why VNatives?

- Designing scalable microservices  
- Handling distributed workflows  
- Event-driven data propagation  
- Read / write workload separation  
- Strict data ownership & isolation  
- Cloud-ready containerized systems  

**VNatives bridges the gap between learning projects and production-grade backend systems.**

---

## 🧠 Core Engineering Principles

- Microservices Architecture  
- Event-Driven Communication (Kafka)  
- Domain-Driven Design (DDD)  
- Database-per-Service  
- Asynchronous Processing  
- Loose Coupling via Events  
- Cloud-Native & Container-Ready  

---


### Design Characteristics

- Each service owns its own database  
- Services publish domain events  
- Services consume only required events  
- No direct service-to-service coupling  
- Every service scales independently  

---

## 🧩 Service Landscape

### 🛒 Commerce Domain

| Service | Responsibility |
|------|---------------|
| vnatives-commerce-shop-service | Seller shop onboarding & management |
| vnatives-commerce-product-catalog-service | Product & category management |
| vnatives-commerce-inventory-service | Inventory & stock tracking |
| vnatives-commerce-pricing-discount-service | Pricing rules & discounts |

---

### 📦 Order Domain

| Service | Responsibility |
|------|---------------|
| vnatives-order-core-service | Order creation & lifecycle |
| vnatives-payment-service | Payment processing |
| vnatives-review-rating-service | Product reviews & ratings |

---

### 🔍 Search Domain

| Service | Responsibility |
|------|---------------|
| vnatives-search-consumer | Kafka consumer for indexing |
| vnatives-search-service | Product search APIs (ElasticSearch) |

---

### 👤 User Domain

| Service | Responsibility |
|------|---------------|
| vnatives-user-profile-service | User & seller profile management |

---

### 🔐 Platform & Infrastructure

| Component | Responsibility |
|------|---------------|
| vnatives-security-gateway | API Gateway & request security |
| vnatives-common-sdk | Shared DTOs & event contracts |
| vnatives-infra | Docker, Kafka & database infrastructure |

---

## 🔁 Core Workflows

### 🧑‍🌾 Seller (Native) Flow

1. Seller profile created  
2. Shop onboarded  
3. Products added  
4. Inventory & pricing configured  
5. Domain events published to Kafka  
6. Search indexes updated asynchronously  

**Key Design Insight:**  
Commerce services never directly call Search services.  
**Events drive the system — not synchronous REST calls.**

---

### 🛍️ Customer Flow

1. User searches products via Search Service  
2. Views product details & reviews  
3. Places an order  
4. Payment is processed  
5. Order lifecycle is updated asynchronously  

Read-heavy operations are optimized separately from write workflows.

---

## 🗄️ Data Storage Strategy

| Use Case | Technology | Reason |
|------|----------|-------|
| Orders & Payments | MySQL | ACID consistency |
| Product Catalog | MongoDB | Flexible schema |
| Inventory | MySQL | Strong consistency |
| Search | ElasticSearch | Full-text search |
| Caching (Planned) | Redis | Low-latency reads |

---

## 🧰 Tech Stack

- **Language:** Java  
- **Framework:** Spring Boot  
- **Messaging:** Apache Kafka  
- **Databases:** MySQL, MongoDB  
- **Search Engine:** ElasticSearch  
- **Caching:** Redis (planned)  
- **Containerization:** Docker  
- **Build Tool:** Maven  
- **Cloud Target:** AWS (ECS / EKS ready)  

---

## 🧪 Local Development

Infrastructure is managed via `vnatives-infra` and includes:

- Kafka & Zookeeper  
- MySQL  
- MongoDB  
- ElasticSearch  

Each service:

- Can run independently  
- Can be started together via Docker Compose  
- Mirrors production-style deployment  

---

## 🎯 What Recruiters Should Notice

This project demonstrates **how I think as a backend engineer**, not just how I write code.

- Real microservices boundaries  
- Event-driven architecture (no REST chaining)  
- Database-per-service discipline  
- Read / write workload separation  
- Cloud-ready deployment mindset  
- Production-grade design decisions  

---

## 👨‍💻 Author

**Sundar Pirabu Raj R**  
Backend Engineer | Java | Spring Boot | Distributed Systems  
Chennai, India  

---

## 📜 License

Apache License 2.0


