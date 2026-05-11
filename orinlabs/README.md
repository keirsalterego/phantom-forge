# Orin Labs

> *"The OS that doesn't trust the developer. Because Rust doesn't either."*

A research-grade cybersecurity operating system built as a Redox OS derivative.

---

## What Is This?

**Orin OS** is a complete operating system — a Redox OS derivative with a memory-safe core. Not a toy kernel demo, not a hobby project that boots once and dies.

It is built from scratch:
- **Kernel:** Vale — Rust kernel with no_std, no unsafe in production paths
- **Userspace:** musl-based, runit init, busybox coreutils
- **Tools:** 8 security/research tools (Drift, Trace, Halo, Veil, Slate, Haven, Atlas, Anvil)
- **Package Manager:** Loom (Rust, signed packages, SHA256 checksums)
- **Build System:** Anvil — reproducible, GPG-signed ISOs
- **SDK:** Atlas — cross-compilation and development kit

Every line of the kernel and userspace is written in Rust. Memory safety is enforced by the compiler, not the developer.

---

## Why This Exists

Because SnakeSec built tools and abandoned them. Because most hobby OS projects boot once and die. Because there is no research-grade OS today with a Rust foundation that people can actually install and use.

Orin Labs is the answer. We are building to be shipped, maintained, and trusted. Modeled after NouResearch — research-grade, not consumer-grade.

---

## The 8 Tools

Each ships independently on crates.io AND in the Orin OS ISO by default.

| Tool | What It Does | crates.io |
|------|-------------|-----------|
| **Drift** | Networking stack (TCP/IP, WireGuard, DNS) | ✅ |
| **Trace** | Packet analysis (PCAP parsing, protocol dissectors) | ✅ |
| **Halo** | Detection rule engine (Sigma → SPL/EQL/regex) | ✅ |
| **Veil** | EDR agent (endpoint detection & response) | ✅ |
| **Slate** | Window manager (Wayland compositor, Rust) | ✅ |
| **Haven** | Sandbox (gvisor-style, memory-safe) | ✅ |
| **Atlas** | SDK (cross-compilation, dev tools) | ✅ |
| **Anvil** | Build system (ISO builder, reproducible) | ✅ |

---

## Documentation

| Document | Purpose |
|----------|---------|
| [OVERVIEW.md](./OVERVIEW.md) | Technical architecture, design philosophy, comparison |
| [STRUCTURE.md](./STRUCTURE.md) | GitHub org structure, repos, maintainership model |
| [FEATURES.md](./FEATURES.md) | Full feature roadmap, phase-by-phase build plan |
| [MARKETING.md](./MARKETING.md) | Content strategy, community growth, press contacts |
| [INSTALL.md](./INSTALL.md) | Installation guide (USB, VM, disk, troubleshooting) |
| [COMMUNITY.md](./COMMUNITY.md) | Communication channels, contributor journey, governance |

---

## Status

Currently in Phase 0 (Planning). Full build starts Week 9 of the PHANTOM curriculum.

Current version: **v0.0.0 (pre-alpha)**

- [ ] Org created on GitHub
- [ ] Repos initialized
- [ ] First boot: target Week 14

---

## Quick Links

| Link | Where |
|------|-------|
| Website | orinlabs.dev (under construction) |
| GitHub | github.com/orinlabs |
| Matrix | #orinlabs:libera.chat |
| Security issues | security@orinlabs.dev |

---

## License

Each repo is MIT unless otherwise specified. See individual repo LICENSE files.

---

*Orin Labs — research-grade cybersecurity. Built to be shipped, maintained, and trusted.*