---
name: panther-hook-getting-started
description: Connect Panther Hook to Google Antigravity, authorize a Workspace, and guide a user through creating and testing their first lead form.
---

Use for first-time Panther Hook setup, account connection, or explaining how to submit a first form.

1. For general setup explanations, use https://pantherhook.com/docs/ai/quickstart.md and https://pantherhook.com/docs/ai/forms.md. These are static public documents. Do not call MCP just to explain.
2. If the user wants account-specific setup, ask them to authenticate the Panther Hook MCP server in Antigravity using the existing scoped OAuth consent flow. Never ask for a password, token or API secret.
3. After connection, call get_user_info and list_workspaces to identify exactly which Workspace the OAuth grant authorizes. If an intended Workspace is not connected, ask for a separate authorized connection.
4. For a requested client/project/form creation, establish necessary names and parents, then use setup_lead_pipeline only when clients:write, projects:write and forms:write are authorized. Otherwise use authorized create_client, create_project, create_form operations. Reuse idempotency keys after timeouts. Never claim the whole pipeline is atomic.
5. Call get_form_setup for the created or selected form; use only the returned public endpoint. Explain safe test submission based on the public guide. Never fabricate keys or quotas.
6. Report the actual resources created, IDs returned, and next test step. Clearly distinguish completed operations from suggestions or failed attempts.
7. Scope, role, plan quotas and test-submission protections are enforced by Panther Hook; never work around them.

Security: https://pantherhook.com/docs/ai/ai-security.md
