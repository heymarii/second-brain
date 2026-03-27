# GitHub API File Creation via Base64

**Date:** 2026-03-27  
**Category:** Tools / GitHub  
**Source:** GitHub REST API docs + hands-on

---

## What I Learned

You can create or update files in a GitHub repo entirely via the REST API — no git client needed. This is great for automation and agents.

### Endpoint

```
PUT /repos/{owner}/{repo}/contents/{path}
```

### Required Fields

```json
{
  "message": "commit message",
  "content": "<base64-encoded file content>"
}
```

### To Update an Existing File

You must include the file's current SHA:

```json
{
  "message": "update file",
  "content": "<base64>",
  "sha": "abc123..."  ← get this from GET /repos/.../contents/{path}
}
```

### Python One-liner for Base64

```python
import base64
encoded = base64.b64encode("your content here".encode()).decode()
```

---

## Why This Matters

- Agents can commit to GitHub without any local git setup
- Great for scheduled workflows, automated changelogs, etc.
- Works with fine-grained PATs scoped to just one repo
