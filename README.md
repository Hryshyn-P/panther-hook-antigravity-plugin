# Panther Hook for Google Antigravity

Officially documented Antigravity plugin layout with five agent skills and one remote MCP server. No local backend, HTTP proxy, API key or token is bundled.

## Install

With Antigravity CLI 1.3.5 or newer, run:

```sh
agy plugin install /absolute/path/to/panther-hook
agy plugin list --json
agy plugin validate /absolute/path/to/panther-hook
```

The directory must directly contain plugin.json and mcp_config.json. For a checked-out private backend repository, replace the path with the absolute path to integrations/google/antigravity-plugin. For standalone distribution, extract the exported ZIP and install its extracted root directory.

For an independently published standalone public repository (not the private backend repository):

```sh
agy plugin install https://github.com/OWNER/PUBLIC-PLUGIN-REPO
```

This GitHub URL is an example, not an existing release. Do not point public installs at a private backend repository.

Alternative manual placement: .agents/plugins/panther-hook inside a workspace, or ~/.gemini/config/plugins/panther-hook globally. Antigravity CLI supports /plugin install /absolute/path and /plugin list inside its interactive session.

## Authorize Panther Hook

1. Install and enable the plugin. Inspect its MCP server in Antigravity Settings > Customizations (or CLI /mcp).
2. Select the plugin MCP entry `panther-hook_api` and Authenticate. The first part is the plugin name; `api` is the short internal server name, chosen so every qualified tool name fits Antigravity CLI's 64-character limit. Sign in to Panther Hook, review OAuth scopes and select the intended Workspace.
3. Antigravity may ask you to copy the authorization code from https://antigravity.google/oauth-callback back into its UI. Treat the code as sensitive.
4. Verify access with native get_user_info and list_workspaces. Write operations require appropriate consent, role and plan. Protected operations additionally require first-party Human Approval.
5. If authentication fails, capture the sanitized error and stop; never attempt direct HTTP calls with scraped session tokens. No API key or client secret belongs in this package.

The server uses HTTPS remote Streamable HTTP through the existing Google API Gateway. Antigravity's published client identity is https://antigravity.google/oauth/client-metadata.json (CIMD); production dynamic client registration is disabled. Whether a given installed Antigravity build accepts this CIMD without DCR must be established by a real native OAuth attempt. The official Antigravity fallback for servers without DCR uses registered OAuth client credentials, with https://antigravity.google/oauth-callback as redirect. Never place user-specific client IDs, secrets or tokens in a public package.

## Skills and documentation

The five packaged skills cover getting started, form management, lead workflows, integrations and troubleshooting. For public product questions the agent should consult https://pantherhook.com/docs/ai/index.md and its linked static Markdown documents rather than request a connected account or call MCP. User data and writes require the OAuth-connected workspace.

Safety details: https://pantherhook.com/docs/ai/ai-security.md
OAuth / MCP reference: https://pantherhook.com/docs/ai/mcp.md
Support: https://pantherhook.com

The branded assets under assets/ are distribution artwork; current official plugin.json schema provides no icon property. Do not add an unsupported icon field to the manifest.

## Publish separately from the backend

Only the files in this plugin directory are permitted in the standalone distribution. From the private backend repository, run pnpm antigravity:check to reproduce the ZIP in integrations/google/build/. Review the ZIP file inventory and checksum before publishing to an independently approved public repository. No GitHub repository is created or made public by this build command.

Provider instructions: https://antigravity.google/docs/plugins, https://antigravity.google/docs/mcp, https://antigravity.google/docs/marketplace.
## CRM workflows (HubSpot, Pipedrive, Zoho CRM)

The existing shared MCP Gateway discovers generic CRM tools for HubSpot, Pipedrive and Zoho after a compatible server release. No provider-specific server or extra credentials belong in this plugin. A workspace Owner/Admin completes CRM OAuth through the browser. Use `list_crm_connections`, `get_crm_fields`, `list_crm_mappings`, and the generic integration/delivery tools; Zoho accepts `module: Leads | Contacts`. Creating destinations and disconnecting providers remain protected by Human Approval. Connection and provider availability depend on the installed server version and the workspace; do not claim live Zoho access until verified. For guidance, see the public /docs/zoho-guide page after its release.
