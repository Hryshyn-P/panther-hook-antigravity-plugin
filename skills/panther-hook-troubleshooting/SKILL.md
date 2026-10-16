---
name: panther-hook-troubleshooting
description: Diagnose form capture, authorization, webhook and integration problems without unnecessary tool calls or changes to user resources.
---

Use when Panther Hook is not capturing forms, an MCP connection fails, a delivery is rejected, or the user is debugging permissions.

1. Start with https://pantherhook.com/docs/ai/troubleshooting.md and https://pantherhook.com/docs/ai/mcp.md. If the question is generic, answer from documentation only.
2. Ask for the smallest useful non-secret details if a specific live diagnosis is needed, such as form identifier, sanitized HTTP status or expected behavior. Do not request passwords or access tokens.
3. For connected Workspace-specific diagnosis, verify identity and scope with get_user_info/list_workspaces; query only suitable read-only tools such as get_workspace_health, list_webhook_deliveries or list_integration_deliveries if available and permitted.
4. Distinguish missing OAuth scope, incorrect Workspace, insufficient role, plan quota and transient failures. Do not promise entitlement or privileges missing from real results.
5. For corrective writes, explain the proposed change and call an authenticated tool only when the user actually requests that operation. For protected settings use get_secure_ui_handoff.
6. Never turn an error into permission to bypass rate limits, anti-abuse gates or owner approval; check get_approval_status for proposed lifecycle changes.
7. Conclude with observed evidence, unverified hypotheses and the next safe diagnostic action.

Security: https://pantherhook.com/docs/ai/ai-security.md
