# Event Sourcing & CQRS with Axon and Spring Boot

This project demonstrates a **Bank Account Management** microservice architecture implementing **Event Sourcing** and **CQRS** (Command Query Responsibility Segregation) patterns using the **Axon Framework** and **Spring Boot**.

## Overview

The application is designed to separate the **Write Model** (Commands) from the **Read Model** (Queries), ensuring scalability and flexibility.

-   **Command Side**: Handles state changes via Commands and Aggregates. Events are stored in an Event Store.
-   **Query Side**: Listens to events and updates a relational database (Projections) for efficient querying.
-   **Real-time Updates**: Uses Server-Sent Events (SSE) to push account updates to clients in real-time.

## Technologies

-   **Java 17**
-   **Spring Boot 3.2.2**
-   **Axon Framework 4.8.0**
-   **Spring Data JPA**
-   **H2 Database** (In-memory for Event Store and Read Model)
-   **Spring WebFlux** (For SSE)
-   **Lombok**
-   **SpringDoc OpenAPI** (Swagger UI)

## Architecture

### Command Model (Write)
-   **Aggregates**: `AccountAggregate`
-   **Commands**: `CreateAccountCommand`, `CreditAccountCommand`, `DebitAccountCommand`
-   **Events**: `AccountCreatedEvent`, `AccountActivatedEvent`, `AccountCreditedEvent`, `AccountDebitedEvent`

### Query Model (Read)
-   **Entities**: `Account`, `AccountOperation`
-   **Projections**: `AccountServiceHandler` updates the Read Database.
-   **Queries**: `GetAccountQuery`, `GetAllAccountsQuery`

##  How to Run

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/MAHDIBATIR/CQRS-and-Event-Sourcing.git
    cd CQRS-and-Event-Sourcing
    ```

2.  **Build the project**:
    ```bash
    ./mvnw clean package
    ```

3.  **Run the application**:
    ```bash
    ./mvnw spring-boot:run
    ```

4.  **Access Swagger UI**:
    ```
    http://localhost:8082/swagger-ui.html
    ```

5.  **Access H2 Console**:
    ```
    http://localhost:8082/h2-console
    ```

## API Endpoints

### Command Side (Write)
-   `POST /commands/account/create` - Create new account
-   `PUT /commands/account/credit` - Credit account
-   `PUT /commands/account/debit` - Debit account

### Query Side (Read)
-   `GET /query/accounts/allAccounts` - Get all accounts
-   `GET /query/accounts/byId/{id}` - Get account by ID
-   `GET /query/accounts/watch/{id}` - Subscribe to real-time updates (SSE)

## Project Structure

```
src/main/java/com/example/eventsourcingandcqrswithaxonandspringboot/
├── commands/
│   ├── aggregates/          # AccountAggregate
│   └── controllers/         # Command Controllers
├── commonapi/
│   ├── commands/            # Command classes
│   ├── events/              # Event classes
│   ├── dtos/                # Data Transfer Objects
│   ├── enums/               # Enumerations
│   └── queries/             # Query classes
├── query/
│   ├── entities/            # JPA Entities
│   ├── repositories/        # Spring Data Repositories
│   ├── service/             # Query Services & Event Handlers
│   └── controllers/         # Query Controllers
└── config/                  # Configuration classes
```

## 🔧 Configuration

The application uses H2 in-memory database by default. Configuration can be modified in `application.properties`.
