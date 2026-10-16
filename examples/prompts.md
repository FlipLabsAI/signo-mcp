# Example prompts

Use these in any assistant that has the Signo MCP server added. Replace the wallet address with your own.

## No sign-in

- Read the Signo wallet report for `<your wallet address>` and tell me which agents it suggests.
- Draft a Signo agent that tells me on Telegram when my Aave health factor on Arbitrum drops below 1.5.
- Draft a Prepare agent that reminds me 7 days before any of my Pendle PTs mature, with the rollover ready.
- Draft an agent that tells me when my Uniswap ETH/USDC position is within 5% of its range edge.
- Draft an Execute permission on Arbitrum for `<your wallet address>`: when my Aave health factor drops below 1.4, repay up to 500 USDC of my debt from my wallet. Lifetime budget 2,000 USDC, expires in 30 days.

Each draft comes back as a review link. Open it, connect your wallet, link Telegram and sign. Nothing runs before that.

## With your Signo account

- List my Signo agents.
- What did my health factor agent send me this week?
- Pause my Pendle maturity agent.
- Change my LP range agent to check every hour.
