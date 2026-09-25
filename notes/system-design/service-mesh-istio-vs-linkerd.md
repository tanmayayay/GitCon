        # Service Mesh: Istio vs Linkerd
        > **Date:** 2026-09-25 | **Category:** System Design | **Confidence:** ⭐⭐⭐⭐⭐

        ## Overview
        Notes captured while researching scalability patterns for a high-throughput service.
        Keeping these here so I can reference them during design reviews.

        ## Key Concepts
        - **Throughput vs Latency**: optimizing for one often hurts the other — pick the right trade-off
        - **Horizontal scaling**: stateless services scale trivially; state is the hard part
        - **Backpressure**: producers must know when consumers are overwhelmed

        ## My Observations
        Working on a side-project that hits ~5k req/s peak traffic forced me to
        actually think through these patterns rather than just memorise them.
        The real insight: textbook definitions miss the *operational* complexity.

        ## Code Reference

```js
// Lightweight event bus
const bus = new EventTarget();
const emit = (e, d) => bus.dispatchEvent(Object.assign(new Event(e), { detail: d }));
const on   = (e, fn) => bus.addEventListener(e, fn);
```


        ## Resources
        - [Martin Fowler's Bliki](https://martinfowler.com/bliki/)
        - [High Scalability Blog](http://highscalability.com/)
        - [AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/)

        ## TODO
        - [ ] Prototype a minimal implementation
        - [ ] Benchmark against naive approach
        - [ ] Write a short blog post summarising findings
