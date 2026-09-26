# GitHub MCP Registry onboarding packet

Status: onboarding request submitted to GitHub's public registry discussion on
2026-08-28. GitHub has not yet curated or published a Loppee registry entry.

Public request:
https://github.com/github/github-mcp-server/discussions/1257#discussioncomment-18194044

GitHub's registry at `github.com/mcp` is a curated downstream catalog, separate
from the Official MCP Registry at `registry.modelcontextprotocol.io`. Publishing
an Official MCP Registry version does not automatically onboard a new GitHub
entry. GitHub can sync later versions only after its initial manual curation.

## Gate status

The Official MCP Registry prerequisite is complete: it reports
`com.loppee/loppee` version `0.1.3` as the only active version, published at
`2026-08-24T18:33:32.121626Z`, with this remote:

```text
https://loppee.com/mcp/discovery
```

GitHub currently returns no Loppee entry. The separate live resource-boundary
gate has passed on production build
`f7fabd81ddde681479a2ff1ac2d3c5e3bf72953c`: `/mcp/discovery` advertises exactly
five tools and no resources or prompts; all five calls succeeded; and the
privacy and text/structured-content parity checks passed.

The onboarding request was posted to GitHub Discussion
`github/github-mcp-server#1257`, the active public venue where GitHub staff
clarified the manual-onboarding model and maintainers continued posting requests
through August 2026. The request includes the Official Registry identity,
endpoint, public metadata repository, exact five-tool boundary, annotations,
and a fresh production verification against build
`de1a33de635601e3b7851ebb622201d381c0ecd9`.

## Evidence checklist

- Official registry name: `com.loppee/loppee`.
- Active/latest version: `0.1.3`.
- Hosted Streamable HTTP endpoint:
  `https://loppee.com/mcp/discovery`.
- Public metadata repository:
  `https://github.com/loppee-ai/loppee-mcp`.
- Manifest:
  `https://github.com/loppee-ai/loppee-mcp/blob/main/server.json`.
- Website: `https://loppee.com/agents`.
- Privacy: `https://loppee.com/privacy`.
- Terms: `https://loppee.com/terms`.
- Support: `https://loppee.com/support`.
- Authentication: none.
- Tool boundary: exactly five public, read-only named-business research tools.
- Resource/prompt boundary: none.
- Output boundary: no caller-location contract, signed media token, internal
  action array, or account/owner/admin authority.
- Input boundary: no user address, city, state, ZIP, coordinates, location
  handoff, account, owner/admin authority, credential, or key.
- Official Registry verification command:

```bash
curl "https://registry.modelcontextprotocol.io/v0.1/servers?search=com.loppee%2Floppee"
```

- GitHub Registry verification command:

```bash
curl "https://api.mcp.github.com/v0.1/servers?search=com.loppee%2Floppee"
```

## Submitted request

Title:

```text
Onboarding request: com.loppee/loppee for github.com/mcp
```

Body:

```markdown
## Request

Please consider `com.loppee/loppee` for initial manual curation in the GitHub
MCP Registry at `github.com/mcp`.

## Server details

- Official MCP Registry name: `com.loppee/loppee`
- Active/latest version: `0.1.3`
- Official Registry API result: https://registry.modelcontextprotocol.io/v0.1/servers?search=com.loppee%2Floppee
- Public metadata repository: https://github.com/loppee-ai/loppee-mcp
- Manifest: https://github.com/loppee-ai/loppee-mcp/blob/main/server.json
- Website: https://loppee.com/agents
- Hosted endpoint: https://loppee.com/mcp/discovery
- Transport: Streamable HTTP
- Authentication: none

Loppee exposes exactly five public, read-only tools for named-business research:
`lookup_business`, `get_trust_card`, `get_business_reviews`,
`explain_recommendation`, and `compare_businesses`. It exposes no resource,
prompt, account, owner, Back Office, write, checkout, credential, key, or user
location/address input surface.

Production build `f7fabd81ddde681479a2ff1ac2d3c5e3bf72953c` was verified at
`2026-08-24T18:36:20Z`. The live MCP initialize response reported version
`0.1.3`; it listed exactly the five tools above, exposed no resources, resource
templates, or prompts, and successfully executed all five tools. The output
privacy scan and text/structured-content parity checks passed, while anonymous
access to the separate `/mcp` surface returned `401`.

The Official MCP Registry manifest passed `mcp-publisher validate` before
publication and version `0.1.3` is the only active version.

Please let us know if the curation team needs any additional metadata or
validation evidence.
```

## External gate

GitHub documents the catalog as curated but does not publish objective
acceptance criteria. The request is submitted, but submission is not inclusion.
Do not imply inclusion until the GitHub Registry API and `github.com/mcp`
listing both show Loppee.

Current official references:

- https://docs.github.com/en/copilot/how-tos/provide-context/use-mcp-in-your-ide/extend-copilot-chat-with-mcp
- https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
- https://github.com/github/github-mcp-server/discussions/1257
