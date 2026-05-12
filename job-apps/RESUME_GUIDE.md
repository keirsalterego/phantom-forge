# RESUME TAILORING GUIDE — Security, Rust, Python & C++ Roles

> Compiled for your job search. Adjust to each role.

---

## The Golden Rules

1. **One resume, one version** — Tailor per role type, not per company
2. **3 bullet points max per job** — Most impactful, not chronological exhaustiveness
3. **ATS keyword match** — Mirror the job description language verbatim
4. **Rust/Python/C++ first** — If the role mentions it, it goes in your header
5. **No soft skills** — No "passionate about security." Show it.

---

## Role Type 1: Security Engineer / Detection Engineer

### Header
```
Keiron Salter-Ego
Security Engineer | Rust · Python · C++ | keir@vyrox.dev
GitHub: github.com/keirsalterego | LinkedIn: linkedin.com/in/keirsalterego
Security clearance: [If applicable]
```

### Projects Section (replace Work Experience if new)
```
PROJECTS

Vyrox Security — AI-Augmented SOC Platform (vyrox.dev)
- Built SIEM pipeline in Rust + Python processing 1M+ events/day
- Integrated Sigma rule engine for real-time threat detection
- Stack: Rust, Python, AsyncIO, PostgreSQL, Kafka

Orin Labs / Drift — Red-Team Proxy Framework
- HTTP/SOCKS5 proxy with TLS MITM capabilities in Rust
- Contributed to Orin OS security toolchain (8 tools in repo)

Halo — Detection Rule Engine (github.com/orin-labs/halo)
- Sigma → SPL/EQL/regex rule converter in Rust
- 70%+ test coverage, 2k+ lines of production Rust
```

### Skills Matrix
```
LANGUAGES:    Rust · Python · C++ · SQL · Bash
SECURITY:     SIEM · ATT&CK · Sigma rules · Threat detection · YARA
TOOLS:        Wireshark · tcpdump · GDB · Volatility3 · OSSEC
CLOUD:        AWS (Security Specialty) · GCP fundamentals
FRAMEWORKS:   Tokio · AsyncIO · FastAPI · Pytest
```

### Quantifiable Metrics Template
```
- [Verb] [what] achieving [metric] using [tech stack]
- Designed/implemented [system] processing [volume] with [improvement]
- Integrated [tool] reducing [metric] by [X%]
```

---

## Role Type 2: Systems Engineer / Platform Engineer

### Header
```
Keiron Salter-Ego
Systems Engineer | Rust · C++ · Python | keir@vyrox.dev
GitHub: github.com/keirsalterego | LinkedIn: linkedin.com/in/keirsalterego
```

### Projects Section
```
PROJECTS

Orin OS (github.com/orin-labs/orin-os)
- Rust-based OS with 8 security tools, reproducible builds
- Built with: Rust, C++, custom allocators, eBPF

Drift — Red-Team Proxy (github.com/orin-labs/drift)
- HTTP/SOCKS5 + TLS MITM proxy in Rust
- Zero-copy parsing with unsafe Rust FFI bindings

Cribl Alternative (in progress)
- Observability data pipeline in Rust
- 50k+ events/second throughput, zero-copy architecture
```

### Skills Matrix
```
LANGUAGES:    Rust (4 yrs) · C++ (2 yrs) · Python (5 yrs) · Go (learning)
SYSTEMS:     OS kernels · TCP/IP · Linux internals · eBPF · FFI
TOOLS:        GDB · valgrind · perf · strace · ltrace
BUILD:        Cargo · CMake · Meson · Cargo-nextest
```

---

## Role Type 3: DevSecOps / Platform Security

### Header
```
Keiron Salter-Ego
DevSecOps / Platform Security | Python · Rust · Terraform | keir@vyrox.dev
GitHub: github.com/keirsalterego | LinkedIn: linkedin.com/in/keirsalterego
```

### Projects Section
```
PROJECTS

Vyrox Security CI/CD Pipeline
- Built GitHub Actions pipeline for Rust + Python SOC platform
- Automated security scanning: Semgrep, Trivy, Grype
- Zero secrets in code — Vault-based secret rotation

Orin Labs Reproducible Builds
- Nix-based reproducible build system for Orin OS
- Binary transparency with reproducible signatures
- Automated nightly CI on GitHub Actions
```

### Skills Matrix
```
IAC:          Terraform · Pulumi · CloudFormation
CI/CD:        GitHub Actions · ArgoCD · Tekton
SECURITY:     Vault · OPA · Falco · Trivy · Grype · Semgrep
CLOUD:        AWS (Security Specialty) · GCP · Azure
CONTAINERS:   Docker · Kubernetes · Helm · Kustomize
```

---

## Role Type 4: Startup / Early-Stage (Generalist)

### Header
```
Keiron Salter-Ego
Founder-Engineer | Rust · Python · C++ | vyrox.dev
Building: AI-augmented SOC platform | 7 production tools in Rust
GitHub: github.com/keirsalterego | keir@vyrox.dev
```

### Unique Angle: Lead with the build
```
EXPERIENCE (or substitute with Projects if no traditional work)

Vyrox Security — Founder (vyrox.dev)
- Building AI-augmented SOC platform (current focus: MVP)
- 7 tools built across Rust/Python: Drift, Slate, Halo, Trace, Haven, Veil, Atlas
- OSS contributions to Sigma HQ, Zeek, Suricata

Orin Labs — Founder (github.com/orin-labs)
- Cybersecurity OS org with 3 repos, public CI, security advisories
- Orin OS: Rust-based OS with reproducible builds, nightly CI
- 2 merged PRs, active contributor to aya-rs (eBPF in Rust)
```

---

## ATS Optimization Checklist

For every application:

- [ ] Copy-paste the **exact** keywords from the job description
- [ ] If job says "Kubernetes security", your resume says "Kubernetes security"
- [ ] If job says "Rust async programming", your resume says "Rust async programming"
- [ ] "SIEM" not "siem" — case matters for some ATS systems
- [ ] Place most-used keywords in first 3 bullet points
- [ ] Put technologies in a dedicated **TECHNOLOGIES** section (ATS parses these)
- [ ] Remove "References available upon request" — dead weight
- [ ] Convert months to "Jan 2024" format — some ATS can't parse "January"

### Keyword Extraction Method
1. Open the job description
2. Copy everything into a text file
3. Remove common words (the, and, to, of, a, in, for, with)
4. Count remaining words — the top 10 are your ATS keywords
5. Sprinkle them into your bullet points naturally

---

## Red Flags That Kill Resumes

| Red Flag | Fix |
|----------|-----|
| "Passionate about cybersecurity" | Replace with actual project outcomes |
| "Strong communication skills" | Every resume says this — delete it |
| Only compliance/GRC experience for security engineering roles | Lead with technical projects |
| No quantifiable metrics | Always add: throughput, scale, improvement % |
| 4+ pages | Cut to 1-2 pages max |
| Generic for all roles | You need at least 3 tailored versions |
| No GitHub link | Add it — hiring managers WILL check |
| Misspelled technologies | Proofread twice. "Tokio" not "Tokyo" |

---

## Cover Letter Angle

For every cover letter:

**Hook** (first 2 sentences): Why this company, specifically, right now.

**Body** (3-4 bullets): What you built that maps to their problems. No padding.

**Closer**: Specific ask — "I'm applying for your Senior Security Engineer role because..." and a clear call to action.

**Length**: 250 words max.

