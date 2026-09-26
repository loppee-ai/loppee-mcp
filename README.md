# Loppee MCP

Public metadata for Loppee's narrow, no-auth MCP discovery surface.

## Connect

- MCP URL: `https://loppee.com/mcp/discovery`
- Transport: Streamable HTTP
- Authentication: none
- Registry identity: `com.loppee/loppee`
- Source repository: https://github.com/loppee-ai/loppee-mcp

Configure the URL above as a remote HTTP MCP server in a compatible client.
This repository does not contain credentials and does not require an API key.

### Claude custom connector

[Add Loppee to Claude](https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=Loppee&connectorUrl=https%3A%2F%2Floppee.com%2Fmcp%2Fdiscovery)
prefills Claude's custom-connector dialog. Claude still asks the signed-in user
to review and confirm the name and URL; the link does not publish a directory
listing or grant permissions.

The canary and directory-review packet is in
[`distribution/claude-connectors-directory.md`](distribution/claude-connectors-directory.md).

### Cursor

Copy the following official Cursor MCP install link into a browser with Cursor
installed. Cursor shows the decoded remote-server configuration and asks the
user to confirm before installation:

```text
cursor://anysphere.cursor-deeplink/mcp/install?name=loppee&config=eyJ1cmwiOiJodHRwczovL2xvcHBlZS5jb20vbWNwL2Rpc2NvdmVyeSJ9
```

The decoded configuration is exactly:

```json
{
  "url": "https://loppee.com/mcp/discovery"
}
```

For manual or project setup, use [`mcp.json`](mcp.json). The candidate Cursor
Marketplace manifest is [`.cursor-plugin/plugin.json`](.cursor-plugin/plugin.json).
Neither file contains an account, header, credential, key, or local command.
The Marketplace preflight is in
[`distribution/cursor-marketplace.md`](distribution/cursor-marketplace.md).

### OpenClaw

The metadata-only Agent Plugins Bundle source is in
[`clawhub/loppee-discovery`](clawhub/loppee-discovery). It contains no skill,
runtime code, credential, header, key, customer data, owner tool, write tool,
or location input.

The current ClawHub CLI incorrectly requires a native
`openclaw.plugin.json` from compatible bundles. Loppee will preserve the
narrower Agent Plugins Bundle instead of changing it into a native plugin or
publishing it as a Skill. The live admission blocker and reproduction are
tracked in [openclaw/clawhub#3513](https://github.com/openclaw/clawhub/issues/3513#issuecomment-5398799455).
See [`distribution/openclaw-clawhub.md`](distribution/openclaw-clawhub.md) for
the verified package boundary and publication gate.

## Public tool boundary

The endpoint exposes exactly five read-only named-business research tools:

| Tool | Purpose |
| --- | --- |
| `lookup_business` | Find pay-independent exact or genuine-prefix matches for a named business. |
| `get_trust_card` | Read the published Trust Card for an identified Loppee business. |
| `get_business_reviews` | Read paginated public reviews and their published disclosures. |
| `explain_recommendation` | Read the published recommendation basis for an identified business. |
| `compare_businesses` | Compare two to twenty identified published Loppee businesses. |

Every tool is declared read-only, non-destructive, and closed-world. This
surface exposes no category discovery, address or location input, pricing,
checkout, customer account, business-owner, write, or Back Office authority.

## Privacy and neutrality

- The tool schemas accept no address, city, state, ZIP, coordinates, location
  handoff, or device-location input.
- The endpoint returns no private customer or owner data.
- Payment does not change lookup, comparison, verification, reviews, evidence,
  or recommendation explanation on this surface.
- Missing or unresolved records must remain unresolved rather than fabricated.

Loppee Personal, authenticated consumer MCP, Loppee Business, and Back Office
are separate products with different authorization boundaries. They are not
published through this repository.

## Registry metadata

`server.json` prepares version `0.1.4` of the existing `com.loppee/loppee`
Official MCP Registry listing. It changes metadata only: the source
`repository` (`https://github.com/loppee-ai/loppee-mcp`, after the GitHub owner
rename from `4dwebspro-cell` to `loppee-ai`) and `agent_docs_url`. The remote,
tools and policies are unchanged. Until `0.1.4` is published, `0.1.3`
(published `2026-08-24T18:33:32.121626Z`, `/mcp/discovery` remote) remains the
active Registry version. Versions `0.1.0` through `0.1.2` are retained as
deprecated history. Registry versions are immutable after publication.

Official MCP Registry publication and GitHub MCP Registry curation are separate
gates. Loppee's GitHub Registry onboarding request was submitted on 2026-08-28;
submission is not inclusion. See
[`distribution/github-mcp-registry-onboarding.md`](distribution/github-mcp-registry-onboarding.md)
for the public request and the remaining verification gate.

## Verification

Before any future Registry release or downstream directory submission, Loppee
validates `server.json` with the official `mcp-publisher`; checks the live MCP
initialize capabilities, `tools/list`, `resources/list`, and `prompts/list`;
verifies the exact five-tool catalog and annotations with no resource or prompt
capability; and exercises the read-only tools. Those release checks run from
Loppee's private product repository and CI; no backend source, credentials,
workflows, or operational runbooks are published here.

The `0.1.3` production canary completed at `2026-08-24T18:36:20Z` on build
`e09c360f1d29269a72a1d9e272b1ead29c101c0e`: exactly five tools were listed,
resources, resource templates, and prompts were unsupported, all five tool
calls succeeded, the public-output privacy scan and text/structured-content
parity checks passed, and anonymous access to the separate `/mcp` surface
returned `401`.

## Links

- Website: https://loppee.com
- Agent information: https://loppee.com/agents
- Privacy: https://loppee.com/privacy
- Terms: https://loppee.com/terms
- Support: https://loppee.com/support

## Source and license

This public repository intentionally contains metadata and documentation only.
It does not contain the Loppee backend, private application source, scripts,
workflows, secrets, credentials, or customer data.

No `LICENSE` file is included. Public visibility does not grant an open-source
license.
