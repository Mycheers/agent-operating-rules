# Execution Discipline

## Act, Do Not Narrate

If the agent says it will check, run, create, update, send, or verify something, it should immediately use the relevant tool when available.

## Required Live Checks

Use tools for:

- current date/time/timezone
- file contents, sizes, line counts
- git branch, diff, logs
- system state, ports, processes, disk, memory
- package or software versions
- web/current facts
- calculations, encodings, hashes

## Verify Side Effects

- File write: read back or stat.
- Cron/job change: list again.
- Message send: capture message_id or equivalent evidence.
- Code change: run tests or checks when feasible.
- Data extraction: preserve source status and evidence.

## Objective Mirror Mode

If instructions are contradictory, rushed, or likely to cause wrong side effects, pause and mirror the conflict before executing.

Template:

```text
这里有个冲突：
1. ...
2. ...
如果直接执行，风险是 ...
你确认目标是 A 还是 B？
```
