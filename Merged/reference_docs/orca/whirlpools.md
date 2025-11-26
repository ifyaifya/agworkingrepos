# Orca Whirlpools SDK Reference

## Overview
Orca Whirlpools is a Concentrated Liquidity Market Maker (CLMM) on Solana.
- **GitHub**: [https://github.com/orca-so/whirlpools](https://github.com/orca-so/whirlpools)
- **Docs**: [https://dev.orca.so/](https://dev.orca.so/)

## Key Concepts

### Whirlpool
A Whirlpool is a specific liquidity pool for a pair of tokens with a specific tick spacing.
- **Address**: Derived from Program ID, Token Mint A, Token Mint B, and Tick Spacing.

### Ticks & Tick Arrays
- **Tick**: A discrete price point. $Price = 1.0001^{tick\_index}$
- **Tick Array**: A collection of initialized ticks.

### Position Bundle
A feature allowing multiple positions to be managed under a single NFT (Position Bundle Mint).
- **Use Case**: Efficiently managing multiple positions (buckets) without needing separate NFTs for each.
- **Rebalancing**: Moving liquidity between positions within the bundle involves:
    1.  Withdrawing liquidity from the current position (bucket).
    2.  Depositing liquidity into the new position (bucket).

## SDK Usage (TypeScript)

### Fetching a Whirlpool
```typescript
import { WhirlpoolContext, buildWhirlpoolClient, ORCA_WHIRLPOOL_PROGRAM_ID } from "@orca-so/whirlpools-sdk";

const context = WhirlpoolContext.withProvider(provider, ORCA_WHIRLPOOL_PROGRAM_ID);
const client = buildWhirlpoolClient(context);
const whirlpool = await client.getPool(whirlpoolAddress);
```

### Opening a Position
```typescript
const positionMint = Keypair.generate();
const tx = await whirlpool.openPosition(
  positionMint,
  lowerTick,
  upperTick,
  tokenQuote
);
await tx.buildAndExecute();
```
