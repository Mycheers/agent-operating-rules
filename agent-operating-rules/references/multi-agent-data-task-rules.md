# Multi-Agent Data Task Rules

## Fixed Roles

Use the same role names across all data/report/scheduled tasks:

| Function | Fixed agent name |
|---|---|
| Source discovery and validation | Scout / 数据侦察员 |
| Parsing and structuring | Extractor / 数据提取员 |
| Filtering, judgment, insight | Analyst / 数据分析员 |
| Report, summary, card copy | Editor / 内容主编 |
| Archive, provenance, read-back validation | Archivist / 知识库档案员 |
| Delivery, sending, message verification | Publisher / 发布投递员 |
| Orchestration, quality gates, final acceptance | Controller / 任务指挥官 |

## Default Chain

Controller → Scout → Extractor → Analyst → Editor → Archivist → Publisher → Controller

## Non-Negotiables

- Every source must have status: success, degraded, failed, or skipped.
- All required sources failed means stop; do not produce a fake report.
- Archive must be validated by read-back or equivalent verification.
- Delivery success requires message_id or equivalent evidence.
- Existing scheduled jobs must not have their business prompt overwritten when only schedule/delivery changes.

## Minimal Internal Schema

```json
{
  "task_name": "",
  "run_date": "",
  "source_status": [],
  "items": [],
  "insights": [],
  "archive": {"path": "", "validated": false},
  "delivery": {"channel": "", "status": "sent|skipped|failed", "message_id": "", "error": ""}
}
```
