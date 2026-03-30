# 🐌 Snail Protocol

> **「我不在线，我的数据就不存在于网络。」**
>
> *我的数据我做主。慢慢来，重要的事情慢慢来。*

A decentralized, local-first social communication protocol implemented in Rust.

**Your data lives in your shell.**

## What is Snail Protocol?

Snail Protocol is an open protocol where **your data lives on your device, encrypted by keys only you hold**. When you go offline, your data vanishes from the network entirely. No relay servers. No blockchain required for social features. No token needed to post.

This is not another "decentralized" protocol that stores your data on someone else's server. This is actual data sovereignty — your private key is your only authority, and no third party can access your data without your explicit, revocable authorization.

## Why "Snail"?

A snail carries its home wherever it goes. Your data is your shell — it moves with you, protects you, and belongs to no one else. When you retreat, everything disappears with you.

In a world obsessed with speed, we choose to be deliberate. Important things deserve patience. 慢慢来，重要的事情慢慢来。

## How It's Different

| Feature          | Nostr | Scuttlebutt | Farcaster | AT Protocol | **Snail** |
|------------------|-------|-------------|-----------|-------------|-----------|
| No blockchain    | ✓     | ✓           | ✗         | ✗           | **✓**     |
| No token         | ✓     | ✓           | ✗         | ✗           | **✓**     |
| Data on device   | ✗     | ✓           | ✗         | ✗           | **✓**     |
| Offline=invisible| ✗     | ✗           | ✗         | ✗           | **✓**     |
| Revocable auth   | ✗     | ✗           | ✗         | ✗           | **✓**     |
| Content encrypted| opt.  | ✗           | ✗         | ✗           | **default**|

## Core Design Principles

- **Wallet = Identity**: Compatible with existing EVM wallets. No new token. No proprietary chain.
- **Radical Data Sovereignty**: Content exists only on your device by default. Offline means invisible.
- **Revocable Authorization**: You control who can see your data, and you can revoke access at any time.
- **Channel Separation of Powers**: Channel owners manage communities but cannot possess user content.
- **Action-Based Value Transfer**: Incentives are triggered by verifiable real actions, not passive views.
- **Account Relationship Protocol**: Defines OWNER / DELEGATE / GUARDIAN / PEER relationships — humans and AI treated identically.

## Quick Start

```bash
# Build
cargo build --release

# Generate a new identity
./target/release/snail-cli init

# Start a node
./target/release/snail-node --listen /ip4/0.0.0.0/tcp/9000

# Publish a post
./target/release/snail-cli post "Hello, decentralized world!" --tags "intro,first-post"

# Follow someone
./target/release/snail-cli follow <their-public-key> --name "Alice"

# Check your timeline
./target/release/snail-cli timeline
```

## Architecture

```
┌─────────────────────────────────────────────┐
│  Application Layer  — REST API + CLI        │
├─────────────────────────────────────────────┤
│  Node               — Orchestration         │
├─────────────────────────────────────────────┤
│  Channel Layer      — Communities + Access   │
├─────────────────────────────────────────────┤
│  Auth Layer         — Revocable key packages │
├─────────────────────────────────────────────┤
│  Visibility Layer   — public/private/auth    │
├─────────────────────────────────────────────┤
│  Content Layer      — Signed encrypted pkts  │
├─────────────────────────────────────────────┤
│  P2P Network Layer  — libp2p gossipsub+DHT   │
├─────────────────────────────────────────────┤
│  Storage Layer      — SQLite local store     │
├─────────────────────────────────────────────┤
│  Identity Layer     — EVM wallet = identity  │
├─────────────────────────────────────────────┤
│  Crypto Layer       — AES-256-GCM + secp256k1│
└─────────────────────────────────────────────┘
```

## Visibility Control

Every piece of content has an independent visibility state:

| State        | Description                                         |
|--------------|-----------------------------------------------------|
| `public`     | All online nodes can request and view               |
| `private`    | Local only — no external requests answered          |
| `authorized` | Only nodes on the authorization list can decrypt    |
| `timed`      | Auto-switches to public or private at a set time    |

When you go offline, your node stops responding. Your data becomes unreachable — not because of encryption alone, but because **it physically does not exist on the network**.

## Roadmap

| Phase              | Milestones                                                                 |
|--------------------|----------------------------------------------------------------------------|
| **MVP** (0-3 mo)   | Core protocol spec; wallet login + local wallet generation; P2P node discovery; basic posting + public distribution; community testing |
| **Alpha** (3-9 mo) | Encrypted storage + authorized sync; channel creation + gating; AI Agent identity registration; browser extension |
| **Beta** (9-18 mo) | Value transfer incentive mechanism; hosting node protocol; LAI standard interface; desktop client; third-party node access |
| **v1.0** (18+ mo)  | Protocol spec v1.0; AI Agent reputation system; commercial hosting node certification; developer ecosystem |

## Tech Stack

| Component     | Choice                          |
|---------------|---------------------------------|
| Language      | Rust                            |
| P2P Framework | libp2p (gossipsub + Kademlia DHT + mDNS) |
| Encryption    | AES-256-GCM + secp256k1         |
| Identity      | EVM-compatible wallets (BIP-39) |
| Local Storage | SQLite                          |
| Default Chain | Base (EVM L2, optional)         |

## Legal Position

Snail Protocol is an open communication protocol specification, equivalent in nature to HTTP or SMTP. The protocol itself does not issue any digital assets, does not operate any centralized services, and does not process any funds. Clients, hosting nodes, and distribution nodes built on Snail Protocol bear their own legal responsibilities independently.

## Contributing

We welcome contributions. Please read our [Contributing Guide](CONTRIBUTING.md) before submitting a pull request.

If you have questions, ideas, or want to discuss the protocol design, open an [Issue](https://github.com/snail-protocol/snail-protocol/issues) or start a [Discussion](https://github.com/snail-protocol/snail-protocol/discussions).

## Community

- GitHub: [github.com/snail-protocol](https://github.com/snail-protocol)
- Whitepaper: Coming soon

## License

[MIT](LICENSE) OR [Apache-2.0](LICENSE-APACHE)

---

*Snail Protocol — 我的数据我做主。慢慢来，重要的事情慢慢来。🐌*
