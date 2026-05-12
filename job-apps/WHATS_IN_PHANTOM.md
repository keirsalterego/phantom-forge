# What Is PHANTOM — Complete Breakdown

> Your 6-month elite accelerator for building Vyrox Security while mastering Rust, C++, Python, cybersecurity, and distributed systems. Status: **May 22, 2026 start date. You have not started yet.**

---

## The Core Goal

Build **Vyrox Security** (your AI-augmented SOC platform at vyrox.dev) while becoming a senior-level systems programmer and security engineer. The curriculum weaves language mastery, security fundamentals, open source contribution, and real-world projects together daily.

---

## What PHANTOM Contains

### 1. Language Mastery Curriculum (24 Weeks)

**Rust** — Zero to senior systems programmer
- Weeks 1–4: Ownership, borrowing, lifetimes, structs, enums, error handling, traits, generics
- Weeks 5–10: Async/await with Tokio, unsafe Rust, FFI, tokio networking, gRPC, custom allocators
- Weeks 11–16: Pin, Future, custom async executors, eBPF with aya-rs, WASM, zero-cost abstractions, MIR internals
- Senior techniques: Zero-copy parsing, SIMD with portable_simd, kernel programming, rustc contributions

**Python** — Zero to AI engineering and security scripting
- Weeks 1–4: Syntax, OOP, decorators, generators, context managers, type hints, dataclasses, packaging
- Weeks 5–10: AsyncIO, NumPy/pandas, SQLAlchemy, FastAPI, pydantic, observability
- Weeks 11–16: AST metaprogramming, Cython/Numba, multiprocessing, LangChain, Volatility3 plugins
- Senior techniques: C extensions, custom pytest plugins, bytecode manipulation, linters

**C++** — Zero to advanced systems programmer
- Weeks 1–4: Pointers, references, RAII, smart pointers, STL, move semantics
- Weeks 5–10: Templates, SFINAE, concepts C++20, inheritance, coroutines, concurrency, atomics
- Weeks 11–16: OS primitives, syscalls, kernel modules, custom allocators, SIMD, GDB, FFI
- Senior techniques: Template metaprogramming, game engine architecture, LLVM contributions

**Daily LeetCode rotation:**
- Mon/Wed/Fri: Rust hard problems
- Tue/Thu: Python medium/hard
- Sat: C++ problems
- Targets: 500 total (200 Rust, 200 Python, 100 C++)

---

### 2. Security Curriculum

**ATT&CK Case Studies** (one per 2-week block):
- SolarWinds/SUNBURST (T1195.002 Supply Chain)
- NotPetya (T1486, T1218 Wiper)
- APT31/ToolShell (T1566.001, T1574.002)
- Scattered Spider (T1621 MFA Bombing)
- APT41/Winnti (T1195, T1574.001)
- DarkSide/Colonial Pipeline (T1486, T1490)
- Lazarus/AppleJeus (T1195.001, T1204.001)
- Hafnium/ProxyLogon (T1190, T1505.003)
- UNC2452/SUNSPOT (T1554, T1195.002)
- Volt Typhoon + REvil/Kaseya (T1059, T1562, T1195)

Each case study produces: ATT&CK navigator layer, Sigma rule, detection hypothesis, write-up.

**OSS/Red Team Org Targets (30+):**
- Tier 1: Vyrox, Orin Labs, Drift, Sigma HQ, Zeek, Suricata, OSSEC, Snort
- Tier 2: Aya-rs, LibreSSL, RustCrypto, Ring, Rustls, OpenSSL
- Tier 3: Velociraptor, Volatility3, Capa, YARA
- Tier 4: Mythic C2, Havoc, Sliver, Caldera, Atomic Red Team
- Tier 5: Tokio, libp2p, Axum, Pingora, OpenTelemetry
- Tier 6: LangChain, Guardrails AI, OpenCTI, MISP

---

### 3. The 7 Core Projects

| # | Project | What It Is | Timeline |
|---|---------|-----------|----------|
| 1 | **Vyrox Security** | AI-augmented SOC platform — YOUR startup | Weeks 1–24 |
| 2 | **Orin Labs / Orin OS** | Bootable Rust OS (Redox derivative) with 8 security tools | Weeks 9–24 |
| 3 | **Drift** | Red-team proxy framework (HTTP/SOCKS5, TLS MITM) | Week 9+ |
| 4 | **Slate** | Secure terminal mesh (Noise protocol, onion routing) | Week 10+ |
| 5 | **Halo** | Detection rule engine (Sigma → SPL/EQL/regex) | Week 12+ |
| 6 | **Trace** | Packet analysis toolkit (PCAP, protocol dissectors) | Week 14+ |
| 7 | **Haven** | Memory forensics framework (Windows dump parsing) | Week 16+ |

Each tool must have: README, architecture doc, CI, tests (≥70% coverage), ≥1 crate on crates.io, ≥1 merged external PR before shipping in Orin OS.

---

### 4. Daily Structure (12-14 hours/day)

```
06:00–07:00   Morning study (reading / theory)
07:00–10:30   Deep build block 1
10:30–11:00   OSS contribution (30 min minimum)
11:00–13:00   Deep build block 2
13:00–14:00   Lunch + light reading
14:00–15:30   Learning block (books / labs)
15:30–17:00   Code quality block (review, refactor, tests)
17:00–17:30   Daily standup journal
```

**Non-negotiable daily rules:**
- At least 1 GitHub commit
- At least 1 journal entry
- At least 1 test written
- 30 min OSS contribution
- 30 min LeetCode (rotate languages)

---

### 5. Book List (50 Books)

**Rust (8 books):** The Rust Programming Language → Rust for Rustaceans → Programming Rust → Zero To Production → Rust in Action → The Rustonomicon → Async Rust

**Python (8 books):** Fluent Python → Python Cookbook → High Performance Python → Black Hat Python → Gray Hat Python → FastAPI Handbook → Building Python APIs

**C++ (8 books):** A Tour of C++ → C++ Primer → Effective Modern C++ → C++ Concurrency in Action → C++ High Performance → API Design for C++ → Game Engine Architecture → Optimizing C++

**Systems & Security (26 books):** Operating Systems: Three Easy Pieces → Linux Kernel Development → TCP/IP Illustrated → DDIA → Security Engineering → Zero Trust Networks → Practical Malware Analysis → The Art of Memory Forensics → Red Team Field Manual → and more.

---

### 6. Weekly Artifacts (Every Week, All 8 Required)

1. Reading notes (book + chapter + specific sections)
2. Lab task (build or break something concrete)
3. Code commit(s) with PR link
4. OSS contribution (target org + issue/PR)
5. Blog topic (title + 5-point outline)
6. Journal prompt reflection
7. ATT&CK mapping (technique + detection hypothesis)
8. Project tie-in (how this advances Vyrox/Orin Labs)

---

### 7. Graduation Criteria

- 15+ OSS PRs across 4+ organizations
- 3+ PRs merged into Vyrox
- 2+ PRs merged into Orin Labs
- 2+ PRs merged into standalone tools (Drift, Slate, Halo, Trace, Haven, Veil)
- 5+ external contributors merged across all projects
- Orin Labs: public ISO released (reproducible builds)
- 24 blog posts published
- 24 journal entries written
- ATT&CK navigator layers for all 10 case studies
- Vyrox: B2B deal progress with demo delivered

---

### 8. What You Have Right Now

| Folder | Contents | Status |
|--------|----------|--------|
| `daily/` | Empty — no daily files yet | Not started |
| `weekly/` | Empty — no weekly reports yet | Not started |
| `journal/` | Empty — no reflections yet | Not started |
| `blog-drafts/` | Empty — no drafts yet | Not started |
| `oss-journals/` | Empty — no audit notes yet | Not started |
| `labs/` | Empty — no lab notes yet | Not started |
| `attack-maps/` | Does not exist yet | Not started |
| `case-studies/` | Empty — no APT write-ups yet | Not started |
| `checkin-data.json` | Empty — 0 entries | Not started |
| `orinlabs/` | Docs only — no code yet | Planning phase |
| `index.html` | Heatmap tracker — built | Ready to use |
| `PHANTOM_Protocol_v3.md` | Full curriculum — written | Ready |

---

## The 3-Month Compressed Version

You're compressing this into 3 months:

| Month | Focus | Daily Hours |
|-------|-------|------------|
| 1 | Rust fundamentals + Python basics + Vyrox MVP | ~6-8 hrs |
| 2 | Rust intermediate/advanced + C++ intro + Detection mesh | ~8-10 hrs |
| 3 | Rust advanced + C++ intermediate/advanced + Vyrox $1M ARR push | ~10-12 hrs |

Orin Labs becomes hobby-only during these 3 months. Resume full-time Orin Labs after landing a job.

---

*PHANTOM — Built to ship. Built to last.*