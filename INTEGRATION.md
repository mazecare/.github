# Integrating with Mazecare: FAQ and Architectural Diagrams

This document provides a framework for creating a Frequently Asked Questions (FAQ) section and architectural diagrams for integrating with Mazecare (www.mazecare.com). Please replace the placeholder information with specific details from Mazecare's API documentation. You can find our API portal here: https://api-hk-dev.mazecare.com/graphql/

## General FAQ

* **Q: What are the benefits of integrating with Mazecare?**
    * A: Streamlined data exchange between all application using Mazecare as a backend
* **Q: What types of systems can integrate with Mazecare?**
    * A: EHR/EMR systems, Clinic Management Systems, Hospital Information Systems, patient applications, claim management systems, CRM systems, billing platforms, IoT devices, etc.)
* **Q: Does Mazecare provide an API for integration?**
    * A: Yes, Mazecare provides a complete GraphQL set of APIs. Currenctly more 700 apis (questies, mutations, subscriptions)
* **Q: What authentication methods does Mazecare use?**
    * A: OAuth 2.0 and Bearer JWT tokens
* **Q: Is there a developer portal or documentation available?**
    * A: Not yet, but we are currently building one
* **Q: Are webhooks supported?**
    * A: Not yet but we will build webhook capabilities if there is a need for it for any client.

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
    A[Applications] --> B(API Gateway);
    B --> C[Backend / Microservices];
    C --> D[Data];

    subgraph Applications
        A1[Hospital]
        A2[Clinic]
        A3[Lab]
        A4[Pharmacy]
        A5[Member / Patient Portal]
        A6[Insurance]
        A7[TPA Systems]
        A1 --> B;
        A2 --> B;
        A3 --> B;
        A4 --> B;
        A5 --> B;
        A6 --> B;
        A7 --> B;
    end

    subgraph Backend / Microservices
        C1[Prescription]
        C2[Inventory]
        C3[Appointments / Booking]
        C4[Queues / Ticketing]
        C5[Medical Records]
        C6[Insurance Policies]
        C7[Claims]
        C8[Insurance Plans]
        C9[Claim Adjudication Engine]
        C10[Document / File Management]
        C11[Messages / Notifications]
        C12[Contract Management]
        C13[Billing / Accounting]
        C14[Authentication / Authorization]
        C15[Datalake Feed]
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
    end

    subgraph Data
        D1[Any Database]
        D2[Any File System]
        D3[Any Datalake]
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
    participant Mazecare Database

    Your System->>Mazecare API: Request (e.g., Get Patient Data)
    Mazecare API->>Mazecare Database: Query Data
    Mazecare Database-->>Mazecare API: Response Data
    Mazecare API-->>Your System: Response (e.g., Patient Data)
```
