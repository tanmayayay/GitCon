        # Database Connection Pooling Best Practices
        > **Date:** 2026-11-02 | **Category:** Backend | **Confidence:** ⭐⭐⭐⭐⭐

        ## Why I'm Looking Into This
        Production incident last week exposed a gap in my understanding.
        Writing this up so the team has a reference.

        ## Core Idea

```python
from functools import wraps
import time

def rate_limit(calls, period):
    min_interval = period / calls
    last_call = [0.0]
    def decorator(fn):
        @wraps(fn)
        def wrapper(*args, **kwargs):
            elapsed = time.monotonic() - last_call[0]
            if elapsed < min_interval:
                time.sleep(min_interval - elapsed)
            last_call[0] = time.monotonic()
            return fn(*args, **kwargs)
        return wrapper
    return decorator
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


---
*Last updated: 2026-11-02T15:00:04.310561Z*
