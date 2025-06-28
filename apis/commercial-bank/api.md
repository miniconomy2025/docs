# Example
> **NOTE**: The following specification is not finalized and is currently only provided as an example structure for reference while writing your docs.

> **Scroll to the very bottom for the Swagger docs example**

---

## Commercial Bank API Specification

### Introduction

The Commercial Bank API facilitates financial transactions and loan management for companies within the cellphone supply chain simulation. It serves as the central hub for inter-company payments and provides essential lending services.


### Authentication
API Key authentication is envisioned for company identification and transaction security. Details to be specified.

### Endpoints

-----

### 1\. Loans to Companies

#### 1.1 Request a Loan

**Endpoint:** `POST /loans`

**Description:** Allows a company to request a loan from the Commercial Bank.

**Request Body:**

```json
{
  "companyId": "string",
  "loanAmount": "number",
  "currency": "string",
  "repaymentTermMonths": "integer"
}
```

**Response (201 Created):**

```json
{
  "loanId": "string",
  "companyId": "string",
  "loanAmount": "number",
  "currency": "string",
  "repaymentTermMonths": "integer",
  "interestRate": "number",
  "status": "string"
}
```

**Error Responses:**

  * `400 Bad Request`: Invalid input or missing parameters.
  * `403 Forbidden`: Company not authorized to request a loan.

#### 1.2 Get Loan Details

**Endpoint:** `GET /loans/{loanId}`

**Description:** Retrieves the details of a specific loan.

**Path Parameters:**

  * `loanId`: `string` (Unique identifier for the loan)

**Response (200 OK):**

```json
{
  "loanId": "string",
  "companyId": "string",
  "loanAmount": "number",
  "currency": "string",
  "repaymentTermMonths": "integer",
  "interestRate": "number",
  "currentBalance": "number",
  "status": "string",
  "repaymentSchedule": [
    {
      "dueDate": "string (YYYY-MM-DD)",
      "amountDue": "number",
      "status": "string"
    }
  ]
}
```

**Error Responses:**

  * `404 Not Found`: Loan with the specified ID not found.
  * `403 Forbidden`: Not authorized to view this loan's details.

#### 1.3 Make Loan Repayment

**Endpoint:** `POST /loans/{loanId}/repayments`

**Description:** Allows a company to make a repayment towards an existing loan.

**Path Parameters:**

  * `loanId`: `string` (Unique identifier for the loan)

**Request Body:**

```json
{
  "companyId": "string",
  "repaymentAmount": "number",
  "currency": "string"
}
```

**Response (200 OK):**

```json
{
  "loanId": "string",
  "companyId": "string",
  "repaymentAmount": "number",
  "currency": "string",
  "newBalance": "number",
  "status": "string"
}
```

**Error Responses:**

  * `400 Bad Request`: Invalid input or amount.
  * `403 Forbidden`: Not authorized to make repayment for this loan.
  * `404 Not Found`: Loan with the specified ID not found.

-----

### 2\. Payments between Companies

#### 2.1 Initiate Payment

**Endpoint:** `POST /payments`

**Description:** Facilitates a payment transfer from one company's account to another company's account.

**Request Body:**

```json
{
  "payerCompanyId": "string",
  "payeeCompanyId": "string",
  "amount": "number",
  "currency": "string",
  "description": "string"
}
```

**Response (201 Created):**

```json
{
  "transactionId": "string",
  "payerCompanyId": "string",
  "payeeCompanyId": "string",
  "amount": "number",
  "currency": "string",
  "description": "string",
  "timestamp": "string (ISO 8601)",
  "status": "string"
}
```

**Error Responses:**

  * `400 Bad Request`: Invalid input, insufficient funds, or missing parameters.
  * `403 Forbidden`: Payer company not authorized to initiate this payment.
  * `404 Not Found`: Payer or payee company not found.

#### 2.2 Get Transaction Details

**Endpoint:** `GET /transactions/{transactionId}`

**Description:** Retrieves the details of a specific payment transaction.

**Path Parameters:**

  * `transactionId`: `string` (Unique identifier for the transaction)

**Response (200 OK):**

```json
{
  "transactionId": "string",
  "payerCompanyId": "string",
  "payeeCompanyId": "string",
  "amount": "number",
  "currency": "string",
  "description": "string",
  "timestamp": "string (ISO 8601)",
  "status": "string"
}
```

**Error Responses:**

  * `404 Not Found`: Transaction with the specified ID not found.
  * `403 Forbidden`: Not authorized to view this transaction's details.

-----

### Data Models

#### Loan Object

| Field                | Type    | Description                                       |
| :------------------- | :------ | :------------------------------------------------ |
| `loanId`             | `string`| Unique identifier for the loan.                   |
| `companyId`          | `string`| ID of the company that took the loan.             |
| `loanAmount`         | `number`| The original amount of the loan.                  |
| `currency`           | `string`| Currency of the loan (e.g., "USD", "ZAR").        |
| `repaymentTermMonths`| `integer`| The original repayment term in months.            |
| `interestRate`       | `number`| Annual interest rate applied to the loan.         |
| `currentBalance`     | `number`| The current outstanding balance of the loan.      |
| `status`             | `string`| Current status of the loan (e.g., "Approved", "Active", "Paid", "Defaulted"). |
| `repaymentSchedule`  | `array` | An array of planned repayment installments.       |

#### Transaction Object

| Field             | Type    | Description                                       |
| :---------------- | :------ | :------------------------------------------------ |
| `transactionId`   | `string`| Unique identifier for the transaction.            |
| `payerCompanyId`  | `string`| ID of the company initiating the payment.         |
| `payeeCompanyId`  | `string`| ID of the company receiving the payment.          |
| `amount`          | `number`| The amount of money transferred.                  |
| `currency`        | `string`| Currency of the transaction.                      |
| `description`     | `string`| A brief description of the transaction purpose.   |
| `timestamp`       | `string`| Date and time of the transaction in ISO 8601 format. |
| `status`          | `string`| Status of the transaction (e.g., "Completed", "Pending", "Failed"). |

-----