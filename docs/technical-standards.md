# Technical Standards (Functional & Layered)

## 1. Architectural Paradigm

- **Paradigm:** Functional Programming (FP). Avoid Classes, `this`, and `new`.
- **Pattern:** Layered Hexagonal (Domain / Infra).
- **Structure:**
  - **Domain (Pure):** Types and pure functions only. No side effects.
  - **Infra (Impure):** Implementation of side effects (Prisma, Elysia, BCrypt).
- **Dependency Injection:** Use Higher-Order Functions (HOF) or argument injection to pass repositories into use cases.

## 2. Domain Logic & Entities

- **Data Models:** Define data structures using TypeScript `type` or `interface`.
- **Immutability:** Never mutate data. Use the spread operator (`...`) to return new objects.
- **Business Rules:** Must be isolated in the `domain/use-cases` as pure functions.

## 3. Financial Integrity (The Ledger)

- **Monetary Values:** Use `BigInt` to represent cents.
- **Balance Calculation:** Balance is a derived state. Use a function to sum `transactions` .
- **Transactions (ACID):** Operations involving multiple records (e.g., `User` + `Account`) MUST use Prisma's `$transaction`.

## 4. Security & Authentication

- **Hashing:** Use `Bun.password.hash()` (Argon2) for user passwords.
- **Auth:** Stateless JWT (JSON Web Tokens) for route protection.
- **Validation:** Use **TypeBox** (native to Elysia) for schema validation at the HTTP layer.

## 5. API Response Standard

- **Success:** Return relevant data objects with HTTP 200/201.
- **Errors:** All errors must follow this structure:

```json
{
  "error": "Readable error message",
  "code": "SPECIFIC_ERROR_CODE",
  "details": {}
}
```
