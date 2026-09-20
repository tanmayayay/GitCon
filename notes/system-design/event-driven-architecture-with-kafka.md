        # Event-Driven Architecture with Kafka
        > **Date:** 2026-09-20 | **Category:** System Design | **Confidence:** ⭐⭐⭐⭐⭐

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
const retry = async (fn, retries = 3, delay = 500) => {
  try { return await fn(); }
  catch (err) {
    if (retries === 0) throw err;
    await new Promise(r => setTimeout(r, delay));
    return retry(fn, retries - 1, delay * 2);
  }
};
```


        ## Resources
        - [Martin Fowler's Bliki](https://martinfowler.com/bliki/)
        - [High Scalability Blog](http://highscalability.com/)
        - [AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/)

        ## TODO
        - [ ] Prototype a minimal implementation
        - [ ] Benchmark against naive approach
        - [ ] Write a short blog post summarising findings
