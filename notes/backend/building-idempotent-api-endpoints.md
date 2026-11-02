        # Building Idempotent API Endpoints
        > **Date:** 2026-11-02 | **Category:** Backend | **Confidence:** ⭐⭐⭐

        ## Why I'm Looking Into This
        Production incident last week exposed a gap in my understanding.
        Writing this up so the team has a reference.

        ## Core Idea

```sql
-- Running total
SELECT date, amount,
       SUM(amount) OVER (ORDER BY date) AS running_total
FROM   transactions;
```


        ## Implementation Notes
        - Always handle the unhappy path first — error cases are where bugs live
        - Write integration tests against a real DB/Redis, not just unit mocks
        - Instrument with structured logging from day one (JSON logs + correlation IDs)

        ## Performance Considerations
        - P99 latency matters more than mean for user-facing endpoints
        - N+1 queries are silent killers — use query logging in dev
        - Connection pool exhaustion looks like a slow app, not a DB problem

        ## Security Checklist
        - [ ] Input validation at the boundary (zod / joi / pydantic)
        - [ ] Rate limiting per user + per IP
        - [ ] Audit log for sensitive mutations
        - [ ] Secrets never in source — use env vars / Vault

        ## Links
        - [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)
        - [PostgreSQL Docs](https://www.postgresql.org/docs/)
