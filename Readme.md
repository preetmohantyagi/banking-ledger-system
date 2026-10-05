

````markdown
# 🏦 Banking Ledger & Transaction Management System

A backend banking ledger system built with **Node.js, Express.js, MongoDB, and Mongoose** for managing accounts, financial transactions, ledger entries, and account balances.

The project follows a **modular and layered backend architecture**, separating routes, controllers, services, models, middleware, and configuration to keep the application organized, maintainable, and scalable.

---

## 🚀 Features

- 👤 Account management
- 💳 Debit and Credit transaction handling
- 📒 Ledger-based transaction tracking
- 💰 Automatic account balance calculation
- 🔄 RESTful API architecture
- 🗄️ MongoDB database integration
- 🧩 Mongoose schemas and models
- 🛡️ Middleware-based request processing
- 📁 Modular backend architecture
- ⚙️ Environment-based configuration
- 🔗 Separation of routes, controllers, services, and models

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **Node.js** | JavaScript runtime |
| **Express.js** | Backend web framework |
| **MongoDB** | Database |
| **Mongoose** | MongoDB ODM |
| **JavaScript** | Programming language |
| **REST API** | Client-server communication |
| **Git & GitHub** | Version control |

---

# 🏗️ System Architecture

The application follows a modular backend architecture where each layer has a specific responsibility.

```text
                         ┌──────────────────────┐
                         │       CLIENT         │
                         │  Postman / Frontend  │
                         └──────────┬───────────┘
                                    │
                                    │ HTTP Request
                                    ▼
                         ┌──────────────────────┐
                         │        ROUTES        │
                         │   API Endpoints      │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │     MIDDLEWARE       │
                         │ Validation / Request │
                         │     Processing       │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │     CONTROLLERS      │
                         │ Request / Response   │
                         │      Handling        │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │      SERVICES        │
                         │    Business Logic    │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │       MODELS         │
                         │ Mongoose Schemas     │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │       MONGODB        │
                         │  Persistent Storage   │
                         └──────────────────────┘
```

---

# 📂 Project Structure

```text
banking-ledger-system/
│
├── src/
│   │
│   ├── config/
│   │   └── Database configuration
│   │
│   ├── controllers/
│   │   └── Request and response handling
│   │
│   ├── middleware/
│   │   └── Middleware functions
│   │
│   ├── models/
│   │   ├── accountModel
│   │   └── ledgerModel
│   │
│   ├── routes/
│   │   └── API route definitions
│   │
│   ├── services/
│   │   └── Business logic
│   │
│   └── app.js
│
├── .env
├── server.js
├── package.json
├── package-lock.json
└── README.md
```

---

# 🧩 Architecture Components

## Routes

The `routes` layer defines the API endpoints exposed by the application.

Responsibilities:

- Define API endpoints
- Handle HTTP methods
- Connect endpoints with controllers
- Keep routing separate from business logic

```text
HTTP Request
      │
      ▼
    Route
      │
      ▼
 Controller
```

---

## Controllers

Controllers handle incoming requests and prepare responses.

They act as the bridge between routes and the application's business logic.

```text
Routes
   │
   ▼
Controllers
   │
   ▼
Services
```

Controllers primarily handle:

- Request data
- Calling required services
- Sending HTTP responses
- Handling request-level errors

---

## Services

The `services` layer contains the core business logic of the application.

It helps keep complex operations outside controllers and makes the backend easier to maintain.

Examples include:

- Account operations
- Transaction processing
- Ledger operations
- Balance-related operations

```text
Controller
     │
     ▼
  Service
     │
     ▼
   Model
```

---

## Models

The `models` layer contains the MongoDB/Mongoose schemas and models.

### Account Model

Represents a bank account and its related information.

### Ledger Model

Represents individual financial transactions associated with an account.

A ledger transaction contains information such as:

```text
Account
Transaction Type
Amount
Timestamp
```

Transaction types:

```text
CREDIT
DEBIT
```

---

## Middleware

Middleware runs between the incoming request and the controller.

It can be used for:

- Request validation
- Authentication
- Authorization
- Request processing
- Error handling

```text
Request
   │
   ▼
Middleware
   │
   ▼
Controller
```

---

## Config

The `config` directory contains application configuration such as the database connection.

Keeping configuration separate from business logic makes the application easier to configure and maintain.

---

# 🔄 Complete Request Flow

A typical request follows this flow:

```text
                    HTTP Request
                         │
                         ▼
                  ┌─────────────┐
                  │    Routes   │
                  └──────┬──────┘
                         │
                         ▼
                  ┌─────────────┐
                  │ Middleware  │
                  └──────┬──────┘
                         │
                         ▼
                  ┌─────────────┐
                  │ Controllers │
                  └──────┬──────┘
                         │
                         ▼
                  ┌─────────────┐
                  │  Services   │
                  └──────┬──────┘
                         │
                         ▼
                  ┌─────────────┐
                  │   Models    │
                  └──────┬──────┘
                         │
                         ▼
                  ┌─────────────┐
                  │  MongoDB    │
                  └──────┬──────┘
                         │
                         ▼
                  Database Result
                         │
                         ▼
                  Service Response
                         │
                         ▼
                     Controller
                         │
                         ▼
                   HTTP Response
```

---

# 💰 Ledger System

The core concept of this application is a **ledger-based transaction system**.

Instead of simply storing a manually updated balance, the account's balance can be derived from its transaction history.

Example:

```text
Account
   │
   ├── CREDIT  ₹10,000
   ├── DEBIT   ₹2,000
   ├── DEBIT   ₹1,000
   └── CREDIT  ₹5,000
```

The balance is calculated using:

```text
Balance = Total Credits - Total Debits
```

For the above example:

```text
Total Credits = ₹15,000

Total Debits = ₹3,000

Balance = ₹15,000 - ₹3,000

Balance = ₹12,000
```

---

# 🧮 Balance Calculation Flow

The account balance is calculated by aggregating ledger transactions belonging to the account.

```text
                 Ledger Transactions
                         │
                         ▼
                Filter by Account
                         │
                         ▼
                 ┌──────────────┐
                 │  Aggregation │
                 └───────┬──────┘
                         │
             ┌───────────┴───────────┐
             ▼                       ▼
       Total CREDIT             Total DEBIT
             │                       │
             └───────────┬───────────┘
                         ▼
                CREDIT - DEBIT
                         │
                         ▼
                  Account Balance
```

MongoDB aggregation is used to calculate the total debit and credit values for an account.

---

# 💳 Transaction Flow

When a new transaction is created, it follows the backend flow:

```text
             Client
                │
                │ Create Transaction
                ▼
        ┌─────────────────┐
        │ Transaction     │
        │ Route           │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ Transaction     │
        │ Controller      │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ Transaction     │
        │ Service         │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │ Ledger Model    │
        └────────┬────────┘
                 │
                 ▼
             MongoDB
                 │
                 ▼
        Transaction Stored
```

Once stored, the transaction becomes part of the account's ledger history.

---

# 🏦 Account & Ledger Relationship

The relationship between an account and its transactions can be visualized as:

```text
                   ACCOUNT
                      │
                      │
          ┌───────────┼───────────┐
          │           │           │
          ▼           ▼           ▼
       Ledger      Ledger      Ledger
     Transaction  Transaction  Transaction
          │           │           │
          ▼           ▼           ▼
       CREDIT       DEBIT       CREDIT
```

Each ledger entry belongs to an account and contributes to the account's calculated balance.

---

# 📊 Example

Suppose an account has the following transactions:

| Transaction | Type | Amount |
|---|---|---:|
| T1 | CREDIT | ₹10,000 |
| T2 | DEBIT | ₹2,500 |
| T3 | CREDIT | ₹5,000 |
| T4 | DEBIT | ₹1,000 |

Calculation:

```text
Credits = ₹10,000 + ₹5,000
        = ₹15,000

Debits = ₹2,500 + ₹1,000
       = ₹3,500

Balance = ₹15,000 - ₹3,500

Balance = ₹11,500
```

---

# 🔌 REST API Architecture

The backend exposes RESTful APIs using Express.js.

The general API organization follows:

```text
/api
│
├── accounts
│
└── transactions
```

The exact endpoints depend on the current implementation of the project.

The API layer is responsible for communication between the client and backend application.

```text
Client
  │
  │ HTTP / JSON
  ▼
Express.js API
  │
  ▼
Business Logic
  │
  ▼
MongoDB
```

---

# 🗄️ Database Layer

MongoDB is used as the primary database.

Mongoose provides:

- Schema definitions
- Model creation
- Database interaction
- Data validation
- Query operations
- Aggregation support

The main data entities are:

```text
MongoDB
   │
   ├── Accounts
   │
   └── Ledger Transactions
```

---

# 🔐 Environment Configuration

Sensitive configuration values are stored using environment variables.

Example:

```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
```

The `.env` file should not be committed to GitHub.

Add it to `.gitignore`:

```text
.env
node_modules/
```

---

# ⚙️ Installation & Setup

## 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/banking-ledger-system.git
```

## 2. Navigate to the Project

```bash
cd banking-ledger-system
```

## 3. Install Dependencies

```bash
npm install
```

## 4. Configure Environment Variables

Create a `.env` file in the root directory:

```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
```

## 5. Start the Server

```bash
npm start
```

For development:

```bash
npm run dev
```

---

# 🧪 API Testing

The REST APIs can be tested using tools such as:

- Postman
- Thunder Client
- REST Client

A typical testing flow:

```text
Create Account
      │
      ▼
Create Transaction
      │
      ▼
Add CREDIT / DEBIT
      │
      ▼
Fetch Account
      │
      ▼
Calculate Balance
```

---

# 📌 Key Concepts Demonstrated

This project demonstrates practical experience with:

- Node.js backend development
- Express.js
- REST API development
- MongoDB
- Mongoose
- Modular backend architecture
- Routes
- Controllers
- Services
- Middleware
- Database models
- MongoDB aggregation
- Debit/Credit transactions
- Ledger-based accounting
- Account balance calculation
- Environment configuration
- Separation of concerns
- Backend API architecture

---

# 🎯 Why This Project?

The project was built to understand how a real-world backend system can be structured using a modular architecture.

It focuses on:

```text
API Design
    +
Business Logic
    +
Database Management
    +
Transaction Processing
    +
Ledger Architecture
```

The project demonstrates how individual backend layers work together to process a request from the client, execute business logic, interact with the database, and return a response.

---

# 🔮 Future Improvements

Potential improvements include:

- JWT authentication
- Role-based authorization
- Transaction pagination
- Advanced transaction filtering
- Swagger/OpenAPI documentation
- Unit and integration testing
- Docker containerization
- Logging and monitoring
- Transaction idempotency
- Cloud deployment

---

# 👨‍💻 Author

**Preet Mohan Tyagi**

B.Tech CSE (AI/ML) | Full-Stack Developer

GitHub:  
https://github.com/preetmohantyagi

LinkedIn:  
https://linkedin.com/in/preetmohantyagi/

---

# ⭐ Project Summary

**Banking Ledger & Transaction Management System** is a modular Node.js backend designed to manage accounts and financial transactions using a ledger-based approach.

The system demonstrates practical implementation of **REST APIs, Express.js, MongoDB, Mongoose, layered backend architecture, transaction processing, and account balance calculation**.

```text
Client
  │
  ▼
Routes
  │
  ▼
Middleware
  │
  ▼
Controllers
  │
  ▼
Services
  │
  ▼
Models
  │
  ▼
MongoDB
  │
  ▼
Ledger Transactions
  │
  ▼
Balance Calculation
```
````
