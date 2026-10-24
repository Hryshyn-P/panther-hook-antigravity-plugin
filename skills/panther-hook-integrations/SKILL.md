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

## CRM management: HubSpot, Pipedrive and Zoho

Panther Hook supports provider-keyed CRM destinations through a **single shared MCP Gateway**, not separate provider connectors. Use `list_crm_connections`, `get_crm_connection` and `get_crm_fields` to inspect workspace-scoped connection status and discover available properties. Use `list_crm_mappings`, `list_integrations` and `list_integration_deliveries` to inspect each form's destination configuration, mapping and delivery status. Do not infer that any provider is connected or enabled from its listing.

Provider values are `HUBSPOT`, `PIPEDRIVE` and `ZOHO`. Zoho supports **Leads or Contacts**; its `get_crm_fields` request optionally accepts `module: "Leads" | "Contacts"` and its destinations have `config: {module, mapping}`. HubSpot supports Contacts; Pipedrive supports Persons. Only map fields advertised as writable by the connected provider. Email is required for matching, and Zoho's required properties vary by module and layout.

To connect a provider, call `start_crm_oauth` with the authorized form and provider, then direct the human to the returned first-party browser authorization URL; never request authorization codes or tokens through chat. Never declare OAuth connected until `get_crm_connection` confirms it. For creation, use `create_crm_integration` with explicit provider, optional Zoho module and mappings; this is a **Human Approval proposal**. Likewise use guarded existing destination-configuration and `disconnect_crm` operations, and confirm execution via `get_approval_status`. Do not bypass user review, workspace isolation, scopes or plan limits.

After a synthetic approved production-mode submission, use integration delivery history **and the CRM-side record** to verify upsert. A successful connection test or HTTP status alone is not proof of delivery. Temporary provider failures may retry; inspect final status. Never create or modify real customer CRM records solely to test an integration.

Zoho guide: https://pantherhook.com/docs/zoho-guide (only claim publicly available after deployment).
