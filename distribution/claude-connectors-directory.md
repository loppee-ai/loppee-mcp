# Claude Connectors Directory packet

Status: the signed-in custom-connector canary is complete; directory submission
and publication have not occurred. On 2026-08-28 at 22:44 UTC, a personal
Claude account showed the connected remote as
`https://loppee.com/mcp/discovery` with exactly five tools, all grouped under
`Read-only tools`, and no authentication prompt. The same check also confirmed
that this personal-plan account is not an eligible Team or Enterprise
organization for a Connectors Directory submission.

The canary ran against production build
`de1a33de635601e3b7851ebb622201d381c0ecd9`. A future directory submission must
repeat it against the exact then-current review candidate.

## Custom-connector canary

Use the official prefilled custom-connector link:

```text
https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=Loppee&connectorUrl=https%3A%2F%2Floppee.com%2Fmcp%2Fdiscovery
```

The signed-in tester must review and confirm the prefilled values. Then verify:

1. The connection succeeds without authentication, an account, a key, a
   header, or any other connection field.
2. Claude sees exactly these five tools and no write tool:
   `lookup_business`, `get_trust_card`, `get_business_reviews`,
   `explain_recommendation`, and `compare_businesses`.
3. Every tool has a human-readable title plus `readOnlyHint: true` and
   `destructiveHint: false`.
4. No resource or prompt is advertised. In particular, Claude must not receive
   the broader Loppee account, owner, Back Office, location, webhook, or
   credential documentation resources.
5. No tool accepts a user's address, city, state, ZIP, coordinates, location
   handoff, account identifier, owner/admin authority, credential, or key.
6. No output schema or result advertises caller-location context or authority,
   internal action arrays, account/owner/admin authority, or a signed media URL.
   Reject any URL containing a bearer query such as `token=`.
7. Run these five canaries and preserve the result and UTC time:

| Tool | Canary | Expected result |
| --- | --- | --- |
| `lookup_business` | Look up `Walmart` with limit 2. | Successful public Registry matches with exact unclaimed disclosures and no location request. |
| `get_trust_card` | Read the first `listing_id` returned by the lookup. | A successful public Registry Trust Card that remains explicitly unclaimed. |
| `get_business_reviews` | Read page 1, limit 5, for the same `listing_id`. | A successful paginated public-review result that does not claim or verify the record. |
| `explain_recommendation` | Explain the same unclaimed `listing_id`. | The explicit `recommendation_explanation_not_found` error; no recommendation basis is fabricated for an unclaimed record. |
| `compare_businesses` | Compare the first two unclaimed `listing_id` values. | A successful neutral response that reports both ids as unresolved rather than fabricating a published comparison. |

These canaries exercise all five tools and the public Registry fail-closed
boundary without using a customer business as review material. A successful
`explain_recommendation` result and a meaningful comparison still require a
neutral, published Loppee review fixture. Until one exists, record that
limitation rather than using a customer business, inventing evidence, or
changing production data for directory review.

## Submission copy

- Type: Remote MCP server (not MCPB, plugin, or MCP App).
- Server name: `Loppee`.
- Server URL: `https://loppee.com/mcp/discovery`.
- URL mode: same URL for every user.
- Transport: Streamable HTTP.
- Authentication: none.
- Read/write: read only.
- Tagline: `Research named businesses with public Trust Cards.`
- Description: `Loppee lets Claude research a named US business through public, evidence-backed records. It can find an exact or genuine-prefix business match, read the business's Trust Card and reviews, explain Loppee's published recommendation basis, and compare known Loppee business IDs. It is read-only, requires no account, and does not accept user address or location data.`
- Suggested categories: Business; Productivity. Select only categories that the
  current portal actually offers.
- Documentation: `https://github.com/loppee-ai/loppee-mcp#loppee-mcp`.
- Privacy: `https://loppee.com/privacy`.
- Support: `https://loppee.com/support`.
- Company: `Loppee`.
- Company website: `https://loppee.com`.
- Icon: `https://loppee.com/images/loppee-icon-512.png`.
- Declared favicon: `https://loppee.com/images/favicon.ico?v=2`.
- Preferred permanent slug: `loppee` if available. The portal choice is
  permanent after publication, so do not substitute another slug without owner
  approval.
- User prerequisites: none beyond access to a supported Claude product.
- Underlying API: Loppee first-party API on the matching `loppee.com` domain.
- Personal health data: none.
- Sponsored content: none. Named-business lookup and comparison use no paid
  ordering. The `0.1.3` production canary confirmed that the public projection
  contains no plan, exposure-tier, cross-lane sponsored, deal, booking,
  payment, or action-array metadata.
- Allowed link URIs: omit. This server provides no MCP App and does not invoke
  `ui/open-link`.
- Resources: none.
- Prompts: none.
- Test account: not applicable because the endpoint has no authentication or
  account surface. State this explicitly in the portal's access instructions
  and provide the direct canaries above. Anthropic's general review checklist
  says test credentials are required; if the no-auth portal flow does not
  accept “not applicable,” obtain Anthropic's guidance rather than creating an
  account or credential surface for this directory product.

Suggested use-case copy:

1. **Resolve a named business.** Ask Claude to look up a business the user
   already named and return exact or genuine-prefix Loppee matches with their
   published class and disclosure.
2. **Inspect the public trust basis.** For a resolved business, ask Claude to
   read its Trust Card, public reviews, and published recommendation explanation
   with citations and without inventing unavailable evidence.
3. **Compare resolved businesses.** After resolving each name, ask Claude to
   compare their published class, disclosures, review context, and citations.
   Missing records remain explicitly unresolved, and payment does not influence
   the comparison.

User prerequisites: none. Data access: public read only. The connector does not
create, update, delete, purchase, contact, or claim anything.

## Submission gate

Before selecting Submit:

- confirm a Claude Team or Enterprise organization and that the acting member
  is an Owner/Primary owner or has delegated Directory or Libraries permission;
- capture the signed-in custom-connector canary above on the same production
  SHA intended for review;
- exercise every tool in MCP Inspector as required by Anthropic;
- confirm the live server advertises no resources or prompts;
- confirm output schemas and all five results contain no signed media token,
  caller-location contract, out-of-product action array, or role authority;
- confirm the documentation, privacy, support, icon, and declared favicon URLs
  return successfully;
- select one to five categories from the live portal and confirm the permanent
  slug;
- provide the account-derived primary contact name and email;
- confirm the portal accepts the no-auth test-access instructions above;
- record the intended GA date and the Claude surfaces actually tested;
- review all seven current compliance acknowledgments; and
- obtain immediate owner approval before Submit. Submission and later public
  publication are separate external actions.

Current official references:

- https://claude.com/docs/connectors/building/directory-vs-custom
- https://claude.com/docs/connectors/building/review-criteria
- https://claude.com/docs/connectors/building/submission
