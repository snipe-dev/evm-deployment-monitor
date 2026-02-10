<div align="center">

<img src="https://raw.githubusercontent.com/snipe-dev/spybot/master/src/assets/logo.png" height="400" alt="Spybot Logo" />

<br/>
<br/>

<strong>
Production-grade EVM Deployment monitoring system
</strong>

<br/>
<br/>

![Last Commit](https://img.shields.io/github/last-commit/snipe-dev/spybot?style=flat-square)
![Stars](https://img.shields.io/github/stars/snipe-dev/spybot?style=flat-square)
![Node](https://img.shields.io/badge/node-22+-blue?style=flat-square&logo=node.js)
![TypeScript](https://img.shields.io/badge/typescript-5.x-blue?style=flat-square&logo=typescript)

</div>

---

# EVM Deployment Monitor

EVM Deployment Monitor is a real-time infrastructure component for
tracking contract deployments across EVM-compatible networks.

The system scans new blocks, detects contract creation transactions
(`CREATE` / `CREATE2`), identifies ERC-20 token deployments, and applies
post-processing analytics such as ERC-20 `approve` and `swap` activity
tracking.

Built on top of the proven transaction processing and decoding modules
originally developed for SpyBot, this project focuses specifically on
deployment intelligence and token-level behavioral signals.

------------------------------------------------------------------------

## Core Capabilities

- Real-time block processing for any EVM-compatible network
- Detection of contract deployment transactions
- ERC-20 token identification at deployment time
- Post-deployment ERC-20 analytics:
    - Approve tracking
    - Swap detection
- Structured event stream suitable for:
    - Telegram bots
    - Webhooks
    - Databases
    - Custom plugins
- Chain-agnostic architecture

------------------------------------------------------------------------

## High-Level Flow

1. BlockReader polls new blocks.
2. MultinodePublicClient ensures RPC reliability.
3. DeploymentProcessor filters `CREATE` / `CREATE2` transactions.
4. ERC20Detector validates token contracts.
5. TokenActivityAnalyzer monitors `approve` and `swap` activity.
6. EventDispatcher forwards structured events to configured consumers.

------------------------------------------------------------------------

## Architecture

The system follows a layered, event-driven design:

### Transport Layer

- MultinodePublicClient
- BlockReader
- Normalized block and transaction delivery

### Processing Layer

- DeploymentProcessor
- Deduplication logic
- Fast-first decoding strategy

### Detection Layer

- ERC20 bytecode heuristics
- Function selector analysis
- Optional trace-based validation

### Analytics Layer

- ERC-20 approve tracking
- Swap detection via known router patterns

### Delivery Layer

- Plugin-based consumers
- Telegram integration (optional)
- Extensible event outputs

All upper layers operate on normalized EVM transaction data, making the
monitor fully chain-agnostic.

------------------------------------------------------------------------

## Design Principles

- Infrastructure-first architecture
- Plugin-oriented extension model
- Memory-bounded deduplication
- RPC fault tolerance
- Deterministic event generation
- Separation of transport, detection, and delivery

------------------------------------------------------------------------

## Production Considerations

- Handles unreliable RPC nodes via multi-node strategy
- Supports horizontal scaling
- Stateless block processing
- Suitable for high-frequency deployment monitoring
- Designed for integration into larger EVM analytics systems

------------------------------------------------------------------------

## Technology Stack

- TypeScript
- viem
- eventemitter3
- MySQL / SQLite
- grammY

------------------------------------------------------------------------

## Requirements

- Node.js 18+
- RPC endpoints for target EVM networks

------------------------------------------------------------------------

## Installation

``` bash
npm install
npm start
```

------------------------------------------------------------------------

## Roadmap

- Advanced honeypot detection
- Liquidity add detection
- Initial liquidity analysis
- Risk scoring engine
- Extended plugin SDK
- Galaxy brain test

------------------------------------------------------------------------

Designed as a reusable infrastructure component for real-time EVM
contract deployment intelligence.
