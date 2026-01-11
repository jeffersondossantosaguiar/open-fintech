# Project Overview: Fintech Core API

## Vision

A high-integrity banking API focused on traceability, security, and financial accuracy. Designed to simulate real-world digital banking operations.

## Core Business Rules

- **Monetary Values:** All currency values MUST be handled as **INTEGERS** representing the smallest unit (cents).
  - Example: $10.50 is stored as `1050`.
  - Never use floats or doubles.
- **Banking Structure:** - Branch (Agência) is fixed at `0001`.
  - Account numbers must be generated with a **Check Digit** (Modulo 11 algorithm).
- **Ledger-Based Accounting:** - The "Balance" is not a static field. It is the sum of all transaction records (Debits and Credits).
  - This ensures a complete audit trail.
- **Idempotency:** All write operations (deposits, withdrawals) must support an `x-idempotency-key` header to prevent duplicate processing.
- **Soft Deletes:** Records are never physically deleted. Use `deleted_at` timestamps for audit purposes.
