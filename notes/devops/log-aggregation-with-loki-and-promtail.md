        # Log Aggregation with Loki and Promtail
        > **Date:** 2026-09-20 | **Category:** DevOps / Infrastructure | **Confidence:** ⭐⭐

        ## Background
        Our deployment pipeline was causing ~8 min downtime windows.
        Researched options and implemented a proper strategy.

        ## Approach

```sql
-- Efficient pagination with keyset
SELECT id, created_at, title
FROM   posts
WHERE  created_at < :cursor
ORDER  BY created_at DESC
LIMIT  20;
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
