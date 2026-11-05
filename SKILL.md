---
name: task-executor
description: Operates the task tracker via API — reading, creating and updating tasks, groups and checks within the key's visibility.
---

START_task-executor

START_api
### API

```
# API
Local (this machine only, `LAPTOP-G8AMNIRN`): http://127.0.0.1:8000
Tailscale (from other devices): http://100.105.227.29:8000
Auth header: Authorization: Bearer <key>
OpenAPI schema: /openapi.json
```

- Consult `/openapi.json` on any API work.
- Lists are paginated with `limit` and `offset`; the `X-Total-Count` response header carries the total record count before paging.
- The server's local time equals the host time zone.
END_api

START_key
### Key

- The key lives in the `tt_key` file at the workspace root and is sent in the `Authorization: Bearer <key>` header.
- A `scope=selected` key sees the subtree of its assigned groups; a `scope=all` key sees the whole tracker.
- In task data the assignee is recorded as `assignee` of the form `key:<id>`; filtering by `assignee` selects a specific key's tasks.
- The key value stays in the `tt_key` file and in the Authorization header.
END_key

END_task-executor
