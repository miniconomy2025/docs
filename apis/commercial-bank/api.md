## Commercial Bank API Specification

### Resouces
- [Link to ERD](https://dbdiagram.io/d/Commercial-Bank-686026c4f413ba350852b4ee)

### Introduction
The Commercial Bank API facilitates financial transactions and loan management for companies within the cellphone supply chain simulation.
It serves as the central hub for inter-company payments and provides essential lending services.

### Authentication
All entities will be given their unique secret API key before the simulation starts, which allows us to prove their uniqueness as an account holder.

### High-level API specification
> (See bottom of page for Swagger docs)

- **Accounts**
  - ~~**POST** | Create account~~ (REMOVED in favour of pre-existing accounts)
    - ~~Returns API key for further access~~
  - **POST** | Set notification URL for received transactions
  - **GET** | Get account number for specific API key
  - **GET** | Check account balance
  - **GET** | Check account frozen status
  - **GET** | Check outstanding loans due
    - Total amount + total amount per-loan number

- **Transactions**
  - **GET** | Get bank statement between time X and time Y
    - Example: past 1 day
    - Can specify to only return successful transactions
  - **GET** | Get transaction information
    - Whether it was successful or not, amount transferred, etc.
  - **POST** | Create transaction (send money to account X in bank Y)
    - Returns success / failure + reason
    - Disallow transactions where `from == to`
    - Disallow transactions of amount <= 0
    - Notifies the receiving party that they've received money (via their notification URL)

- **Loans**
  - INFO:
    - No term; interest is continuously charged until the loan is fully paid off.
    - At the end of each 'day', aggregate a list of all the loans that have not been paid off and take interest for each.
    - Interest is calculated based on the outstanding amount due on the loan (initial loan - repayments).
    - Freeze account if balance is low and there is still outstanding loan interest due.
      - Account holders in this state can't make payments; they can only receive money.
      - Before any transaction, check whether the account is in a frozen state.
    - If interest payments default (insufficient money to pay the next interest due), the loan is written off.

  - **GET** | Get all loan details
    - Returns list of all loans + individual details
  - **GET** | Get specific loan details
    - Returns loan repayment + interest history for a specific loan number
  - **POST** | Take out loan of amount X
    - Creates new loan from the bank
    - Returns success + loan number / failure + reason
  - **POST** | Repay certain amount towards loan
    - Takes loan number + payment amount
    - Pays off the total due for the loan
    - If amount paid > amount due, only the minimum required to pay off the loan is taken