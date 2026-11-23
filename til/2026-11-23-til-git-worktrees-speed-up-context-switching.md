        # TIL: Git worktrees speed up context-switching
        > **Date:** 2026-11-23 | **Category:** TIL | Quick note

        Ran into this today and wanted to jot it down before I forget.


```sql
-- Efficient pagination with keyset
SELECT id, created_at, title
FROM   posts
WHERE  created_at < :cursor
ORDER  BY created_at DESC
LIMIT  20;
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
