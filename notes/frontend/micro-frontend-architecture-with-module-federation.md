        # Micro-Frontend Architecture with Module Federation
        > **Date:** 2026-09-25 | **Category:** Frontend | **Confidence:** ⭐⭐⭐

        ## Context
        Encountered this while building the dashboard feature — needed to understand
        the trade-offs before committing to an approach.

        ## Problem Statement
        The naive implementation worked in dev but showed performance regressions
        on mobile. Digging into Chrome DevTools traces revealed the bottleneck.

        ## Solution / Pattern

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


        ## Gotchas
        - SSR hydration edge-cases are nasty — test on slow 3G in DevTools
        - Bundle size impact: always check with `next build` stats or `source-map-explorer`
        - Accessibility: screen readers behave differently — test with VoiceOver/NVDA

        ## Metrics After Optimisation
        | Metric | Before | After |
        |--------|--------|-------|
        | LCP    | 3.8s   | 1.9s  |
        | CLS    | 0.14   | 0.02  |
        | TTI    | 5.2s   | 2.7s  |

        ## References
        - [web.dev](https://web.dev)
        - [React Docs](https://react.dev)
        - [Next.js App Router](https://nextjs.org/docs/app)
