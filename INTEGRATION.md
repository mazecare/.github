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
graph LR
    A1[Hospital] & A2[Clinic] & A3[Lab] & A4[Pharmacy] & A5[Patient Portal] & A6[Insurance] & A7[TPA Systems] --> B(API Gateway);

    B --> C1([auth-service]);
    B --> C2([product-service]);
    B --> C3([case-service]);
    B --> C4([encounter-service]);
    B --> C5([record-service]);
    B --> C6([entity-service]);
    B --> C7([file-service]);
    B --> C8([booking-service]);
    B --> C9([inventory-service]);
    B --> C10([accounting-service]);
    B --> C11([message-service]);
    B --> C12([payment-service]);
    B --> C13([order-service]);
    B --> C14([contract-service]);
    B --> C15([claim-service]);
    B --> C16([marketing-service]);
    B --> C17([template-service]);

    C1 --> D[Data];
    C2 --> D[Data];
    C3 --> D[Data];
    C4 --> D[Data];
    C5 --> D[Data];
    C6 --> D[Data];
    C7 --> D[Data];
    C8 --> D[Data];
    C9 --> D[Data];
    C10 --> D[Data];
    C11 --> D[Data];
    C12 --> D[Data];
    C13 --> D[Data];
    C14 --> D[Data];
    C15 --> D[Data];
    C16 --> D[Data];
    C17 --> D[Data];

    D --> D1((Database));
    D --> D2[File System];
    D --> D3[Datalake];

    style D1 fill:#fffacd,stroke:#333,stroke-width:2px;
    style D2 fill:#fffacd,stroke:#333,stroke-width:2px;
    style D3 fill:#fffacd,stroke:#333,stroke-width:2px;

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
