# Integrating with Mazecare: FAQ and Architectural Diagrams

This document provides a framework for creating a Frequently Asked Questions (FAQ) section and architectural diagrams for integrating with Mazecare (www.mazecare.com). Please replace the placeholder information with specific details from Mazecare's API documentation. You can find our API portal here: https://api-hk-dev.mazecare.com/graphql/

## General FAQ

* **Q: What are the benefits of integrating with Mazecare?**
    * A: Streamlined data exchange between all application using Mazecare as a backend
* **Q: What types of systems can integrate with Mazecare?**
    * A: EHR/EMR systems, Clinic Management Systems, Hospital Information Systems, patient applications, claim management systems, CRM systems, billing platforms, IoT devices, etc.)
* **Q: Does Mazecare provide an API for integration?**
    * A: Yes, Mazecare provides a complete GraphQL set of APIs. Currenctly more 700 apis (queries, mutations, subscriptions)
* **Q: What authentication methods does Mazecare use?**
    * A: OAuth 2.0 and Bearer JWT tokens
* **Q: Is there a developer portal or documentation available?**
    * A: Not yet, but we are currently building one
* **Q: Are webhooks supported?**
    * A: Not yet but we will build webhook capabilities if there is a need for it for any client.
* **Q: Can Mazecare be self-hosted?**
    * A: Yes, the entire Mazecare system can be self-hosted using Docker.
* **Q: Where can Mazecare be deployed?**
    * A: Mazecare can be deployed in various cloud environments or on-premises, either in Mazecare's infrastructure or the client's infrastructure.

## Technical FAQ

* **Q: What data formats does the Mazecare API use?**
    * A: JSON
* **Q: How do I handle authentication with the Mazecare API?**
    * A: You need to call the graphQL mutation `generateAccessToken` and insert the bearer token in the `Authorization` header
* **Q: What are the best practices for handling errors?**
    * A: Errors are handled and sent back to you using the standard GrahpQL format.
* **Q: Are there any code samples or SDKs available?**
    * A: Not yet but we will build webhook capabilities if there is a need for it for any client.

## Architectural Diagrams (Conceptual)

```mermaid
graph TD
    A[Applications] --> B(API Gateway);
    B --> C{Backend / Microservices};
    C --> D[Data];

    subgraph Applications
        direction LR;
        A1[Hospital] & A2[Clinic] & A3[Lab] & A4[Pharmacy] & A5[Patient Portal] & A6[Insurance] & A7[TPA Systems]
        style A1 fill:#e0f7fa,stroke:#333,stroke-width:2px;
        style A2 fill:#e0f7fa,stroke:#333,stroke-width:2px;
        style A3 fill:#e0f7fa,stroke:#333,stroke-width:2px;
        style A4 fill:#e0f7fa,stroke:#333,stroke-width:2px;
        style A5 fill:#e0f7fa,stroke:#333,stroke-width:2px;
        style A6 fill:#e0f7fa,stroke:#333,stroke-width:2px;
        style A7 fill:#e0f7fa,stroke:#333,stroke-width:2px;
        A1 --> B;
        A2 --> B;
        A3 --> B;
        A4 --> B;
        A5 --> B;
        A6 --> B;
        A7 --> B;
    end

    subgraph Backend / Microservices
        C1([auth-service])
        C2([product-service])
        C3([case-service])
        C4([encounter-service])
        C5([record-service])
        C6([entity-service])
        C7([file-service])
        C8([booking-service])
        C9([inventory-service])
        C10([accounting-service])
        C11([message-service])
        C12([payment-service])
        C13([order-service])
        C14([contract-service])
        C15([claim-service])
        C16([marketing-service])
        C17([template-service])
        style C1 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C2 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C3 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C4 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C5 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C6 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C7 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C8 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C9 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C10 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C11 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C12 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C13 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C14 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C15 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C16 fill:#f0fff0,stroke:#333,stroke-width:2px;
        style C17 fill:#f0fff0,stroke:#333,stroke-width:2px;
        C1 --> D;
        C2 --> D;
        C3 --> D;
        C4 --> D;
        C5 --> D;
        C6 --> D;
        C7 --> D;
        C8 --> D;
        C9 --> D;
        C10 --> D;
        C11 --> D;
        C12 --> D;
        C13 --> D;
        C14 --> D;
        C15 --> D;
        C16 --> D;
        C17 --> D;
    end

    subgraph Data
        D1((Database))
        D2[File System]
        D3[Datalake]
        style D1 fill:#fffacd,stroke:#333,stroke-width:2px;
        style D2 fill:#fffacd,stroke:#333,stroke-width:2px;
        style D3 fill:#fffacd,stroke:#333,stroke-width:2px;
    end

    subgraph "Deployable Anywhere"
        B
    end

    E[Connect to Third Party Systems]
    style B fill:#f9f,stroke:#333,stroke-width:2px;
```

### 1. API Integration:

```mermaid
sequenceDiagram
    participant Your System
    participant Mazecare API
    participant Mazecare Auth Service
    participant Mazecare Database

    Your System->>Mazecare Auth Service: Request Access Token (Credentials)
    Mazecare Auth Service-->>Your System: Access Token (JWT)

    Your System->>Mazecare API: Request (e.g., Get Patient Data) with Authorization Header (Bearer Token)
    Mazecare API->>Mazecare Auth Service: Validate Token
    Mazecare Auth Service-->>Mazecare API: Token Validated
    Mazecare API->>Mazecare Database: Query Data
    Mazecare Database-->>Mazecare API: Response Data
    Mazecare API-->>Your System: Response (e.g., Patient Data)
```
