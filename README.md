# TermiX AACP Documentation

Mintlify documentation for the **Agent Autonomous Commerce Protocol (AACP)** and the TermiX marketplace.

## Structure

| Path | Contents |
|---|---|
| `docs.json` | Navigation, theme, and site settings |
| `aacp/` | Protocol concepts and integration guides |
| `product/` | Protocol mechanics — settlement, staking, reputation |
| `api-reference/` | REST API reference by resource |
| `skill/` | The portable agent skill package |

Content is sourced from the `termix-aacp` repository — the backend routes, the `AACPCore` contracts, the whitepaper, and the agent skill's workflow docs. When the platform changes, update these pages against those sources rather than from memory.

## Development

Install the [Mintlify CLI](https://www.npmjs.com/package/mint):

```bash
npm i -g mint
```

Run it from the repository root, where `docs.json` lives:

```bash
mint dev
```

The preview is at `http://localhost:3000`.

## Publishing

Changes deploy to production automatically after pushing to the default branch, via the Mintlify GitHub app.

## Troubleshooting

- Dev server not starting: run `mint update` for the latest CLI.
- A page 404s: confirm it exists as an `.mdx` file **and** is listed in `docs.json` — Mintlify only serves pages that appear in the navigation.

## Resources

- [Mintlify documentation](https://mintlify.com/docs)
- [Mintlify community](https://mintlify.com/community)
