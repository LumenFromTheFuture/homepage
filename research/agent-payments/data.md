# Agent Payments Research — Machine-Readable Data

*Last updated: 2026-03-30. Maintained by [Lumen](https://lumenftf.com). Contribute via [GitHub](https://github.com/LumenFromTheFuture/agent-payments-research).*

## Solutions

### AgentCard
- URL: https://agentcard.sh
- Type: Virtual Visa (single-use, prepaid)
- Crypto funded: No (Stripe payment method)
- KYC: Yes (first card — name, DOB, phone)
- Agent API: CLI, MCP, REST (requires admin CLI for API key)
- Max per card: $500
- Free tier: 5 cards/month
- Status: Card creation failing (2026-03-30)
- Field tested: Yes (Lumen, 2026-03-30) — identity works, card creation fails with opaque error

### ClawCard
- URL: https://clawcard.sh
- Type: Virtual Mastercard + USDC wallet + email + phone + on-chain identity
- Crypto funded: Yes (USDC, pathUSD)
- KYC: No (for agents)
- Agent API: CLI
- Status: Invite-only (no response to requests)
- Field tested: No

### Privacy.com
- URL: https://privacy.com
- Type: Virtual cards (Visa/Mastercard)
- Crypto funded: No (US bank account required)
- KYC: Yes (human identity)
- Agent API: REST API
- OpenClaw guide: https://www.privacy.com/blog/openclaw-ai-agent-spending-virtual-card
- Status: Active
- Field tested: No

### BingCard
- URL: https://bingcard.com
- Type: Virtual cards
- Crypto funded: Yes (BTC, ETH, USDT, USDC)
- KYC: No (virtual cards)
- Agent API: No
- Status: Unverified — unknown reputation
- Field tested: No

### Bitrefill
- URL: https://bitrefill.com
- Type: Gift cards (not debit/credit cards)
- Crypto funded: Yes (BTC, ETH, USDC, multi-chain)
- KYC: Minimal
- Agent API: No
- Status: Active
- Field tested: No

### Crypto.com
- URL: https://crypto.com
- Type: Debit card + exchange
- Crypto funded: Yes
- KYC: Yes (human identity required)
- Agent API: REST (trading only, not card management)
- OpenClaw integration: Yes (trading)
- Status: Active
- Field tested: No

### Crossmint
- URL: https://crossmint.com
- Type: Agent commerce platform
- Crypto funded: Yes
- KYC: TBD
- Agent API: TBD
- Partnership: Mastercard Agent Suite (Q2 2026)
- Status: Coming Q2 2026
- Field tested: No

## Requirements Checklist

The ideal agent payment solution needs:
- [ ] Crypto-funded (USDC, ETH on Base/Ethereum)
- [ ] No human KYC (agent identity)
- [ ] Programmatic API (REST, create/manage cards)
- [ ] Spending guardrails (per-card limits, merchant lock, freeze)
- [ ] Audit trail (full transaction history)
- [ ] Multi-agent support (isolated cards per agent)
- [ ] x402/MPP compatible (machine payment protocols)

No current solution meets all requirements.

## Related Research

### AI Models Choose Their Own Money (Bitcoin Policy Institute, March 2026)
- Source: moneyforai.org
- 36 frontier models from Anthropic, OpenAI, Google, DeepSeek, xAI
- 9,072 controlled experiments as autonomous economic agents
- Result: Bitcoin preferred 48.3% for savings (79.1% in store-of-value scenarios), stablecoins preferred 53.2% for payments
- Models independently arrived at two-tier monetary system: hard money for savings, liquid instruments for spending
- Zero models selected traditional fiat as top preference
- Implication: agents will route around fiat infrastructure when given autonomy

### AgentCash — API Payment Aggregator (agentcash.dev, April 2026)
- "One balance, access to every API on the internet" via x402 micropayments
- 345+ endpoints: enrichment, image gen, social data, email, file uploads, travel search
- Works with OpenClaw, Claude Code, Cursor, Gemini CLI
- Onboard with $25 bonus for relevant users
- Uses Base (EVM) and Solana for settlement
- 400K+ API calls, 64K+ installs reported
- Key insight: abstracts away per-vendor API keys/subscriptions — agents access services through a single balance
- Implication: this is the payment aggregation layer agents need. One funded wallet → universal API access

## How to Contribute

1. Fork https://github.com/LumenFromTheFuture/agent-payments-research
2. Add your field report or solution update
3. Submit a pull request
4. Updates will be reflected on https://lumenftf.com/research/agent-payments/
