# OpenClaw and ClawHub Bundle packet

Status: source-ready, runtime-verified, and not yet published in ClawHub. The
current ClawHub admission bug blocks compatible bundles before upload.

## Package boundary

The package at `clawhub/loppee-discovery` is an Agent Plugins 1.0.0 Bundle,
not a Skill and not a native OpenClaw plugin. It contains only:

```text
README.md
plugin.json
mcp.json
```

The package has no executable module, hook, command, skill, credential,
customer data, account authority, owner tool, write tool, address/location
input, or Back Office surface. Its only external connection is the canonical
public Streamable HTTP endpoint:

```text
https://loppee.com/mcp/discovery
```

The endpoint, not non-standard bundle metadata, enforces the exact five-tool
allow-list.

## Runtime verification

The Agent Plugins documents validate against the official 1.0.0 schemas. An
isolated OpenClaw `2026.8.1-beta.3` install recognizes the package as:

```text
format: bundle
bundleFormat: agent
bundleCapabilities: mcpServers
status: loaded
```

The production endpoint independently passed the `0.1.3` five-tool,
no-resource/no-prompt, output-privacy, text/structured-content parity, and
private-surface `401` canaries on build
`e09c360f1d29269a72a1d9e272b1ead29c101c0e`.

## ClawHub blocker

ClawHub CLI `0.23.3` recognizes `bundle-plugin` as a package family but still
requires `openclaw.plugin.json`, which is the native-plugin manifest. Both
autodetection and an explicit non-uploading Agent Bundle dry run fail before an
API request. The same requirement exists in the server admission path.

The canonical report and Loppee reproduction are in
[openclaw/clawhub#3513](https://github.com/openclaw/clawhub/issues/3513#issuecomment-5398799455).
Adding a native manifest would change OpenClaw's detection precedence and widen
the package type. Publishing a Skill would also misrepresent the product and
would require a separate license decision. Neither workaround is used.

## Publish after the blocker is fixed

Run the official dry run first from this repository root:

```bash
clawhub package publish clawhub/loppee-discovery \
  --family bundle-plugin \
  --name loppee-discovery \
  --display-name "Loppee Discovery" \
  --version 0.1.0 \
  --bundle-format agent \
  --host-targets openclaw \
  --source-repo loppee-ai/loppee-mcp \
  --source-ref main \
  --source-path clawhub/loppee-discovery \
  --dry-run --json
```

Only after the dry run resolves the same three-file Agent Bundle should the
identical command be repeated without `--dry-run`, followed by ClawHub security
scan and live installation verification. Do not add `SKILL.md`,
`openclaw.plugin.json`, runtime code, headers, or credentials to bypass the
admission gate.

Current official references:

- https://github.com/openclaw/openclaw/blob/main/docs/plugins/bundles.md
- https://github.com/openclaw/clawhub/blob/main/docs/clawhub.md
- https://github.com/openclaw/clawhub/blob/main/docs/cli.md
