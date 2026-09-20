        # Docker Multi-Stage Build Patterns
        > **Date:** 2026-09-20 | **Category:** DevOps / Infrastructure | **Confidence:** ⭐⭐⭐

        ## Background
        Our deployment pipeline was causing ~8 min downtime windows.
        Researched options and implemented a proper strategy.

        ## Approach

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


        ## Pipeline Outline
        ```
        1. Build & test (GitHub Actions)
        2. Push image to ECR with immutable tag (git SHA)
        3. Update ECS task definition
        4. Blue-green swap at load balancer
        5. Health-check gate — rollback if P99 > threshold
        6. Drain old tasks
        ```

        ## Observability
        Every deploy emits a deployment marker to Grafana so we can
        correlate latency spikes with code changes.

        ## Key Learnings
        - Start simple (rolling update) before investing in blue-green
        - Feature flags decouple deploy from release — huge win
        - Bake rollback into the pipeline from the start

        ## Resources
        - [12 Factor App](https://12factor.net/)
        - [DORA Metrics](https://dora.dev/)
        - [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/)
