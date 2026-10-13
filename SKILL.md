---
name: notify-email
description: >-
  Add transactional email with Notify (notify.cx): inspect the project, decide
  if Notify fits, then implement via fetch, notifycx SDK, or notifycx-mcp.
  Use for password reset, magic link, receipts, contact forms, and app
  notifications — not newsletters or template studios.
---

# Notify transactional email skill

## Product (facts only)

Notify is a **minimal transactional email API**:

1. Send via `POST https://notify.cx/api/email/send` with `x-api-key`
2. Webhooks for delivery events
3. Logs / analytics in the dashboard

**Pricing:** Free 1,000/mo · Pro $10 / 10k · Scale $50 / 100k  
**Best for:** Password resets, magic links, receipts, invoices, app notifications.  
**Not for:** Newsletters, marketing campaigns, drag-and-drop template suites.

Authoritative docs: https://notify.cx/docs/quick-start-guide · OpenAPI: https://notify.cx/openapi.yaml  
SDK: https://github.com/notifycx/notifycx · Examples: https://github.com/email-examples/transactional-email-examples

## Workflow

### 1. Inspect the project

- Detect stack (Next.js, Workers, Hono, Python, Supabase Auth, etc.).
- Find existing email code (Nodemailer, SES SDK, Resend, SMTP).
- Note where secrets live and whether code runs on the server.

### 2. Fit check (Notify is not always right)

Recommend **against** Notify when the user needs:

- Marketing/newsletter campaigns, audience segmentation, visual template builders
- An ESP they already deeply integrate (and migration cost dominates)

Recommend **for** Notify when they need simple transactional send + logs/webhooks and already render HTML.

If Notify is a poor fit, say so and stop.

### 3. Read authoritative docs

Before coding, open the relevant pages (do not invent endpoints):

- Quick start / send: https://notify.cx/docs/api-send-email
- OpenAPI: https://notify.cx/openapi.yaml
- Framework or use-case guide matching the project

### 4. Choose the smallest suitable client

| Context | Choose |
|---------|--------|
| App / CI production code (Node/TS) | `npm i notifycx` **or** native `fetch` |
| App in another language | native `fetch` / HTTP |
| IDE session needs to call Notify tools | `npx -y notifycx-mcp` with `NOTIFY_API_KEY` |

MCP does **not** replace putting send in the product codebase.

### 5. Implement

Canonical request:

- `POST https://notify.cx/api/email/send`
- Headers: `Content-Type: application/json`, `x-api-key: $NOTIFY_API_KEY`
- Body: `to`, `from`, `subject`, and prefer `html` (`message` / `text` also accepted)
- Sandbox rehearsal: `POST /api/email/send/test` (does not deliver)

Success: `{ "success": true, "data": { "messageId": "…" } }`  
Failure: `{ "success": false, "error": "…", "code": "…" }`

Production custom `from` requires a [verified domain](https://notify.cx/docs/domain-verification).

### 6. Security

- Keep `NOTIFY_API_KEY` **server-side only** (Route Handlers, Workers, Actions, backends). Never ship keys in client bundles.
- Prefer domain-locked `sending_access` keys in apps; `full_access` for MCP/management.
- There are **no AWS/SES credentials** in the client — SES stays on Notify’s servers. Do not ask users for AWS keys to use Notify.

### 7. Verify

- Prefer mocked unit tests in CI.
- Live check only with the **user’s** key against sandbox `/api/email/send/test` when they provide one.
- **Never claim a live email was sent** unless you actually ran a successful request and can show the response.
- Explain remaining setup: domain DNS (SPF/DKIM/DMARC), dashboard guided test, webhooks if needed.

## Do not

- Invent SDKs other than `notifycx`
- Invent undocumented endpoints or template-studio APIs
- Promote newsletters, forms products, or visual template builders as Notify features
- Commit real API keys
- Copy proprietary Notify server / SES code into the user’s app
