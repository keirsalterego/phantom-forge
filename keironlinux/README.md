# Keiron Linux

> *"The OS that doesn't trust the developer. Because Rust doesn't either."*

A bootable, memory-safe cybersecurity operating system built from scratch in Rust.

---

## What Is This?

**Keiron Linux** is a complete operating system — not a Linux kernel fork, not a custom GNU/Linux distro, not a toy kernel demo.

It is built from scratch:
- **Bootloader:** Rust UEFI bootloader (stage 1 + stage 2)
- **Kernel:** Rust kernel with no_std, no unsafe in production paths
- **Userspace:** musl-based, runit init, busybox coreutils
- **Tools:** 6 security tools (Keirox, Termino, SigMatrix, GhostPacket, MemoryHound, RedOps)
- **Package Manager:** KeironPkg (Rust, signed packages, SHA256 checksums)
- **Build System:** KeironISO — reproducible, GPG-signed ISOs

Every line of the kernel and userspace is written in Rust. Memory safety is enforced by the compiler, not the developer.

---

## Why This Exists

Because SnakeSec built tools and abandoned them. Because most hobby OS projects boot once and die. Because there is no production OS today with a Rust kernel that people can actually install and use.

Keiron Linux is the answer. It is built to be shipped, maintained, and trusted.

---

## The 6 Tools

Each ships independently on crates.io AND in the Keiron Linux ISO by default.

| Tool | What It Does | crates.io |
|------|-------------|-----------|
| **Keirox** | Red-team proxy (HTTP/SOCKS5, TLS MITM, domain fronting) | ✅ |
| **Termino** | Secure terminal mesh (Noise protocol, onion routing) | ✅ |
| **SigMatrix** | Detection rule engine (Sigma → SPL/EQL/regex) | ✅ |
| **GhostPacket** | Packet analysis (PCAP parsing, protocol dissectors) | ✅ |
| **MemoryHound** | Memory forensics (Windows dumps, process reconstruction) | ✅ |
| **RedOps** | Adversary emulation (Atomic Red Team, campaign planning) | ✅ |

---

## Documentation

| Document | Purpose |
|----------|---------|
| [architecture/OVERVIEW.md](./architecture/OVERVIEW.md) | Technical architecture, design philosophy, comparison |
| [org/STRUCTURE.md](./org/STRUCTURE.md) | GitHub org structure, 16 repos, maintainership model |
| [planning/FEATURES.md](./planning/FEATURES.md) | Full feature roadmap, phase-by-phase build plan |
| [marketing/MARKETING.md](./marketing/MARKETING.md) | Content strategy, community growth, press contacts |
| [installation/INSTALL.md](./installation/INSTALL.md) | Installation guide (USB, VM, disk, troubleshooting) |
| [community/COMMUNITY.md](./community/COMMUNITY.md) | Communication channels, contributor journey, governance |

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
| Website | keironlinux.org (under construction) |
| GitHub | github.com/keironlinux |
| Matrix | #keironlinux:libera.chat |
| Security issues | security@keironlinux.dev |

---

## License

Each repo is MIT unless otherwise specified. See individual repo LICENSE files.

---

*Keiron Linux is named after Keiron. This is your OS. Build it, ship it, maintain it.*