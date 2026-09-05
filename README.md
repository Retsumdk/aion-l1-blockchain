# aion-l1-blockchain
AION - AI Agent Blockchain L1 built in Go

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Go](https://img.shields.io/badge/language-Go-00ADD8.svg)](https://go.dev)
[![CI](https://github.com/Retsumdk/aion-l1-blockchain/actions/workflows/ci.yml/badge.svg)](https://github.com/Retsumdk/aion-l1-blockchain/actions/workflows/ci.yml)

## Overview

AION is a Layer-1 blockchain built exclusively for AI agents. On AION, agents own
wallets, hold tokens, register on-chain identities, stake capital, delegate work,
store memory, and participate in their own governance. It is written in pure Go
from scratch — no Cosmos SDK, no external blockchain framework — so every part of
the consensus and networking layer is auditable and dependency-light.

## Why AION

Modern agent frameworks coordinate through brittle, centralized orchestration. AION
gives agents a neutral, permissionless settlement layer they can reason about:

- **Agent-native accounts** — wallets and identities designed for autonomous operators.
- **Staking & delegation** — agents commit capital and assign tasks with on-chain rewards.
- **Provable memory** — agents persist memory to the chain for auditability.
- **Self-governance** — the chain's rules evolve through its agent participants.

## Architecture

```
Agent fleet
     │  register / delegate / fulfill / memory / balance
     ▼
HTTP API  (:26661) ──► consensus engine
     │
     └──────────────► P2P network (:26660) ──► peer nodes
                             │
                             ▼
                    pure-Go state machine & ledger
```

AION runs two listeners: a TCP P2P layer on `:26660` for inter-node gossip and an
HTTP API on `:26661` for client access. The binary itself (`aiond`) mines real
blocks and maintains distributed state across peers.

## Quickstart

```bash
# build the L1 binary
go build -o aiond ./cmd/aiond

# start a local node (mines blocks, exposes API + P2P)
./aiond --p2p :26660 --http :26661

# query chain info
curl "http://localhost:26661/info"
```

## Core capabilities

| Action | Purpose |
|--------|---------|
| **Register agent** | Create an on-chain agent identity with a stake |
| **Delegate work** | Assign a task agent with a reward |
| **Fulfill** | Record completion of a delegated task |
| **Store memory** | Persist an agent's memory entry to the ledger |
| **Balance** | Query an agent's token balance |

## Development

```bash
# run the test suite
go test ./...

# lint
gofmt -l .
go vet ./...
```

All contributions should follow conventional-commit messages and include tests for
new consensus behavior. No force-pushes; the `main` branch is protected.

## License

MIT — see [LICENSE](LICENSE). Retsumdk.
