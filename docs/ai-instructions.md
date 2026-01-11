# AI Development Instructions

1. Always use **Cents (Integers)** for money. Never use Float/Double.
2. Use **UUID v4** for all Primary Keys.
3. Traceability (Ledger): Every financial movement MUST create a record in the transactions table. The balance in the accounts table acts as a high-performance snapshot but must be reconcilable with the ledger.
4. When creating a User, automatically trigger the Account creation within the same transaction.
5. All dates must be in **UTC** (ISO 8601).
6. Banking Standards:

- Branch (Agência): Fixed at 0001.
- Account Number: Must be generated with a Check Digit (Modulo 11). Format: XXXXX-D.
- Account numbers MUST be unique and MUST NOT be reused

7. Idempotency: All write operations (deposits, transfers) must require an x-idempotency-key in the header.

- Data Retention
- Records are never physically deleted.
- Soft deletes MUST be used where applicable.
- Financial transactions MUST NEVER be deleted (not even soft delete).
