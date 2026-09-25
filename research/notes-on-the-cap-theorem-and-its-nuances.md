# Notes on the CAP Theorem and Its Nuances
> **Date:** 2026-09-25 | **Category:** Research / Reading | **Confidence:** ⭐⭐

## Why I Read This
Recommended by a senior engineer during a design review.
Wanted to fill gaps in my distributed systems mental model.

## Core Thesis
The paper argues that the hardest problems in distributed systems
aren't algorithmic — they're about managing *partial failure* and
*asynchrony* gracefully.

## Key Takeaways
1. **Failure is the norm, not the exception** — design for it from day one
2. **Consensus is expensive** — avoid it on the critical path
3. **Monotonic IDs** prevent split-brain ambiguity better than wall-clock time

## Memorable Quote
> "A distributed system is one in which the failure of a computer you
> didn't even know existed can render your own computer unusable."
> — Leslie Lamport

## How This Changes My Work
- Will audit our service-to-service calls for missing timeouts
- Going to add jitter to all retry logic to avoid thundering herds
- Revisiting our DB failover runbook with these principles in mind

## Related Reading
- Designing Data-Intensive Applications — Kleppmann
- The Morning Paper (blog)
- ACM Queue
