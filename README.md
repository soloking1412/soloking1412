<div align="center">

# Maheswaran Velmurugan
### Full Stack · Backend · Blockchain · Smart Contract Developer

**Building production infrastructure across 8+ chains — solo, grant-funded, shipped.**

[![Twitter](https://img.shields.io/badge/@lord__soloking-000?style=flat-square&logo=x&logoColor=white)](https://x.com/lord_soloking)
[![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=flat-square&logo=telegram&logoColor=white)](https://t.me/maheswar1412)
[![NPM](https://img.shields.io/badge/stylus--toolkit-npm-CB3837?style=flat-square&logo=npm&logoColor=white)](https://www.npmjs.com/package/stylus-toolkit)
[![Sherlock](https://img.shields.io/badge/Sherlock-Auditor-1A1A2E?style=flat-square&logo=shield&logoColor=white)](https://audits.sherlock.xyz/watson/soloking)
[![PBA](https://img.shields.io/badge/Polkadot_Blockchain_Academy-Graduate-E6007A?style=flat-square&logo=polkadot&logoColor=white)](https://polkadot.network/development/blockchain-academy/)

</div>

---

## About

Full stack and blockchain developer with a focus on developer tooling, DeFi protocol engineering, and smart contract security. I build end-to-end — TypeScript CLI tools, Python SDKs, React frontends, Solidity/Clarity/Rust smart contracts, and backend indexers — and I ship independently without a team.

Grant recipient from the Arbitrum Foundation and the Stacks Foundation. Active security researcher with 20+ confirmed High/Medium findings across Sherlock, Code4rena, Cantina, and Immunefi. Polkadot Technical Fellowship candidate and Polkadot Blockchain Academy graduate, with open-source contributions to `paritytech/polkadot-sdk`. I audit the same protocols I know how to build, which means I find what others miss.

**Languages:** TypeScript · Python · Solidity · Rust · Clarity · Cairo · Move · JavaScript  
**Frameworks:** Node.js · React · Next.js · Hardhat · Foundry · Anchor · web3.py · viem  
**Chains:** Ethereum · Arbitrum · Solana · Stacks · Rootstock · Polkadot · Starknet · BNB · Aptos

---

## Featured Projects

### [Stylus-Toolkit](https://github.com/soloking1412/Stylus-Toolkit) — `npm install -g stylus-toolkit`

> **CLI development environment for Arbitrum Stylus (Rust) smart contracts. Think Hardhat, but for Stylus.**

Arbitrum grant-approved. Shipped both milestones.
![npm downloads](https://img.shields.io/npm/dt/stylus-toolkit?style=flat-square&label=npm%20downloads)
![stars](https://img.shields.io/github/stars/soloking1412/Stylus-Toolkit?style=flat-square)

```bash
stylus-toolkit init --name my-token --template erc20
stylus-toolkit build
stylus-toolkit profile
```

```
┌──────────────────────┬──────────────┬──────────────┬────────────┬────────┐
│ Function             │ Rust (Stylus)│ Solidity     │ Savings    │ %      │
├──────────────────────┼──────────────┼──────────────┼────────────┼────────┤
│   read               │ 5,000        │ 6,000        │ 1,000      │ 16.67% │
│   write              │ 12,000       │ 20,000       │ 8,000      │ 40.00% │
│   compute            │ 8,000        │ 15,000       │ 7,000      │ 46.67% │
│   oracle             │ 75,000       │ 103,000      │ 28,000     │ 27.18% │
│ Avg per-call         │ -            │ -            │ -          │ 32.6%  │
└──────────────────────┴──────────────┴──────────────┴────────────┴────────┘
✅ 32.6% average gas savings proven · 26%+ full TCO savings
```

**What it does:** `init` with 4 templates (basic, ERC20, ERC721, DeFi) · `build` to WASM · `profile` for side-by-side Rust vs Solidity gas benchmarks · `dashboard` analytics web UI · `dev` one-command Docker testnet · `deploy` to local / Arbitrum Sepolia / Arbitrum One

**Stack:** TypeScript · Node.js · Rust · Docker · GitHub Actions CI

---

### [Rootstock-Agentic-DeFi-Framework](https://github.com/soloking1412/Rootstock-Agentic-DeFi-Framework)

> **MCP framework that lets AI agents autonomously manage DeFi positions on Rootstock/Bitcoin — with policy enforcement and session-scoped spend limits.**

```
MCP Client (Claude / any AI)
        │
        ▼
   MCP Server (5 tools)
        ├── get_protocol_data  → Money on Chain + Tropykus RPC
        ├── simulate_swap      → viem call/estimateGas (no broadcast)
        ├── execute_intent     → Session validation → Policy engine → sendRawTransaction
        ├── get_position_health → Tropykus health factor
        └── get_wallet_balances → RBTC + ERC-20 balances
```

5 hard-coded policy rules block every unsafe action before broadcast — zero-address transfers, selfdestruct calls, single-tx values over 10 RBTC, spend cap overflows, and non-whitelisted contracts. Every decision (allow or deny) is written to an audit log.

**Protocol integrations:** Money on Chain (MoCState — BTC price, coverage ratio, BPRO/DOC rates) · Tropykus (Compound fork — supply/borrow APY, per-account health factor)

**Stack:** TypeScript · `@modelcontextprotocol/sdk` · `viem` · `zod` · `tsup` · Node.js ≥ 20

---

### [Rootstock-Python-SDK](https://github.com/soloking1412/Rootstock-Python-SDK) — `pip install rootstock-sdk`

> **Python SDK for the Rootstock (RSK) blockchain — wallet management, ERC-20 tokens, smart contracts, RNS domain resolution.**

```python
from rootstock import RootstockProvider, Wallet, ERC20Token

provider = RootstockProvider.from_mainnet()
wallet   = Wallet.from_private_key("0x...", chain_id=30)

# ERC-20 in 3 lines
rif = ERC20Token.from_symbol(provider, "RIF")
print(rif.balance_of_human(wallet.address))   # "150.5"
receipt = rif.transfer(wallet, to="0x...", amount=100 * 10**18)

# EIP-1191 Rootstock-specific checksum
addr = to_checksum_address("0x5aaeb6...", chain_id=30)
```

**Covers:** Wallet create/import/encrypt · RBTC transfers · ERC-20 (balance, transfer, approve) · arbitrary contract call/transact · RNS forward + reverse resolution · gas estimation · mainnet and testnet

**Stack:** Python ≥ 3.10 · web3.py · eth-account · pytest · ruff · PyPI published

---

### [satoshi-yield](https://github.com/soloking1412/satoshi-yield)

> **Non-custodial sBTC yield optimizer on Stacks — compare live APY across Bitflow, ALEX, Zest, Velar, and Hermetica; rebalance in one atomic Clarity call.**

```clarity
;; vault.clar — core deposit/withdraw, 5% performance fee on yield only
(define-public (deposit (amount uint)))
(define-public (withdraw (amount uint)))
(define-read-only (get-position (user principal)))
(define-read-only (get-accrued-yield (user principal)))
```

```clarity
;; yield-source trait — every protocol adapter implements this
(define-trait yield-source-trait
  ((get-current-apy  ()    (response uint uint))
   (deposit-sbtc     (uint) (response bool uint))
   (withdraw-sbtc    (uint) (response bool uint))))
```

Adding a new protocol = one new adapter contract. Core vault never changes.

**Architecture:** `contracts/` (Clarity 4: vault, yield-tracker, rebalancer, trait) · `indexer/` (Node.js + TypeScript APY fetchers for each protocol, Express API) · `frontend/` (React + Stacks.js, Leather + Xverse wallet connection, YieldTable, PositionCard, RebalanceModal)

**Stack:** Clarity 4 · Clarinet · TypeScript · React · Stacks.js · Vercel + Railway · Stacks Foundation grant

---

## Open Source Contributions

Beyond my own repos, I contribute directly to protocol-level infrastructure used by other teams:

- **[Bitcoin Dev Kit (BDK)](https://github.com/bitcoindevkit/bdk)** — Added a `fuzz/` crate with three cargo-fuzz targets: `apply_update` (fuzzing `Wallet::apply_update` with arbitrary txs/anchors), `create_tx` (fuzzing `build_tx` with arbitrary fee rates, amounts, and RBF), and `descriptor_parse` (fuzzing arbitrary bytes through `IntoWalletDescriptor`, covering miniscript/key-path/checksum handling) — plus a `fuzz.yml` CI workflow that builds on every PR and runs extended 60-second fuzzing sessions weekly with crash-artifact upload. ([issue #61](https://github.com/bitcoindevkit/bdk/issues/61))
- **[Polkadot SDK](https://github.com/paritytech/polkadot-sdk)** — Open and merged pull requests on `pallet-revive`'s Ethereum JSON-RPC layer, part of ongoing Polkadot Technical Fellowship work. ([view my PRs →](https://github.com/paritytech/polkadot-sdk/pulls?q=is%3Apr+author%3Asoloking1412))

---

## Currently Building

| Project | What | Ecosystem |
|---|---|---|
| **Ansim** | Non-custodial consumer-protection layer for KRW-stablecoin payments — reversible-window escrow, pre-sign safety screen, Dojang-anchored dispute resolution | GIWA (OP Stack) · GASOK accelerator |
| **AvaGuard** | Circuit breaker + Guardian Agent SDK + Invariant CLI for Avalanche L1s — 30 tests, deployed | Avalanche |
| **SoroGuard** | Position-protection protocol for Stellar DeFi | Stellar |
| **ComputeLens** | Compute-unit profiler for Solana programs | Solana |

---

## Shipped & Deployed

| Project | What | Status |
|---|---|---|
| [Stylus-Toolkit](https://github.com/soloking1412/Stylus-Toolkit) | CLI toolchain for Arbitrum Stylus — build, profile, deploy | ✅ Live on NPM · Arbitrum grant · Both milestones shipped |
| [Rootstock-Agentic-DeFi-Framework](https://github.com/soloking1412/Rootstock-Agentic-DeFi-Framework) | AI agent DeFi execution layer on Rootstock/Bitcoin | ✅ Active |
| [Rootstock-Python-SDK](https://github.com/soloking1412/Rootstock-Python-SDK) | Python SDK for RSK — wallets, ERC-20, contracts, RNS | ✅ Published on PyPI |
| [satoshi-yield](https://github.com/soloking1412/satoshi-yield) | sBTC yield optimizer on Stacks | 🔄 In development · Stacks Foundation grant |
| AvaGuard | Circuit breaker + Guardian Agent SDK for Avalanche L1s | ✅ Deployed · 30 tests passing |

---

## Security Research

20+ confirmed High/Medium findings across Sherlock, Code4rena, Cantina, and Immunefi. The same protocol knowledge that lets me build DeFi tooling also lets me find what breaks it.

| Severity | Protocol | Finding | Platform |
|---|---|---|---|
| 🔴 High | SuperDCA | Missing reward claiming mechanism — users permanently lose yield | Sherlock |
| 🔴 High | SukukFi | Cross-vault share fungibility breaks fund isolation | Sherlock |
| 🔴 High | Threshold Network | Force-decrease authorization logic inversion — unauthorized stake slashing | Immunefi |
| 🟡 Medium | Merkl | Pre-deposit double-spend — campaign rewards claimable before funding | Sherlock |
| 🟡 Medium | SukukFi | KYC fund lock — compliant users permanently locked out | Sherlock |
| 🟡 Medium | Inverse Finance | DOS at `MIN_ASSETS` in jDOLA vault — deposits permanently frozen | Sherlock |
| 🟡 Medium | Brix Money | Cooldown stacking bypass — withdrawal delay circumventable | Sherlock |
| 🟡 Medium | LicenseToken | IP derivative registration DOS via gas exhaustion | Cantina |

**Rankings:** #45 Ammplify · #48 Super DCA on Sherlock — [full audit history →](https://audits.sherlock.xyz/watson/soloking)

---

## Tech Stack

**Languages**

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Solidity](https://img.shields.io/badge/Solidity-363636?style=flat-square&logo=solidity&logoColor=white)
![Rust](https://img.shields.io/badge/Rust-000000?style=flat-square&logo=rust&logoColor=white)
![Clarity](https://img.shields.io/badge/Clarity-5546FF?style=flat-square)
![Cairo](https://img.shields.io/badge/Cairo-FF6B35?style=flat-square)
![Move](https://img.shields.io/badge/Move-6B46C1?style=flat-square)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)

**Frameworks & Tooling**

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![Foundry](https://img.shields.io/badge/Foundry-000000?style=flat-square&logo=ethereum&logoColor=orange)
![Hardhat](https://img.shields.io/badge/Hardhat-FFF100?style=flat-square&logoColor=black)
![Anchor](https://img.shields.io/badge/Anchor-9945FF?style=flat-square&logo=solana&logoColor=white)
![Clarinet](https://img.shields.io/badge/Clarinet-5546FF?style=flat-square)
![viem](https://img.shields.io/badge/viem-1a1a1a?style=flat-square)
![web3.py](https://img.shields.io/badge/web3.py-3776AB?style=flat-square&logo=python&logoColor=white)

**Chains**

![Ethereum](https://img.shields.io/badge/Ethereum-3C3C3D?style=flat-square&logo=ethereum&logoColor=white)
![Arbitrum](https://img.shields.io/badge/Arbitrum-28A0F0?style=flat-square)
![Solana](https://img.shields.io/badge/Solana-9945FF?style=flat-square&logo=solana&logoColor=white)
![Stacks](https://img.shields.io/badge/Stacks-5546FF?style=flat-square)
![Rootstock](https://img.shields.io/badge/Rootstock-FF6B35?style=flat-square)
![Polkadot](https://img.shields.io/badge/Polkadot-E6007A?style=flat-square&logo=polkadot&logoColor=white)
![Starknet](https://img.shields.io/badge/Starknet-FF6B35?style=flat-square)
![BNB Chain](https://img.shields.io/badge/BNB_Chain-F3BA2F?style=flat-square&logo=binance&logoColor=black)
![Aptos](https://img.shields.io/badge/Aptos-00B4CC?style=flat-square)

---

## GitHub Stats

![GitHub Stats](https://github-readme-stats.vercel.app/api?username=soloking1412&show_icons=true&theme=radical&hide_border=true)
![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=soloking1412&layout=compact&theme=radical&hide_border=true)

---

## Open to

Security reviews · Protocol audits · Full stack / backend / blockchain engineering roles · Ecosystem grants · Dev tooling collaborations

<div align="center">
<sub>Tamil Nadu, India · Polkadot Blockchain Academy Graduate · Polkadot Technical Fellowship Candidate · Superteam India · Solo since day one</sub>
</div>
