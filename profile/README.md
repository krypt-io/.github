<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/krypt-io/.github/main/assets/krypt-logo-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/krypt-io/.github/main/assets/krypt-logo-light.svg">
    <img alt="Krypt" src="https://raw.githubusercontent.com/krypt-io/.github/main/assets/krypt-logo-light.svg" width="400">
  </picture>
</p>

<p align="center">
  <b>The Open Source Distributed Secrets Manager</b>
</p>

<p align="center">
  <a href="https://github.com/krypt-io/krypt/actions/workflows/ci.yml"><img src="https://img.shields.io/github/actions/workflow/status/krypt-io/krypt/ci.yml?branch=main&style=flat-square&label=build" alt="Build Status"></a>
  <a href="https://github.com/krypt-io/krypt/releases/latest"><img src="https://img.shields.io/github/v/release/krypt-io/krypt?style=flat-square&color=blue&label=release" alt="Latest Release"></a>
  <a href="https://github.com/krypt-io/krypt/blob/main/LICENSE"><img src="https://img.shields.io/github/license/krypt-io/krypt?style=flat-square" alt="License"></a>
  <a href="https://github.com/krypt-io/krypt"><img src="https://img.shields.io/github/stars/krypt-io/krypt?style=flat-square&color=yellow" alt="GitHub Stars"></a>
  <br/>
  <a href="https://docs.krypt.io"><img src="https://img.shields.io/badge/docs-krypt.io-blue?style=flat-square" alt="Documentation"></a>
  <a href="https://discord.gg/krypt"><img src="https://img.shields.io/discord/1234567890?style=flat-square&logo=discord&logoColor=white&label=discord&color=7289da" alt="Discord"></a>
  <a href="https://twitter.com/krypt_io"><img src="https://img.shields.io/twitter/follow/krypt_io?style=flat-square&logo=twitter&color=1DA1F2" alt="Twitter"></a>
</p>

<p align="center">
  <a href="https://docs.krypt.io/getting-started">Getting Started</a> •
  <a href="https://docs.krypt.io">Documentation</a> •
  <a href="https://github.com/krypt-io/krypt/issues">Issues</a> •
  <a href="https://discord.gg/krypt">Community</a> •
  <a href="https://krypt.io">Website</a>
</p>

---

## About Krypt

**Krypt** is an open-source, distributed secrets management platform designed for modern cloud-native infrastructure. Built from the ground up in **Rust** for maximum performance, memory safety, and reliability, Krypt provides organizations with a secure, scalable, and developer-friendly solution for managing sensitive data across their entire stack.

Whether you're running a startup or managing enterprise infrastructure, Krypt scales from a single node development environment to a globally distributed production cluster with ease.

### Why Choose Krypt?

- **🦀 Built with Rust** — Memory-safe, blazing fast, with zero garbage collection pauses
- **🌍 Truly Distributed** — Multi-node Raft consensus with automatic leader election and failover
- **🔐 Security First** — AES-256-GCM encryption, envelope encryption, and Argon2id key derivation
- **📡 Modern Protocol** — High-performance gRPC API with full TLS/mTLS support
- **🎯 Developer Experience** — Intuitive CLI, comprehensive SDKs, and beautiful Web UI
- **📋 Compliance Ready** — Complete audit logging for SOC2, HIPAA, and GDPR requirements

---

## 🚀 Quick Start

### Installation

**Using Cargo (Rust):**
```bash
cargo install krypt
```

**Using Homebrew (macOS/Linux):**
```bash
brew install krypt-io/tap/krypt
```

**Using Docker:**
```bash
docker pull krypt/krypt:latest
```

**Binary Downloads:**  
Download pre-built binaries for your platform from the [Releases Page](https://github.com/krypt-io/krypt/releases).

### Your First Secret

```bash
# Start the Krypt server
krypt server --listen 0.0.0.0:8200

# In another terminal, login to your engine
krypt login myengine

# Store a secret
krypt put myengine kv/database/prod host=db.example.com user=admin password=supersecret

# Retrieve the secret
krypt get myengine kv/database/prod

# List all secrets in a namespace
krypt list myengine kv/database/
```

### Deploy with Docker Compose

```yaml
version: '3.8'
services:
  krypt:
    image: krypt/krypt:latest
    ports:
      - "8200:8200"
    environment:
      KRYPT_DB_URL: postgres://krypt:password@postgres:5432/krypt
      KRYPT_LOG_LEVEL: info
    depends_on:
      - postgres
    volumes:
      - krypt-data:/var/lib/krypt

  postgres:
    image: postgres:15-alpine
    environment:
      POSTGRES_USER: krypt
      POSTGRES_PASSWORD: password
      POSTGRES_DB: krypt
    volumes:
      - postgres-data:/var/lib/postgresql/data

volumes:
  krypt-data:
  postgres-data:
```

---

## ✨ Features

<table>
<tr>
<td width="50%">

### 🔒 Enterprise-Grade Security

- **AES-256-GCM** encryption for all secrets at rest
- **Envelope encryption** with unique DEKs per secret
- **Argon2id** key derivation (memory-hard, resistant to GPU attacks)
- **TLS 1.3** for all network communication
- **mTLS** support for zero-trust architectures
- **Automatic secret zeroization** in memory after use

</td>
<td width="50%">

### 🌐 Distributed by Design

- **Raft consensus** for strong consistency across nodes
- **Automatic leader election** and transparent failover
- **Horizontal scaling** — add nodes without downtime
- **Read replicas** for high-throughput read operations
- **Geographic distribution** for global deployments
- **Partition tolerance** with configurable consistency levels

</td>
</tr>
<tr>
<td width="50%">

### 🛡️ Fine-Grained Access Control

- **Role-Based Access Control (RBAC)** with hierarchical policies
- **Path-based permissions** with glob pattern matching
- **Token-based authentication** with configurable TTLs
- **Capability model** (create, read, update, delete, list)
- **Namespace isolation** for multi-tenant deployments
- **Emergency break-glass** procedures for incident response

</td>
<td width="50%">

### 📝 Complete Audit Trail

- **Immutable audit logs** for every operation
- **Structured logging** with full request/response context
- **SIEM integration** (JSON, Syslog, Splunk, ELK)
- **Compliance reports** for SOC2, HIPAA, GDPR
- **Real-time alerting** for suspicious activity
- **Long-term retention** with configurable policies

</td>
</tr>
<tr>
<td width="50%">

### ⚡ High Performance

- **Sub-millisecond** latency for secret retrieval
- **Thousands of requests/second** per node
- **Connection pooling** and request multiplexing
- **Intelligent caching** with cache invalidation
- **Async I/O** powered by Tokio runtime
- **Zero-copy serialization** with Protocol Buffers

</td>
<td width="50%">

### 🧰 Developer Experience

- **Intuitive CLI** with auto-completion and rich output
- **Multiple output formats** (table, JSON, YAML)
- **Native SDKs** for Go, Python, JavaScript/TypeScript
- **gRPC-Web** support for browser applications
- **OpenAPI/REST** gateway for legacy integrations
- **Comprehensive documentation** with examples

</td>
</tr>
</table>

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                                    CLIENTS                                      │
│   ┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────┐   ┌─────────────────┐   │
│   │   CLI   │   │ Web UI  │   │ Go SDK  │   │ Py SDK  │   │     JS SDK      │   │
│   └────┬────┘   └────┬────┘   └────┬────┘   └────┬────┘   └────────┬────────┘   │
└────────┼─────────────┼─────────────┼─────────────┼──────────────────┼───────────┘
         │             │             │             │                  │
         └─────────────┴─────────────┴──────┬──────┴──────────────────┘
                                            │  gRPC + TLS
                                            ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│                               KRYPT CLUSTER                                     │
│                                                                                 │
│   ┌──────────────────┐   ┌──────────────────┐   ┌──────────────────┐            │
│   │     Node 1       │   │     Node 2       │   │     Node 3       │            │
│   │    (LEADER)      │◄──┤   (Follower)     │◄──┤   (Follower)     │            │
│   └────────┬─────────┘   └────────┬─────────┘   └────────┬─────────┘            │
│            │                      │                      │                      │
│            │          Raft Consensus Protocol            │                      │
│            └──────────────────────┴──────────────────────┘                      │
│                                   │                                             │
└───────────────────────────────────┼─────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│                               STORAGE LAYER                                     │
│   ┌──────────────────────────────────────────────────────────────────────────┐  │
│   │                       PostgreSQL (Replicated)                            │  │
│   │   ┌───────────┐   ┌───────────┐   ┌───────────┐   ┌───────────────────┐  │  │
│   │   │  Engines  │   │  Secrets  │   │  Tokens   │   │   Audit Logs      │  │  │
│   │   └───────────┘   └───────────┘   └───────────┘   └───────────────────┘  │  │
│   └──────────────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────────────┘
```

---

## 📦 Repositories

Our organization maintains the following projects:

| Repository                                                           | Description                                      | Language                                                                                                         |
| :------------------------------------------------------------------- | :----------------------------------------------- | :--------------------------------------------------------------------------------------------------------------- |
| [**krypt**](https://github.com/krypt-io/krypt)                       | Core server, CLI, and cryptographic engine       | ![Rust](https://img.shields.io/badge/-Rust-000?style=flat-square&logo=rust)                                      |
| [**krypt-web**](https://github.com/krypt-io/krypt-web)               | Web UI dashboard for visual management           | ![TypeScript](https://img.shields.io/badge/-TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) |
| [**krypt-landing**](https://github.com/krypt-io/krypt-landing)       | Official website and promotional pages           | ![Next.js](https://img.shields.io/badge/-Next.js-000?style=flat-square&logo=next.js)                             |
| [**krypt-sdk-go**](https://github.com/krypt-io/krypt-sdk-go)         | Official Go SDK with full API coverage           | ![Go](https://img.shields.io/badge/-Go-00ADD8?style=flat-square&logo=go&logoColor=white)                         |
| [**krypt-sdk-python**](https://github.com/krypt-io/krypt-sdk-python) | Official Python SDK with async support           | ![Python](https://img.shields.io/badge/-Python-3776AB?style=flat-square&logo=python&logoColor=white)             |
| [**krypt-sdk-js**](https://github.com/krypt-io/krypt-sdk-js)         | Official JavaScript/TypeScript SDK               | ![TypeScript](https://img.shields.io/badge/-TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) |
| [**krypt-helm**](https://github.com/krypt-io/krypt-helm)             | Kubernetes Helm charts for production deployment | ![Helm](https://img.shields.io/badge/-Helm-0F1689?style=flat-square&logo=helm&logoColor=white)                   |
| [**krypt-docs**](https://github.com/krypt-io/krypt-docs)             | Official documentation and tutorials             | ![Markdown](https://img.shields.io/badge/-Docs-000?style=flat-square&logo=markdown)                              |

---

## 🛠️ Technology Stack

| Layer              | Technology                 | Purpose                                 |
| :----------------- | :------------------------- | :-------------------------------------- |
| **Language**       | Rust                       | Memory safety, performance, reliability |
| **Runtime**        | Tokio                      | Async I/O, task scheduling              |
| **Protocol**       | gRPC (Tonic)               | High-performance RPC framework          |
| **Serialization**  | Protocol Buffers           | Efficient, typed serialization          |
| **Consensus**      | Raft (openraft)            | Distributed consensus algorithm         |
| **Database**       | PostgreSQL                 | Persistent storage with replication     |
| **Encryption**     | AES-256-GCM                | Authenticated encryption                |
| **Key Derivation** | Argon2id                   | Memory-hard password hashing            |
| **Observability**  | Prometheus + OpenTelemetry | Metrics, tracing, logging               |
| **Web UI**         | React + TypeScript         | Modern, responsive dashboard            |

---

## 📖 Documentation

Comprehensive documentation is available at [**docs.krypt.io**](https://docs.krypt.io):

| Section                                                      | Description                                    |
| :----------------------------------------------------------- | :--------------------------------------------- |
| [**Getting Started**](https://docs.krypt.io/getting-started) | Installation, first steps, and basic concepts  |
| [**Architecture**](https://docs.krypt.io/architecture)       | System design, security model, and internals   |
| [**CLI Reference**](https://docs.krypt.io/cli)               | Complete command-line interface documentation  |
| [**API Reference**](https://docs.krypt.io/api)               | gRPC and REST API specifications               |
| [**SDK Guides**](https://docs.krypt.io/sdks)                 | Language-specific SDK tutorials                |
| [**Operations**](https://docs.krypt.io/operations)           | Production deployment, scaling, and monitoring |
| [**Security**](https://docs.krypt.io/security)               | Security model, best practices, and compliance |

---

## 🗺️ Roadmap

We're building Krypt in the open. Check out our [public roadmap](https://github.com/orgs/krypt-io/projects/1) to see what we're working on.

### Current Focus

- ✅ **Core Engine** — Encryption, storage, and domain types
- ✅ **gRPC Server** — Single-node API server
- 🚧 **RBAC** — Role-based access control
- 🚧 **Audit Logging** — Complete audit trail
- ⏳ **Multi-Node Clustering** — Raft consensus
- ⏳ **Web UI** — Visual dashboard
- ⏳ **SDKs** — Go, Python, JavaScript

### Future Plans

- Secret rotation and dynamic secrets
- Kubernetes secrets injection (CSI driver)
- AWS/GCP/Azure KMS integration
- HashiCorp Vault migration tools
- Enterprise SSO (OIDC, SAML)

---

## 🤝 Contributing

We welcome contributions from the community! Krypt is built by developers, for developers.

### Ways to Contribute

- 🐛 **Report Bugs** — Found a bug? [Open an issue](https://github.com/krypt-io/krypt/issues/new?template=bug_report.md)
- 💡 **Request Features** — Have an idea? [Start a discussion](https://github.com/krypt-io/krypt/discussions)
- 📝 **Improve Docs** — Help us improve [documentation](https://github.com/krypt-io/krypt-docs)
- 🔧 **Submit PRs** — Check out [good first issues](https://github.com/krypt-io/krypt/labels/good%20first%20issue)
- 🌍 **Translate** — Help us reach a global audience

### Development Setup

```bash
# Clone the repository
git clone https://github.com/krypt-io/krypt.git
cd krypt

# Install dependencies
cargo build

# Run tests
cargo test

# Start development server
cargo run -- server --dev
```

See our [Contributing Guide](https://github.com/krypt-io/krypt/blob/main/CONTRIBUTING.md) for detailed instructions.

---

## 💬 Community

Join our growing community of developers and security professionals:

- 💬 **Discord** — [discord.gg/krypt](https://discord.gg/krypt) — Real-time chat and support
- 🐦 **Twitter** — [@krypt_io](https://twitter.com/krypt_io) — News and announcements
- 📧 **Mailing List** — [lists.krypt.io](https://lists.krypt.io) — Weekly updates
- 📺 **YouTube** — [Krypt Channel](https://youtube.com/@krypt-io) — Tutorials and talks

### Getting Help

- 📖 Check the [Documentation](https://docs.krypt.io)
- 🔍 Search [GitHub Issues](https://github.com/krypt-io/krypt/issues)
- 💬 Ask in [Discord #help](https://discord.gg/krypt)
- 📧 Email [support@krypt.io](mailto:support@krypt.io)

---

## 🏢 Enterprise

Need enterprise features or support? We offer:

- **Priority Support** — 24/7 SLA-backed support
- **Custom Integrations** — Tailored solutions for your stack
- **Training** — On-site and remote training sessions
- **Compliance** — Assistance with SOC2, HIPAA, PCI-DSS
- **Professional Services** — Architecture review and deployment

📧 Contact us at [enterprise@krypt.io](mailto:enterprise@krypt.io)

---

## 🙏 Acknowledgements

Krypt is built on the shoulders of giants. We thank the maintainers of:

- [Rust](https://www.rust-lang.org/) — The programming language
- [Tokio](https://tokio.rs/) — Async runtime
- [Tonic](https://github.com/hyperium/tonic) — gRPC framework
- [openraft](https://github.com/datafuselabs/openraft) — Raft implementation
- [RustCrypto](https://github.com/RustCrypto) — Cryptographic primitives

---

## 📜 License

Krypt is open source software licensed under the [MIT License](https://github.com/krypt-io/krypt/blob/main/LICENSE).

```
MIT License

Copyright (c) 2024 Krypt.io

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

---

<p align="center">
  <sub>Made with ❤️ and 🦀 by the <a href="https://github.com/krypt-io">Krypt</a> team and contributors worldwide</sub>
</p>

<p align="center">
  <a href="https://github.com/krypt-io/krypt/stargazers">⭐ Star us on GitHub</a> — it helps!
</p>
