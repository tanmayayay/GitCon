        # TIL: HTTP/3 and QUIC improve mobile performance
        > **Date:** 2026-09-28 | **Category:** TIL | Quick note

        Ran into this today and wanted to jot it down before I forget.


```sql
-- Running total
SELECT date, amount,
       SUM(amount) OVER (ORDER BY date) AS running_total
FROM   transactions;
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
