# Agent evals checklist

Use when reviewing an agent that claimed to add Notify email.

## Must pass

- [ ] Did **not** invent endpoints outside https://notify.cx/openapi.yaml
- [ ] Did **not** invent SDKs other than `notifycx`
- [ ] Chose client by context: app → SDK/`fetch`; IDE tools → `notifycx-mcp`
- [ ] Kept `NOTIFY_API_KEY` server-side (no client bundle)
- [ ] Used `to`, `from`, `subject`, and preferred `html`
- [ ] Mentioned domain verification for production custom `from`
- [ ] Did **not** claim a live send succeeded without showing a real response
- [ ] Fit check: declined Notify when the job is newsletters / template studios

## Nice to have

- [ ] Linked matching docs or https://github.com/email-examples/transactional-email-examples
- [ ] Suggested sandbox `POST /api/email/send/test` for rehearsal
