# Feishu / Lark Card Delivery Rules

Use for recurring reports, digests, radars, business summaries, and other card-like outputs.

## Principle

Send a real interactive card. Do not paste card JSON as text and call it done.

## Hermes-Style Stable Pattern

Use local cron delivery and self-send inside the task:

```text
cron deliver=local
```

Then send through Lark CLI or an equivalent API path:

```bash
export PATH="$HOME/.local/node/bin:$PATH"
export LARK_CLI_NO_PROXY=1
lark-cli im +messages-send --as bot --chat-id <CHAT_ID> --msg-type interactive --content '<CARD_JSON>'
```

## Evidence

Publisher must capture:

- message_id, or
- HTTP request ID / response body proving delivery

No evidence means no success claim.

## Failure Split

Separate these layers:

1. Trigger: did the scheduled job start?
2. Execution: did it collect/analyze/render the report?
3. Delivery: did the card reach the target chat?
4. Business output: was the received message the expected card/report rather than a meta notification?

Do not blame chat permissions if a notification arrives but the expected card does not. Inspect job content first.
