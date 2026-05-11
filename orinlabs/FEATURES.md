# Orin Labs — Feature Roadmap

> *"We ship features when they're ready. Not before."*

---

## Phase 0 — Bootstrap (Weeks 9–10)

**Goal:** Set up the org, publish the plan, get the first repo ready.

### Repos Created

- `orinlabs/os` — main distro repo, ISO build skeleton
- `orinlabs/Vale` — Vale skeleton with QEMU boot test
- `orinlabs/bootloader` — UEFI stage 1 + stage 2 skeleton
- `orinlabs/keiron-docs` — documentation hub
- `drift-keiron` — first standalone tool repo
- `orinlabs/community` — issue templates, PR templates, Matrix channel

### Features

- [ ] GitHub org `orinlabs` created
- [ ] All 16 repos initialized (empty, documented)
- [ ] README.md on every repo with purpose and status
- [ ] GitHub Actions CI on Vale repo (QEMU boot test)
- [ ] orinlabs.dev website (single page: "Coming Soon")
- [ ] Matrix channel: `#orinlabs:libera.chat`
- [ ] GPG key generated for signing releases
- [ ] Drift repo scaffolded with Cargo + tests + CI

---

## Phase 1 — Kernel Core (Weeks 11–14)

**Goal:** The Vale boots. To a shell. In QEMU. That is the only goal.

### Week 11 — Bootloader

- [ ] Stage 1: UEFI application, parses FAT32 ESP, loads stage 2
- [ ] Stage 2: x86_64 long mode switch, page tables setup
- [ ] GRUB2 integration (optional, for dual-boot scenarios)
- [ ] QEMU boot test in CI (boots to Vale panic with "waiting for VFS")
- [ ] UEFI firmware test (OVMF in QEMU)

### Week 12 — Memory + IDT

- [ ] Physical memory allocator (buddy system)
- [ ] Virtual memory manager (page tables, 4-level)
- [ ] IDT setup (Rust, memory-safe, no unsafe in handler)
- [ ] APIC support (local APIC + IOAPIC)
- [ ] Basic IRQ handling (keyboard, timer)
- [ ] SMP support skeleton (multi-core boot protocol)

### Week 13 — VFS + Scheduler

- [ ] VFS abstraction layer
- [ ] ext2 driver (read-only initially)
- [ ] FAT32 driver (read-write, for ESP)
- [ ] Device file abstraction (/dev/null, /dev/zero, /dev/tty)
- [ ] Path resolution (absolute, relative, symlinks)
- [ ] Process scheduler (round-robin, preemptive)
- [ ] PID allocator

### Week 14 — First ISO

- [ ] Userland skeleton (musl-based, busybox)
- [ ] runit init system setup
- [ ] anvil build scripts functional
- [ ] ISO boots to shell in QEMU
- [ ] ISO boots on real hardware (test laptop #1)
- [ ] Nightly ISO CI pipeline working
- [ ] **Milestone: Orin Labs v0.1.0-alpha.1 released**

---

## Phase 2 — Userspace + Networking (Weeks 15–18)

**Goal:** A usable system. Network works. Tools compile and run.

### Week 15 — Core Utilities + Shell

- [ ] Custom Rust coreutils (ls, cat, ps, mkdir, rm, cp)
- [ ] sh (Alpine's busybox sh or mksh)
- [ ] Basic /etc structure (passwd, group, hostname)
- [ ] getty + login flow
- [ ] Keyboard layout support (US + EU)

### Week 16 — TCP/IP Stack

- [ ] IPv4 stack (DHCP, static IP)
- [ ] TCP + UDP sockets (Berkeley-like API)
- [ ] DNS resolver (gethostbyname)
- [ ] ping (ICMP)
- [ ] Network interface configuration
- [ ] nftables basic firewall (default deny)

### Week 17 — EDR Module

- [ ] Syscall hooking (seccomp-bpf)
- [ ] Process creation monitoring (audit via EDR hooks)
- [ ] Network connection tracking
- [ ] File write monitoring
- [ ] Ring buffer event log (safe Rust, no allocation in ISR)
- [ ] Event export format (JSON over Unix socket)

### Week 18 — Loom v1

- [ ] Package format definition (.kpkg)
- [ ] Package index (signed, SHA256)
- [ ] `loom install` — download, verify, extract
- [ ] `loom update` — refresh index
- [ ] `loom search` — query index
- [ ] `loom verify` — check GPG signature
- [ ] First 10 packages: bash, openssh, nmap, wireshark-cli, strace, gdb, vim, curl, wget, tcpdump
- [ ] **Milestone: Loom functional, 10 packages available**

---

## Phase 3 — Tools + Hardening (Weeks 19–22)

**Goal:** All 6 standalone tools ship. Security hardening is complete.

### Week 19 — Drift v1

- [ ] HTTP proxy (CONNECT method, MITM support)
- [ ] SOCKS5 proxy
- [ ] Domain fronting (Cloudflare, AWS, Azure)
- [ ] TLS inspection (self-signed CA, user-installed)
- [ ] Connection logging (JSON)
- [ ] Published to crates.io
- [ ] **Milestone: Drift v1.0.0 on crates.io + in ISO**

### Week 20 — Slate + Halo

**Slate:**
- [ ] Noise protocol handshake
- [ ] Onion routing (2-hop initially)
- [ ] Peer discovery (gossip protocol)
- [ ] Encrypted dead-drops
- [ ] Published to crates.io

**Halo:**
- [ ] Sigma rule parser (YAML → AST)
- [ ] Backend: Splunk SPL, Elastic EQL, plain regex
- [ ] YARA-style pattern matching
- [ ] Event correlation engine
- [ ] Published to crates.io

- [ ] **Milestone: Slate + Halo v1.0.0 on crates.io + in ISO**

### Week 21 — Trace + Haven

**Trace:**
- [ ] PCAP/PCAPNG parsing (pcap crate)
- [ ] TCP/UDP/HTTP/TLS/DNS dissectors
- [ ] Anomaly detection (threshold-based)
- [ ] Zeek-style log output (JSON)
- [ ] Published to crates.io

**Haven:**
- [ ] Windows memory dump parsing (raw, hibernation)
- [ ] Process reconstruction
- [ ] Malicious artifact detection (YARA integration)
- [ ] Plugin architecture (load .so / .dyl)
- [ ] Published to crates.io

- [ ] **Milestone: Trace + Haven v1.0.0 on crates.io + in ISO**

### Week 22 — Veil + Hardening

**Veil:**
- [ ] Atomic Red Team YAML integration
- [ ] Attack planning (sequence executor)
- [ ] Campaign reporting (JSON + HTML)
- [ ] Detection gap analysis
- [ ] Published to crates.io

**Security Hardening:**
- [ ] KASLR enabled (Vale base randomized)
- [ ] SMEP + SMAP enabled
- [ ] W^X enforcement (no writable code pages)
- [ ] AppArmor profiles on all daemons
- [ ] Kernel lockdown module
- [ ] kptr_restrict enabled
- [ ] UEFI Secure Boot (signed GRUB + Vale)
- [ ] Audit daemon (auditd) running

- [ ] **Milestone: All 6 tools v1.0.0 shipped. Orin Labs v0.2.0-beta**

---

## Phase 4 — SDK + Docs + Community (Weeks 23–24)

**Goal:** Make it easy to use, easy to contribute, easy to trust.

### Week 23 — Atlas SDK

- [ ] cargo-atlas target (x86_64-keiron-linux-gnu)
- [ ] Sysroot generation (musl-based)
- [ ] Cross-compilation guide (i686, aarch64)
- [ ] SDK documentation (ARCHITECTURE.md in atlas repo)
- [ ] First external package: python3 (via musl cross-compile)

### Week 24 — Documentation + First Public Release

**Documentation (keiron-docs repo):**
- [ ] Installation guide (USB, VM, bare metal)
- [ ] Hardening guide (CIS-level step-by-step)
- [ ] Package development guide (how to package for Loom)
- [ ] Architecture overview (Mermaid diagrams)
- [ ] Contributing guide
- [ ] Security policy
- [ ] Upgrade path guide
- [ ] FAQ (50 questions)

**Community:**
- [ ] orinlabs.dev fully functional (website, blog, docs)
- [ ] Alternative distrowatch.com submission
- [ ] Hacker News "Show HN" post
- [ ] /r/linux post (organic)
- [ ] 3+ confirmed real-hardware testers
- [ ] First merged external PR (any repo)
- [ ] Blog post about the build process (from external contributor)

**ISO:**
- [ ] Production ISO build (reproducible verified)
- [ ] SHA256 hash published
- [ ] GPG signature published
- [ ] Release notes written

- [ ] **Milestone: Orin Labs v1.0.0 — First Public Release**
- [ ] **Milestone: 5+ external contributors merged across all repos**

---

## Post-Launch: Lifecycle

After v1.0.0, the cadence shifts:

### Monthly (every 4 weeks)
- Patch releases (bug fixes, security fixes)
- New packages in Loom index
- CI improvements

### Every 6 months
- Minor release (new Vale features, new tools, updated packages)
- Kernel bump (new Rust nightly + updated dependencies)
- Release notes with full changelog

### Yearly
- Major release (architectural changes, new architectures)

### Ongoing
- Security advisories within 72h of confirmed CVE
- 30-day private disclosure window before public CVE
- Community growth: maintainer recruitment, issue triage, PR reviews

---

## Deferred / Stretch Goals

These are not blocking v1.0.0. They ship when they're ready.

| Feature | Priority | Complexity | Notes |
|---------|----------|-----------|-------|
| aarch64 support | High | Medium | Raspberry Pi 4, Apple Silicon |
| ZFS driver | Medium | High | For users wanting ZFS root |
| Secure boot chain (tianocore) | Medium | High | Full UEFI secure boot |
| Python 3 in Loom | High | Low | Via musl cross-compile |
| Container support (runc) | Low | High | After Vale is stable |
| Full-disk encryption (LUKS) | Medium | High | dm-crypt integration |
| Wireless support (iwlwifi, rtw88) | Medium | High | WiFi in live ISO |
| Haskell/Golang toolchain | Low | Medium | For advanced users |

---

*Last updated: May 2026*
*Feature version: 1.0*