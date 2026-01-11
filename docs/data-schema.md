# Database Schema Specification

## Table: `users`

- `id`: UUID (Primary Key)
- `full_name`: String
- `document_id`: String (Unique - CPF/Tax ID)
- `email`: String (Unique)
- `password_hash`: String
- `created_at`: Timestamp
- `deleted_at`: Timestamp (Nullable)

## Table: `accounts`

- `id`: UUID (Primary Key)
- `user_id`: FK -> users.id
- `number`: String (Unique)
- `branch`: String (Default "0001")
- `type`: Enum (PERSONAL, BUSINESS)
- `status`: Enum (ACTIVE, BLOCKED, CLOSED)
- `created_at`: Timestamp

## Table: `transactions`

- `id`: UUID (Primary Key)
- `account_id`: FK -> accounts.id
- `type`: Enum (DEBIT, CREDIT)
- `category`: Enum (DEPOSIT, WITHDRAWAL, TRANSFER, PIX)
- `amount`: BigInt (Cents)
- `description`: String
- `reference_id`: UUID (Optional - for transfers)
- `created_at`: Timestamp
