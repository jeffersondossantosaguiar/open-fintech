# AI Development Instructions

1. Always use **Cents (Integers)** for money. Never use Float/Double.
2. Use **UUID v4** for all Primary Keys.
3. Every financial movement MUST create a record in the `transactions` table.
4. When creating a User, automatically trigger the Account creation within the same transaction.
5. All dates must be in **UTC**.
6. Use **Agência 0001** for all accounts.
