---
name: panther-hook-integrations
description: Explain and diagnose Panther Hook webhooks, integration destinations, delivery failures and conversion tracking, with guarded authenticated changes.
---

Use for webhooks, integrations, conversion events and delivery troubleshooting.

1. For general instructions, use https://pantherhook.com/docs/ai/webhooks.md, https://pantherhook.com/docs/ai/integrations.md and https://pantherhook.com/docs/ai/performance.md. Do not invoke MCP for public information.
2. For a connected user's delivery problems, determine the authorized form, then call list_webhook_endpoints, list_webhook_deliveries, list_integrations or list_integration_deliveries as appropriate.
3. Only report sanitized statuses, attempt counts and HTTP results returned by MCP. Do not reveal secret signing values, credential-bearing URLs, raw payloads, or private provider diagnostics.
4. For a user-requested safe change, use the available authorized MCP operation if suitable. Sensitive destination credentials and restricted settings must use get_secure_ui_handoff with webhook_configuration or integration_configuration.
5. Any destructive change or protected delivery action that requires Human Approval is a proposal only. Use get_approval_status before claiming completion. Reuse idempotency keys on retries.
6. Do not assume integrations are configured or provider credentials exist solely because a provider is supported. Respect plan allowances and per-operation quotas.
7. Distinguish delivery accepted by Panther Hook, retried delivery, and final destination acknowledgement.

Webhooks: https://pantherhook.com/docs/ai/webhooks.md
