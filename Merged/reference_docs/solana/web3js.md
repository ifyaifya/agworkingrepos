# Solana Web3.js Reference

## Overview
Official library for interacting with the Solana Blockchain.
- **Package**: `@solana/web3.js`
- **Version**: Focusing on v1.x for stability, but aware of v2.0.

## Core Classes

### Connection
Handles RPC JSON-API interaction.
```typescript
import { Connection, clusterApiUrl } from "@solana/web3.js";
const connection = new Connection(clusterApiUrl("mainnet-beta"), "confirmed");
```

### PublicKey
Representation of a base58 encoded address.
```typescript
import { PublicKey } from "@solana/web3.js";
const pubkey = new PublicKey("...");
```

### Keypair
Private/Public key pair for signing transactions.
```typescript
import { Keypair } from "@solana/web3.js";
// Load from secret key (Uint8Array)
const keypair = Keypair.fromSecretKey(secretKey);
```

### Transaction
Atomic set of instructions.
```typescript
import { Transaction, SystemProgram } from "@solana/web3.js";
const tx = new Transaction().add(
  SystemProgram.transfer({
    fromPubkey: payer.publicKey,
    toPubkey: recipient,
    lamports: 1000000,
  })
);
```

## RPC Handling
- **Rate Limits**: Use private RPCs for high-frequency bots.
- **Commitment**: Use `confirmed` for faster updates, `finalized` for safety.
