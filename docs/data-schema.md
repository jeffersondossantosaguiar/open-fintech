# Database Schema Specification

## Table: `users`

- `id`: UUID (Primary Key)
- `full_name`: String
- `document_id`: String (Unique - CPF/Tax ID)
- `email`: String (Unique)
- `password_hash`: String (Argon2)
- `created_at`: Timestamp
- `deleted_at`: Timestamp (Nullable)

## Table: `accounts`

- `id`: UUID (Primary Key)
- `user_id`: FK -> users.id
- `balance`: BigInt (Cents - SnapShot)
- `number`: String (Unique)
- `branch`: String (Default "0001")
- `type`: Enum (PERSONAL, BUSINESS)
- `status`: Enum (ACTIVE, BLOCKED, CLOSED)
- `created_at`: Timestamp
- `closed_at`: Timestamp (Nullable)

Rules

- Accounts MUST NOT allow negative balances.
- Once CLOSED, an account becomes immutable.

## Table: `transactions`

- `id`: UUID (Primary Key)
- `account_id`: FK -> accounts.id
- `type`: Enum (DEBIT, CREDIT)
- `category`: Enum (DEPOSIT, WITHDRAWAL, TRANSFER, PIX)
- `amount`: BigInt (Cents - Always positive, sign determined by type)
- `idempotency_key`: String (Scoped uniqueness)
- `reference_id`: UUID (Optional - Used to link two sides of a transfer)
- `description`: String`
- `created_at`: Timestamp

Rules

- amount is always positive.
- The transaction sign is determined exclusively by type.
- Transactions are immutable and append-only.
