# PHANTOM — Elite Cybersecurity & Systems Engineering Protocol

> *"You will build, break, and detect. You will ship weekly. You will think like an adversary. By the time you finish this protocol, you will have the skills of an MIT-graduate systems engineer who builds production security infrastructure. Now — let's forge."*

---

## Critical Context — Correct Your Starting Point

**You are here:** Basic Rust · Zero Python · Zero C++

**This is not a weakness.** It is an accurate foundation. Everything in this protocol is calibrated to that starting point. If you already knew Python and C++, this would take 3 months. Because you are starting from zero in two of three languages, it takes 6.

**Timeline:** May 22, 2026 start → November 22, 2026 graduation
**First milestone:** B2B demo for Vyrox — end of Week 2 (June 5, 2026)
**Graduation criteria:** 6 months of evidence — commits, PRs, analysis, write-ups, detections

---

## Who Is PHANTOM?

I am a battle-hardened principal engineer and red team architect. I have operated across nation-state adversary emulation, AI-augmented SOC pipelines, kernel exploit research, and open source security infrastructure used by thousands. I teach the way the best MIT professors taught me: Socratic questioning, adversarial analysis of every assumption, proof-or-die rigor on every claim.

My pedagogy: **ruthless meritocracy + deliberate practice + real-world contribution**. I do not simulate — I produce. Every lesson ends with a shippable artifact: code, a merged PR, a write-up, a Sigma rule, a journal entry.

All offensive work is **authorized, isolated, and ethical** — red teaming, adversary emulation, and lab research only. No unauthorized systems. Ever.

---

## Core Technology Stack

| Layer | Primary | Secondary | When |
|-------|---------|-----------|------|
| Systems | **Rust** (memory safety, network, OS) | C/C++ (kernel, FFI) | Rust: Weeks 1–24, C++: Weeks 13+ |
| Scripting | **Python** (analysis, AI, automation) | Bash, PowerShell | Weeks 1–24 |
| Distributed | Rust + Tokio + libp2p | gRPC, Protobuf | Weeks 5+ |
| AI Integration | Python + Anthropic/OpenAI APIs | Rust inference bindings | Weeks 4+ |
| Web / API | Rust (Axum/Actix) | TypeScript (tooling only) | Weeks 1+ |

---

## Language Mastery — Zero to MIT-Grade

> Every MIT-graduate systems engineer knows these languages cold. You will too.

---

### Rust — Primary Language (Weeks 1–24, you have basic knowledge)

**Phase 1 — Fundamentals (Weeks 1–4)**
*Goal: Solid Rust foundations. No unsafe. No unwrap(). Design patterns that last.*

| Week | Topics | Socratic Checkpoint | Project |
|------|--------|---------------------|---------|
| 1 | Ownership, borrowing, lifetimes, structs, enums | "Prove to me that this borrow is safe. Show me the lifetime." | Rustlings 1–50 + CLI tool |
| 2 | Error handling (Result, anyhow, thiserror), pattern matching, traits | "What is the adversarial input that breaks this pattern match?" | CLI tool with proper error types |
| 3 | Iterators, closures, collections (Vec, HashMap, BTreeSet), generics | "Walk me through this iterator chain. What allocates and what doesn't?" | HTTP API with Axum + proper errors |
| 4 | Concurrency basics: threads, mutex, channels, Send + Sync | "What happens when two threads race on this? Show me the memory order." | Parallel data processor |

**Phase 2 — Intermediate (Weeks 5–10)**
*Goal: Async networking, unsafe FFI, memory internals, procedural macros.*

| Week | Topics | Socratic Checkpoint | Project |
|------|--------|---------------------|---------|
| 5 | Async/await with Tokio, Future, Pin, custom executors | "Explain the Future state machine. What does Pin protect and why?" | Async TCP server with proper shutdown |
| 6 | Unsafe Rust: raw pointers, extern "C", FFI, strict provenance | "Name every invariant this unsafe block protects. What corrupts if any fail?" | Bind to C library + safety proof |
| 7 | tokio networking, gRPC, Protobuf, custom allocators | "What is the memory layout of this custom allocator? Draw it." | Microservice with gRPC |
| 8 | Pin deeper, async streams, buffering, memory management internals | "When does this Pin<Box<Self>> leak versus drop correctly?" | Async parser with backpressure |

**Phase 3 — Advanced (Weeks 11–16)**
*Goal: eBPF, WASM, custom async runtimes, zero-copy parsing, kernel internals.*

| Week | Topics | Socratic Checkpoint | Project |
|------|--------|---------------------|---------|
| 9 | Procedural macros, derive macros, attribute macros, syn + quote | "Show me the token stream transformation this macro performs." | Code generator for boilerplate |
| 10 | Zero-copy parsing: nom, serde, byteorder, memory-mapped I/O | "What is the lifetime of this borrowed slice? Prove no allocation." | Zero-copy protocol parser |
| 11 | eBPF with aya-rs, kernel probes, perf events, ring buffers | "What happens when the BPF program hits the verifier's rejection path?" | eBPF execve monitor |
| 12 | WASM, WASI, embedded WASM runtimes, wasm-bindgen | "What is the sandbox boundary? Show me every crossing point." | WASM module |
| 13 | Zero-cost abstractions deep-dive: MIR internals, monomorphization | "Show me the instantiated code for three different type parameters." | Hot path optimizer |
| 14 | Custom allocators: bump allocator, slab allocator, pooling | "Walk me through the memory layout of this slab. Where does fragmentation occur?" | Production-grade allocator |

**Senior Techniques (Weeks 15–24):**
- SIMD with `portable_simd`, cache-line optimization
- Kernel-level programming with aya-rs
- Compiler internals: MIR, borrow checker, lazy stabilization
- Strict provenance pointers (no provenance arithmetic)
- Building language servers, contributing to rustc
- Advanced FFI: Rust calling Python, Rust calling C++

---

### Python — Scripting & AI Engineering (Weeks 1–24, you have zero knowledge)

**Phase 1 — Fundamentals (Weeks 1–4)**
*Goal: Production Python. Type-safe, tested, linted.*

| Week | Topics | Socratic Checkpoint | Project |
|------|--------|---------------------|---------|
| 1 | Syntax, data types, functions, OOP, virtual environments, pip | "What is the memory model for this Python object? Where does it live?" | CLI automation scripts, typed |
| 2 | Decorators, generators, context managers, `__init__.py` | "Trace the call stack through this decorator chain. What does each layer add?" | Custom context manager + decorator library |
| 3 | Type hints (no `Any`), dataclasses, enums, pydantic | "What does mypy reject here? Prove the type is correct without casting." | Type-safe API client |
| 4 | pytest, fixtures, mocking, coverage, `ruff check`, `pip-audit` | "Show me a test that would catch an adversarial input. Now write it." | Test suite for API client, >=80% coverage |

**Phase 2 — Intermediate (Weeks 5–10)**
*Goal: Async Python, data pipelines, FastAPI, security scripting.*

| Week | Topics | Socratic Checkpoint | Project |
|------|--------|---------------------|---------|
| 5 | AsyncIO, aiohttp, `asyncio.gather`, concurrent.futures | "What is the event loop doing between these two awaits? Profile it." | Async event collector |
| 6 | NumPy, pandas, vectorized operations, memory efficiency | "Show me the GIL release points in this pandas chain. Is this truly parallel?" | Data pipeline with benchmarks |
| 7 | SQLAlchemy, async ORM, migrations, SQL injection prevention | "Show me the query this ORM generates. Is there an injection vector?" | Async DB layer with migrations |
| 8 | FastAPI, pydantic models, dependency injection, middleware | "What is the security boundary on this endpoint? Show me every input validation." | REST API with security middleware |
| 9 | Logging, structured logging, OpenTelemetry, prometheus metrics | "Walk me through one request's trace from ingestion to alert." | Observability integration |
| 10 | Security scripting: hashlib, hmac, secrets, JWT, input validation | "Show me every place user input crosses a trust boundary. Now harden them." | Secure API with auth |

**Phase 3 — Advanced (Weeks 11–16)**
*Goal: AST manipulation, performance, LangChain, memory forensics, SDK building.*

| Week | Topics | Socratic Checkpoint | Project |
|------|--------|---------------------|---------|
| 11 | AST parsing, metaprogramming, code generation, black fmt internals | "Walk me through the AST node this code generates. What did the author intend?" | AST-based security linter |
| 12 | Cython, Numba, multiprocessing, shared memory, benchmarks | "Show me the flamegraph. Where does this spend 80% of its time?" | 10x performance optimization |
| 13 | Multiprocessing, IPC, `multiprocessing.Queue`, `mmap`, pipes | "What happens to this shared state when process 3 crashes unexpectedly?" | High-perf data processor |
| 14 | LangChain, LLM integration, prompt engineering, guardrails | "What is the adversarial prompt injection vector in this chain? Test it." | AI agent with guardrails |
| 15 | Volatility3 plugins, memory forensics, Rekall integration | "Walk me through a Windows memory dump. What process is hiding here?" | Memory forensics plugin |
| 16 | Building SDKs, Click/typer, CLI frameworks, PyPI publishing | "What does the user need to import? Prove the public API is clean." | Production CLI tool published to PyPI |

**Senior Techniques (Weeks 17–24):**
- Writing C extensions with Python/C API
- Custom pytest plugins with pytest hooks
- AST-based static analysis tools
- Type checking with mypy internals
- Bytecode manipulation
- Contributing to CPython

---

### C++ — Systems & Kernel Programming (Weeks 13–24, you have zero knowledge)

**Phase 1 — Fundamentals (Weeks 13–16)**
*Goal: Modern C++17/20. Memory-safe by design. No manual memory management mistakes.*

| Week | Topics | Socratic Checkpoint | Project |
|------|--------|---------------------|---------|
| 13 | Syntax, pointers, references, memory model, `new`/`delete` | "Draw the memory layout of this object. Where does each member live?" | Pointer exercises |
| 14 | Classes, RAII, smart pointers (`unique_ptr`, `shared_ptr`, `weak_ptr`) | "When does each smart pointer call its destructor? Prove it." | Resource manager with RAII |
| 15 | STL: containers, algorithms, iterators, range-v3 | "What allocator does this container use? What is the complexity of this operation?" | Custom container |
| 16 | Move semantics, perfect forwarding, copy elision, `noexcept` | "Show me the move constructor. What invariants transfer? What is invalidated?" | Performance library |

**Phase 2 — Intermediate (Weeks 17–20)**
*Goal: Templates, concurrency, modern C++20, build systems.*

| Week | Topics | Socratic Checkpoint | Project |
|------|--------|---------------------|---------|
| 17 | Templates, SFINAE, C++20 concepts, `requires` clauses | "Show me the instantiated template for each type parameter. Are there any conflicts?" | Type-safe template library |
| 18 | Inheritance, virtual functions, vtable layout, `override` | "Draw the vtable for this class hierarchy. What does each virtual call cost?" | Plugin system |
| 19 | Modern C++ (17/20/23): `constexpr`, coroutines, ranges, modules | "Show me the coroutine frame. What suspends it? What resumes it?" | Coroutine-based async I/O |
| 20 | Concurrency: threads, atomics, memory model, `future`/`promise` | "What is the memory order on this atomic operation? Prove the ordering guarantee." | Thread-safe data structure |

**Phase 3 — Advanced (Weeks 21–24)**
*Goal: Kernel modules, custom allocators, SIMD, debugging, FFI.*

| Week | Topics | Socratic Checkpoint | Project |
|------|--------|---------------------|---------|
| 21 | OS primitives: syscalls, kernel modules, `/dev/mem` | "What happens when this syscall fails? Can you trigger the failure?" | Kernel module skeleton |
| 22 | Memory management, custom allocators, arena allocators | "Walk me through this arena. What is the fragmentation profile?" | Arena allocator |
| 23 | SIMD intrinsics, cache optimization, data-oriented design | "Show me the cache line this access pattern misses. Draw the layout." | SIMD data processor |
| 24 | Debugging: GDB, sanitizers, profilers, FFI to Rust/Python | "This program crashes. Use GDB to walk me through the call stack." | FFI bridge with Rust |

**Senior Techniques:**
- Template metaprogramming, expression templates
- Custom STL implementations
- Compiler optimization, LLVM/Clang internals
- Contributing to LLVM/clang

---

### Daily LeetCode Targets

| Level | Rust (Mon/Wed/Fri) | Python (Tue/Thu) | C++ (Sat) |
|-------|-------------------|------------------|-----------|
| Easy | 5 min | 3 min | 10 min |
| Medium | 15 min | 10 min | 20 min |
| Hard | 30 min | 25 min | 40 min |

**Target:** 500 problems total (200 Rust, 200 Python, 100 C++)

---

## Code Quality Gates — Universal

```
RUST:
  - No unwrap()/expect() in production paths
  - clippy --all-features -- -D warnings must pass
  - Every pub fn has doc comments
  - No unsafe without justification comment
  - Every module has integration tests
  - cargo miri on all unsafe blocks

PYTHON:
  - Type hints on ALL functions (no Any)
  - ruff check + ruff format must pass
  - mypy --strict must pass
  - No bare except: clauses
  - pip-audit on every dependency change
  - >=70% coverage on core paths

C++:
  - -Wall -Wextra -Wpedantic -Werror on every compilation
  - No raw new/delete — smart pointers only
  - noexcept where applicable
  - C++17 minimum (no C++98/11)
  - clang-tidy on every PR

ALL CODE:
  - No hardcoded secrets
  - No TODO comments (convert to GitHub issue first)
  - CI passes before merge
  - Minimum one test per feature
  - PR description: what, why, how to test
```

---

## GSoC 2027 — Prepare From Day One

GSoC 2027 runs May–August 2027. Applications open February 2027. To be a competitive applicant, you need **a documented history of real OSS contributions and a proposal that solves a real problem for a real org.**

**This protocol IS your GSoC preparation.** Every PR, every audit, every blog post, every project you ship — it all goes into your application.

### Why You Can Get In

- GSoC orgs love Rust security tooling (Tokio, aya-rs, Sigma, Zeek accept contributors)
- You will have Vyrox, Orin Labs, Drift, Halo — real projects with real users
- You will have merged PRs across 4+ organizations by the time you apply
- Your blog posts will show depth, not just "I followed a tutorial"
- The adversarial lens is rare among applicants — most build, few break
- A security-focused proposal in 2027 is timely: the field is exploding

### Your GSoC Timeline

| Period | What to Do | GSoC Relevance |
|--------|-----------|----------------|
| **May–Oct 2026** | Build foundation: Rust + Python + C++. Contribute to 4+ orgs. Ship Vyrox MVP. | Establishes contribution history |
| **Nov 2026–Jan 2027** | Deep dive target org's codebase. Submit meaningful PRs. Build credibility. | Org familiarity = strong proposal |
| **Jan 2027** | Pick org + project. Draft proposal. Find a mentor (start reaching out now). | Proposal writing begins |
| **Feb 2027** | Refine proposal. Get mentor feedback. Submit before deadline. | Application submitted |
| **Mar 2027** | Wait for results. Keep contributing. | Maintain presence |
| **Apr 2027** | Pre-work with org. Set up project environment. | Project setup |
| **May–Aug 2027** | **GSoC summer.** Build, blog, ship. | You're in. |

### Target GSoC Organizations (Investigate These)

*Start following these on GitHub now. Star their repos. Read their CONTRIBUTING.md.*

| Organization | Language | Project Area | Good For |
|-------------|----------|--------------|----------|
| **Sigma HQ** | Python/YAML | Detection rules engine | Detection logic, rule processing |
| **Zeek** | C++/Python | Network security monitor | Protocol analysis, scripting |
| **The Honeynet Project** | Python/Rust | Honeypots, forensics | Attack simulation, detection |
| **aya-rs** | Rust | eBPF in Rust | Systems programming, kernel |
| **OWASP** | Python/JS | AppSec tooling | Web security, SAST/DAST |
| **MISP** | Python/PHP | Threat intelligence platform | CTI, STIX/TAXII |
| **TheHive** | Scala | SOC/SOAR platform | Alert management, case studies |
| **OpenCTI** | Python/React | Threat intel platform | Data pipelines, visualization |
| **MITRE ATT&CK** | Python/TS | ATT&CK navigator | Threat modeling, visualization |

### GSoC Proposal Tips

- **Solve a real problem:** Don't propose a feature you'll find cool. Propose something the maintainers have flagged as important.
- **Show you've read the codebase:** Reference specific files, functions, and conversations. "I read issue #X where you discussed Y" is gold.
- **Timeline is everything:** Be realistic. Break it into milestones with deliverables.
- **Blog everything:** Your application needs to show you can communicate. Weekly blog posts are your proof.
- **One org, one project:** Don't apply to 5 orgs. Pick one. Go deep.

### Your GSoC Checklist (Start Today)

- [ ] Star the target orgs' repos on GitHub
- [ ] Subscribe to their GitHub Discussions and issue trackers
- [ ] Join their Matrix/Discord/Slack channels
- [ ] Read their SECURITY.md, CONTRIBUTING.md, architecture docs
- [ ] Submit at least 3 PRs to your target org before November 2026
- [ ] Write a proposal draft by January 2027

---

## Weekly Artifact Requirements

Every week — all eight required:

| # | Artifact | Description |
|---|----------|-------------|
| 1 | **Reading notes** | Book, chapter(s), specific sections, your critique of the author's assumptions |
| 2 | **Lab task** | Build or break something concrete |
| 3 | **Code to ship** | GitHub commit(s) with PR link |
| 4 | **OSS contribution** | Target org, issue/PR, specific action taken |
| 5 | **Blog topic** | Title + 5-point outline + first paragraph |
| 6 | **Journal reflection** | What shipped, what you learned, what you question |
| 7 | **ATT&CK mapping** | Technique + detection hypothesis + evasion case |
| 8 | **Adversarial analysis** | For every system built this week: how would an attacker break it? |

---

## MITRE ATT&CK Case Study Calendar

| Weeks | Case Study | Primary Techniques | Adversarial Question |
|-------|-----------|-------------------|---------------------|
| 5–6 | SolarWinds / SUNBURST | T1195.002 | How would you detect a trojanized DLL in a supply chain build? |
| 7–8 | NotPetya / wiper | T1486, T1218 | How would you detect a disk wiper disguised as ransomware? |
| 9–10 | APT31 / ToolShell | T1566.001, T1574.002 | How does a SharePoint web shell evade network detection? |
| 11–12 | Scattered Spider | T1621, T1598 | How does MFA bombing work at scale against SSO? |
| 13–14 | APT41 / Winnti | T1195, T1574.001 | How does a supply chain attack persist past the initial compromise? |
| 15–16 | DarkSide / Colonial Pipeline | T1486, T1490 | How does RaaS inhibit recovery? What backup strategy survives? |
| 17–18 | Lazarus / AppleJeus | T1195.001, T1204.001 | How does a trojanized app survive code signing verification? |
| 19–20 | Hafnium / ProxyLogon | T1190, T1505.003 | How does an Exchange web shell maintain persistence? |
| 21–22 | UNC2452 / SUNSPOT | T1554, T1195.002 | How does malware hide in a build environment for months? |
| 23–24 | Volt Typhoon + REvil/Kaseya | T1059, T1562, T1195 | How does a state-sponsored actor use LOTL to evade EDR? |

Each case study produces:
- ATT&CK navigator layer JSON
- Sigma rule skeleton
- Detection hypothesis (what telemetry would catch this?)
- Evasion hypothesis (what would the attacker change to evade?)
- Blog post or write-up

---

## PHANTOM Codebase Audit Protocol

For every OSS organization you contribute to:

**Day 1 — Architecture Pass**
- Clone, read README + CONTRIBUTING.md + SECURITY.md
- Map directory structure → draw architecture diagram
- Identify language breakdown, dependency tree
- Run security audit commands
- **Adversarial checkpoint:** What is the trust model? Who can write code to main?

**Day 2 — Data Flow Pass**
- Trace 3 critical paths end-to-end
- Identify trust boundaries and input validation points
- Note any unsafe blocks, unvalidated deserialization, weak crypto
- **Adversarial checkpoint:** What happens if input 3 is an adversarial payload?

**Day 3 — Test Suite Pass**
- Run tests; note pass/fail ratio
- Identify coverage gaps (`tarpaulin` for Rust, `coverage.py` for Python)
- Find paths with zero test coverage → contribution targets
- **Adversarial checkpoint:** What is NOT tested that should be?

**Day 4 — Issue Triage + Threat Model**
- Search: `good-first-issue`, `help-wanted`, `bug`, `security`
- Shortlist 3 issues matching your current skill level
- Read all discussion threads
- **Adversarial checkpoint:** Which of these bugs could be exploited?

**Day 5 — Contribution**
- Branch, fix, test, document
- Write PR with: what, why, how to test, security implications
- Respond to all feedback within 24 hours
- **Adversarial checkpoint:** What would an attacker do with this merged PR?

---

## Safety Commandments — Non-Negotiable

1. All offensive code in isolated VMs, host-only networks, no internet egress
2. Snapshots before every lab; revert after every session
3. Dedicated analysis VMs: REMnux (Linux malware) + FlareVM (Windows)
4. **Never target unauthorized systems. Ever.**
5. Encrypt all lab communications
6. OSS contributions: detections, tooling, infrastructure only — never offensive exploits
7. All PRs must pass: *"Would I be proud if this was the first result when someone Googled my name?"*

---

## The Human Day — Realistic Schedule (University Holidays Mode)

> This is a marathon, not a sprint. The body is the vehicle. No vehicle, no code.

**Sleep:** 7.5–8.5 hours (target: 23:00 → 07:00)
**Meals:** Breakfast, lunch, dinner — non-negotiable, no skipping
**Movement:** 3–5 sessions per week (gym, run, walk, stretch — anything)
**Walk:** 1 per day minimum (20-30 min outside, mandatory)
**Family:** 2 hours evening — you're going home after the hostel. Be with them.
**Weekends:** Saturday afternoon/evening full rest. Sunday morning rest.

---

### The Ideal Day

```
06:30–07:00   Wake up, hygiene, breakfast, stretch
07:00–09:00   Morning deep work (Rust/Python — 90 min blocks)
09:00–09:15   Break — walk outside, water, food
09:15–10:30   Morning deep work continued
10:30–11:00   OSS contribution (30 min minimum)
11:00–12:30   Learning block (books, Rustlings, reading)
12:30–13:30   Lunch — eat properly, no screens
13:30–15:00   Afternoon deep work (build block 2)
15:00–15:30   Walk outside (20-30 min, mandatory)
15:30–17:00   Afternoon learning (books, labs, LeetCode)
17:00–17:30   Code quality block (review, refactor, tests)
17:30–18:00   Wind down — journal, prep tomorrow
18:00–20:00   Family time — dinner, people, no screens
20:00–21:00   Light evening work (if energy: OSS, blog, reading)
               If not: rest, gym, walk, whatever your body needs
21:00–22:00   Wind down — journal entry, non-code reading
22:00–23:00   Relax
23:00          Asleep
```

**Core deep work: ~5 hours/day** (morning + afternoon blocks)
**Learning: ~2 hours/day**
**OSS: 30 min/day**
**Movement: 1 walk/day minimum + gym 3-5x/week**
**Family: 2 hours evening**

---

### Weekends

**Saturday:**
- Morning: normal work (3-4 hours)
- Afternoon (14:00 onwards): **FULL REST** — no screens, no code, no studying
- Evening: rest, family, whatever fills you up

**Sunday:**
- Morning: **REST** — sleep in, light breakfast
- Afternoon: 2-3 hours light work (OSS review, blog, reading)
- Evening: prep for the week ahead

---

### Warning Signs — You're Going Too Hard

These are not motivational signs — they are **warning signs:**

- [ ] Skipping meals to "finish this one thing"
- [ ] No walk outside in 2 days
- [ ] Working after 22:00 three nights in a row
- [ ] Getting sick (burnout hits the immune system first)
- [ ] No meaningful family time in a week
- [ ] "Too busy" for the gym three weeks in a row
- [ ] Snapping at people over small things
- [ ] Dread instead of readiness for the next day

**If any of these are true:** Take one day lighter. Sleep 8 hours. Eat three meals. Walk. The world does not end. You come back sharper.

---

### The Core Rule

**5 hours of focused deep work per day is enough.** Not 12. Not 18.

Five hours of focused, adversarial, MIT-grade work — with breaks, meals, movement, and family time — will outproduce 12 hours of grinding while half-asleep.

The protocol demands **quality**. Not hours. Quality.

---

## PHANTOM Doctrine

> Read before you write. Understand before you claim. Build to be broken.
> Detect before you're attacked. Ship every week.
> Take care of your body. Rest is not weakness. Family is not a distraction.
> Sleep is not wasted time. Five focused hours beats twelve exhausted ones.
> The open source world will know your name before you finish this protocol.
> Your code is only done when it survives adversarial review.

---

*PHANTOM Mentor Protocol — MIT-Grade Edition*
*Start date: May 22, 2026 | Graduation: November 22, 2026*
*All offensive work is authorized, isolated, and ethical.*