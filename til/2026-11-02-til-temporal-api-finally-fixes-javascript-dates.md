        # TIL: Temporal API finally fixes JavaScript dates
        > **Date:** 2026-11-02 | **Category:** TIL | Quick note

        Ran into this today and wanted to jot it down before I forget.


```js
// Lightweight event bus
const bus = new EventTarget();
const emit = (e, d) => bus.dispatchEvent(Object.assign(new Event(e), { detail: d }));
const on   = (e, fn) => bus.addEventListener(e, fn);
```


        ## Why It Matters
        Small things like this compound — knowing the right tool for the job
        saves hours over the course of a project.

        ## Try It Yourself
        ```bash
        # Quick test in a throw-away environment
        npx degit tanmayayay/starter-template test-project
        cd test-project && npm install && npm run dev
        ```

        ---
        *Part of my ongoing effort to document everything I learn, however small.*
