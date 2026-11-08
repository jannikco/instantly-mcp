# Instantly MCP server

Inspect campaigns and explicitly create a new campaign with a reviewed schedule, without activating it.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `INSTANTLY_API_KEY`



Credential help: https://api.instantly.ai/openapi/api_v2.json

## Provider setup

Use your own Instantly v2 API key with campaign read/create permissions. Creation requires a valid schedule. This connector does not expose campaign activation, lead uploads, sender setup or bulk emailing.

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call instantly_list_campaigns '{"limit":10}'
```

## Use with an MCP client

Launch `node /absolute/path/instantly-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| instantly_list_campaigns | Read | Read one bounded page of campaigns. |
| instantly_create_campaign | Explicit approval required | Create campaign configuration with a required schedule; no activation or sending tool is exposed. |

## Concrete workflow

Inspect campaigns and explicitly create a new campaign with a reviewed schedule, without activating it.

1. instantly_list_campaigns
2. instantly_create_campaign

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=instantly&integration=instantly-mcp&utm_source=github&utm_campaign=github-instantly-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/instantly/).

## Provenance and maintenance

- https://api.instantly.ai/openapi/api_v2.json

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
