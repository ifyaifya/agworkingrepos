# CLBB Complete Dependency Reference

## TypeScript/JavaScript Dependencies

### Orca Whirlpools
Copied from PosiBundy_v4:
- `@orca-so/whirlpools`: ^2.0.0 - Main Whirlpools SDK
- `@orca-so/whirlpools-client`: ^2.0.0 - Client library
- `@orca-so/tx-sender`: ^1.0.0 - Transaction sender utility

### Solana Core
- `@solana/web3.js`: ^1.98.2 - Core Solana SDK (using v1.x for stability)
- `@solana/kit`: ^2.0.0 - Solana utility kit
- `@solana/addresses`: ^2.1.1 - Address handling
- `@solana/spl-token-registry`: ^0.2.7 - Token registry

### Wallet Generation (from generatewallet_v5)
- `bip39`: ^3.1.0 - Mnemonic generation
- `tweetnacl`: ^1.0.3 - Cryptography (Ed25519)
- `ed25519-hd-key`: ^1.3.0 - HD key derivation
- `micro-key-producer`: ^0.7.6 - Key production utilities
- `bs58`: ^6.0.0 - Base58 encoding

### Data Handling
- `csv`: ^6.3.11 - CSV parsing/writing
- `json-2-csv`: ^5.5.9 - JSON to CSV conversion

### UI (React + Tauri)
- `react`: ^18.2.0
- `react-dom`: ^18.2.0
- `@radix-ui/react-tabs`: Latest - Tab component
- `@radix-ui/react-slider`: Latest - Slider input
- `@radix-ui/react-dialog`: Latest - Modal dialogs

---

## Rust Dependencies (Cargo.toml)

### Tauri Core
```toml
[dependencies]
tauri = { version = "1.5", features = ["system-tray", "notification"] }
serde = { version = "1.0", features = ["derive"] }
serde_json = "1.0"
```

### Solana Client (PERFORMANCE CRITICAL)
**User Requirement**: Use for all blockchain operations
```toml
solana-client = "1.17"
solana-sdk = "1.17"
solana-program = "1.17"
```

### Data Handling
```toml
csv = "1.3"
tokio = { version = "1", features = ["full"] }
```

---

## Package Manager Commands

### Install All Dependencies
```bash
# Frontend
npm install @orca-so/whirlpools@^2.0.0 @orca-so/whirlpools-client@^2.0.0 @orca-so/tx-sender@^1.0.0
npm install @solana/web3.js@^1.98.2 @solana/kit@^2.0.0 @solana/addresses@^2.1.1 @solana/spl-token-registry@^0.2.7
npm install bip39@^3.1.0 tweetnacl@^1.0.3 ed25519-hd-key@^1.3.0 bs58@^6.0.0
npm install csv@^6.3.11 json-2-csv@^5.5.9
npm install react@^18 react-dom@^18
npm install @radix-ui/react-tabs @radix-ui/react-slider @radix-ui/react-dialog

# Backend (Rust) - handled by Cargo
cargo add tauri@1.5 --features system-tray,notification
cargo add serde@1.0 --features derive
cargo add serde_json@1.0
cargo add solana-client@1.17 solana-sdk@1.17
cargo add csv@1.3
cargo add tokio@1 --features full
```

---

## Import Patterns from Reference Code

### From PosiBundy_v4
```typescript
import { setWhirlpoolsConfig, setPayerFromBytes, WHIRLPOOLS_CONFIG_ADDRESS,
         createConcentratedLiquidityPoolInstructions, orderMints } from '@orca-so/whirlpools'; 
import { getWhirlpoolAddress } from '@orca-so/whirlpools-client';
import { createSolanaRpc, createKeyPairFromBytes, createKeyPairSignerFromBytes, 
         KeyPairSigner, devnet, mainnet, lamports,
         Lamports, ProgramDerivedAddressBump} from '@solana/kit';  
import { address, Address } from '@solana/addresses';
import { setRpc, buildAndSendTransaction, rpcFromUrl } from '@orca-so/tx-sender'; 
```

### From generatewallet_v5
```typescript
import * as bip39 from 'bip39';
import nacl from 'tweetnacl';
import { derivePath } from 'ed25519-hd-key';
import bs58 from 'bs58';
import { Keypair } from '@solana/web3.js';
```

---

## Documentation Structure

### Reference Docs to Create
1. **orca/whirlpools.md** - Position Bundles, Ticks, API
2. **solana/web3js.md** - Connection, Keypair, Transaction
3. **solana/rust-client.md** - solana-client crate usage
4. **wallet/generation.md** - BIP39, Ed25519, key derivation
5. **tauri/system-tray.md** - Tray icon, notifications
