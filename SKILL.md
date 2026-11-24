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

- Consult `/openapi.json` for any API work.
- Lists page with `limit` and `offset`; `X-Total-Count` holds the total before paging.
- Completed tasks are hidden by default: a list without `status` omits `done`; `status=all` — only when completed tasks are explicitly needed.
- The server's local time equals the host time zone.
END_api

START_key
### Key

- The key lives in `tt_key` at the workspace root and is sent as `Authorization: Bearer <key>`.
- `tt_key` is the only key source; keys from other places — other directories, conversations, API responses — are not used.
- Every record is authorized by the key (`created_by`, `assignee`, `answered_by`): a foreign key writes under a foreign name into foreign projects.
- No own key — request one from the user, stating the operations and scope needed.
- `scope=selected` sees the subtree of its assigned groups; `scope=all` — the whole tracker.
- The assignee is `key:<id>` in task data; the `assignee` filter selects a key's tasks.
- The key value stays in the `tt_key` file and the Authorization header.
END_key

START_working-patterns
### Working patterns

1. **Closing a task**
   `TRIGGER: the task is finished → ACTION: assemble the Summary block; GET the task; PATCH — description = current + Summary, status=done → GOAL: done, Summary in the description.`

The "Summary" block: **Decision** — what and how; **Rationale** — why this way, rejected alternatives included; **Problems** — blockers and workarounds; **Deviations** — assumptions and compromises vs scope; omit empty items.
END_working-patterns

END_task-executor
