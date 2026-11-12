# Shopping fork

Active repository: https://github.com/behnawwm/torob-mcp-mmdju

This fork's main branch combines the changes submitted separately upstream:

- Dependencies: https://github.com/mmdju/torob-mcp/pull/5
- Local HTTP boundaries: https://github.com/mmdju/torob-mcp/pull/6
- Upstream origins, redirects and response limits: https://github.com/mmdju/torob-mcp/pull/7
- Merchant text and purchase-link safety: https://github.com/mmdju/torob-mcp/pull/8
- Shopping-list comparison: https://github.com/mmdju/torob-mcp/pull/9

## Local setup

```sh
npm ci --ignore-scripts
npm run build
codex mcp add torob --env TOROB_MCP_STORE=off -- node /absolute/path/to/torob-mcp-mmdju/dist/index.js
```

Use the absolute path to the node executable when the MCP client's PATH differs
from your terminal. The local entry point is stdio; no port or Torob account is
needed. The setting above disables disk persistence. Restart/reload your MCP
client after registration. Do not use the upstream hosted demo to access these
fork-only changes.

## Shopping flow

1. Search each item and confirm the exact model/variant.
2. Pass the selected cards' `prk`, `details_url` and desired quantities to
   `compare_shopping_list` (at most 10 distinct products).
3. Review shops by item coverage first, then subtotal. Missing or failed items
   remain explicit; unknown stock and unreliable prices are excluded. Shipping
   is excluded, and quantity availability is not guaranteed.
4. Use returned product links to favorite through the heart button in your
   logged-in Torob browser, or use the selected shop's buy links for cart entry.
   Confirm listing variants, warranty, stock, shipping and final total there.

Favorites, carts, ordering and payment are a browser/manual handoff. The MCP
never accepts login cookies, changes favorites, creates carts or places orders.

## Verification

- Reproducible install with lifecycle scripts disabled.
- All 228 offline tests pass on the combined main branch.
- Full dependency audit reports zero known vulnerabilities at verification time.
- Live stdio MCP check lists 16 tools, searches two public USB products and
  compares their sellers successfully. No favorites/cart/order changes made.
