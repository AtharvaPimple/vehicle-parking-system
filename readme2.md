# Vehicle Parking Management System (VPMS)

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Architecture Diagram](#architecture-diagram)
- [Module Overview](#module-overview)
  - [Parking Spot Service](#parking-spot-service)
  - [Reservation Service](#reservation-service)
  - [User Service](#user-service)
  - [Notification Service](#notification-service)
- [API Gateway](#api-gateway)
- [Discovery Server (Eureka)](#discovery-server-eureka)
- [Setup Instructions](#setup-instructions)
- [Testing](#testing)
- [Advanced Features](#advanced-features)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

The **Vehicle Parking Management System (VPMS)** is a backend system built using a microservices architecture. It manages parking spot allocation, user registrations, reservations, and real-time notifications. The system exposes RESTful APIs and supports relational databases like **MySQL**, **PostgreSQL**, and **H2** (for development).

---

## Features

- **Parking Spot Management:** Real-time tracking and status updates.
- **Reservation Management:** Bookings, modifications, and cancellations.
- **User Management:** Secure registration, authentication, and role-based access.
- **Notifications:** System updates and reservation alerts via email/SMS.

---

## Technologies Used

| Layer        | Technology               |
|--------------|---------------------------|
| Backend      | Spring Boot (Java)        |
| ORM          | Hibernate / JPA           |
| Databases    | MySQL, PostgreSQL, H2     |
| Security     | Spring Security + JWT     |
| Documentation| Swagger / OpenAPI         |
| Logging      | SLF4J + Logback           |
| Testing      | JUnit + Mockito           |

---

## Architecture Diagram
```mermaid
flowchart TD

  subgraph Client [Client Applications]
    A[Web App]
    B[Mobile App]
  end

  subgraph Gateway [API Gateway]
    C[API Gateway]
  end

  subgraph Infra [Infrastructure Services]
    D[Load Balancer]
    E[Discovery Service]
    F[Config Service]
  end

  subgraph Services [Microservices]
    G[User Management Service] --> GDB[(User DB)]
    H[Parking Slot Management Service] --> HDB[(Parking Slot DB)]
    I[Vehicle Entry & Exit Logging Service] --> IDB[(Vehicle Log DB)]
    J[Reservation Service] --> JDB[(Reservation DB)]
    K[Billing and Payments Service] --> KDB[(Billing DB)]
  end

  subgraph External [External Services]
    M[Payment Gateway]
  end

  %% Connections
  A --> C
  B --> C
  C --> D
  D --> E
  D --> F
  C --> G
  C --> H
  C --> I
  C --> J
  C --> K
  K --> M

  %% Styling
  classDef client fill:#e3f2fd,stroke:#2196f3,color:#0d47a1
  classDef gateway fill:#fff3e0,stroke:#ff9800,color:#e65100
  classDef infra fill:#ede7f6,stroke:#673ab7,color:#311b92
  classDef service fill:#e8f5e9,stroke:#4caf50,color:#1b5e20
  classDef external fill:#fce4ec,stroke:#f06292,color:#880e4f
  classDef db fill:#f3e5f5,stroke:#ab47bc,color:#4a148c

  class A,B client
  class C gateway
  class D,E,F infra
  class G,H,I,J,K service
  class M external
  class GDB,HDB,IDB,JDB,KDB db

```
