# Data-Science-Projects

Projects from A Collection of Data Science Take-Home Challenge by Guilio Palombo

1. Conversion Rate
2. A/B Testing - Spanish Translation
3. Employee Retention
4. Fraud
5. Funnel Analysis
6. Pricing Test


**# Banking API

## Overview

The **Banking API** is a simple financial institution backend API that allows bank employees to manage customer accounts, perform fund transfers, and retrieve balances and transaction histories. The project uses **FastAPI** for the API layer, **SQLAlchemy** for database interactions, and **pytest** for testing.

---

## Table of Contents

- [Project Setup](#project-setup)
- [Project Structure](#project-structure)
- [API Usage](#api-usage)
  - [Root Endpoint](#root-endpoint)
  - [Accounts Endpoints](#accounts-endpoints)
  - [Transfer Endpoints](#transfer-endpoints)
  - [Customer Endpoints](#customer-endpoints)
- [Testing](#testing)
  - [Unit Tests](#unit-tests)
  - [Integration Tests](#integration-tests)
- [Run the Application](#run-the-application)

---

## Project Setup<a id='project-setup'></a>

### 1. Clone the Repository
```bash
git clone https://your-repository-url.git
cd banking-api
```

### 2. Create a Virtual Environment
```bash
python -m venv venv
source venv/bin/activate
```
### 3. Install Required Dependencies
```bash
pip install -r requirements.txt
```
Alternatively, you can manually install the required packages:
```bash
pip install fastapi uvicorn sqlalchemy pydantic pytest
```

## Project Structure<a id='project-structure'></a>
Project Structure
The project follows a simple folder structure.
```
banking-api/
├── app/
│   ├── main.py                      # FastAPI app definition and routes
│   ├── model.py                     # Database models (Customer, Account, Transfer)
│   ├── service.py                   # Business logic (account creation, transfers)
│   ├── db.py                        # Database connection and session handling
│   └── data.py                      # Test data and sample customer records
├── tests/
│   ├── integration/                 # Integration tests
│   │   ├── conftest.py              # Test setup and fixtures
│   │   ├── test_root.py             # Test root endpoint
│   │   ├── test_accounts.py         # Test account-related APIs
│   │   ├── test_transfer.py         # Test transfer-related APIs
│   │   ├── test_customer_summary.py # Test customer summary endpoint
│   └── unit/                        # Unit tests for business logic
│       └── test_service_logic.py    # Unit tests for service logic
├── requirements.txt                 # Project dependencies
├── Summary.txt                      # Project documentation
└── README.md                        # Project Guidlines
```

## API Usage<a id='api-usage'></a>
### Root Endpoint<a id='root-endpoint'></a>
**URL**: `/`

The root endpoint simply returns a message indicating that the API is live.
- **GET** `/`
    - **Response** `{"message": "Hello! Entrix Banking API is live!"}` 

### Accounts Endpoint<a id='accounts-endpoints'></a>
**URL**: `/accounts/`

This endpoint allows creating new bank accounts and retrieving information about existing accounts.
#### Create Account
- **POST** `/accounts/`
    - **Request**:
    ```json
    {
    "customer_id": 1,
    "initial_deposit": 500
    }
    ```
    - **Response**:
    ```json
    {
    "account_id": 1,
    "customer_id": 1,
    "balance": 500
    }
    ```
#### Get Account Balance
- **GET** `/accounts/{account_id}`
    - **Response**:
    ```json
    {
    "account_id": 1,
    "balance": 500
    }
    ```
#### Get Transfer History for Account
- **GET** `/accounts/{account_id}/transfers`
    - **Response**:
    ```json
    [
        {
            "transfer_id": 1,
            "from_account": 1,
            "to_account": 2,
            "amount": 100,
            "timestamp": "2025-03-24T16:07:41.427135"
        }
    ]
    ```

### Transfer Endpoint<a id='transfer-endpoints'></a>
**URL**: `/transfer/`

This endpoint allows transferring funds from one account to another.
#### Transfer Fund
- **POST** `/transfer/`
    - **Request**:
    ```json
    {
    "from_account_id": 1,
    "to_account_id": 2,
    "amount": 100
    }
    ```
    - **Response**:
    ```json
    {
    "transfer_id": 1,
    "from_account": 1,
    "to_account": 2,
    "amount": 100,
    "timestamp": "2025-03-24T16:07:41.427135"
    }
    ```

### Customers Endpoint<a id='customer-endpoints'></a>
URL: `/customers/`

This endpoint allows you to retrieve customer information and associated accounts.
#### Get Customer Accounts
- **GET** `/customers/{customer_id}/accounts`
    - **Request**:
    ```json
    {
    "customer_id": 1,
    }
    ```
    - **Response**:
    ```json
    {
        "customer_id": 1,
        "customer_name": "Arisha Barron",
        "accounts": [
            {
            "account_id": 1,
            "balance": 400
            }
        ]
    }
    ```
#### Get Customer Account Summary
- **GET** `/customers/summary`
    - **Response**:
    ```json
    [
        {
            "customer_id": 1,
            "customer_name": "Arisha Barron",
            "account_count": 1,
            "total_balance": 400
        },
        {
            "customer_id": 2,
            "customer_name": "Branden Gibson",
            "account_count": 1,
            "total_balance": 200
        },
        {
            "customer_id": 3,
            "customer_name": "Rhonda Church",
            "account_count": 0,
            "total_balance": 0
        },
        {
            "customer_id": 4,
            "customer_name": "Georgina Hazel",
            "account_count": 0,
            "total_balance": 0
        }
    ]
    ```


## Testing<a id='testing'></a>

### Unit Tests<a id='unit-tests'></a>
Unit tests are located in the tests/unit folder. These tests cover the business logic in isolation.

To run the unit tests, use:
```bash
pytest tests/unit
```

### Integration Tests<a id='integration-tests'></a>
Integration tests are located in the tests/integration folder. These tests ensure that the FastAPI application interacts correctly with the database and the overall application flow (e.g., creating accounts, performing transfers via the API).

To run the integration tests, use:

```bash
pytest tests/integration
```

## Run the Application<a id='run-the-application'></a>
1. Run the FastAPI app with Uvicorn:
```bash
uvicorn app.main:app --reload
```
This will start the development server. You can now visit your API at `http://127.0.0.1:8000`.
2. API Docs: FastAPI automatically generates interactive documentation for your API. Visit the following URL to access it:
`http://127.0.0.1:8000/docs`
3. Swagger UI: You can test the API directly from the Swagger UI provided by FastAPI.



Run it:
uvicorn app.main:app --reload
Open in browser: http://127.0.0.1:8000

http://127.0.0.1:8000/docs
pytest -s tests/test_account.py**
