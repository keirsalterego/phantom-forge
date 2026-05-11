# Orin Labs — Organization Structure

> *"A great project needs a great structure. A great structure needs great maintainers."*

---

## GitHub Organization: `orinlabs`

All repos live under https://github.com/orinlabs

**Naming convention:** `orinlabs/<repo>` for the distro core. `<tool>-keiron` for standalone tools (e.g., `drift-keiron`).

---

## Repository Map

### Core OS Repositories (7 repos)

| Repo | Purpose | Language | CI Required |
|------|---------|----------|-------------|
| `orinlabs/os` | Main distro repo — ISO builds, build scripts, package index | Shell + Rust | ✅ QEMU boot test |
| `orinlabs/Vale` | Rust Vale (no_std, memory-safe) | Rust | ✅ QEMU boot test |
| `orinlabs/bootloader` | Stage 1 + Stage 2 UEFI bootloader | Rust | ✅ UEFI test |
| `orinlabs/loom` | Package manager (Rust CLI) | Rust | ✅ integration tests |
| `orinlabs/atlas` | SDK: cross-compilation toolchain, cargo targets | Rust | ✅ test sysroot |
| `orinlabs/anvil` | ISO build automation scripts | Shell + Rust | ✅ ISO smoke test |
| `orinlabs/keiron-docs` | Documentation hub (architecture, guides) | Markdown | ✅ link check |

### Standalone Tool Repositories (6 repos)

| Repo | Purpose | crates.io | ISO Default? |
|------|---------|-----------|-------------|
| `drift-keiron` | Red-team proxy framework | ✅ | ✅ |
| `termino-keiron` | Secure terminal mesh | ✅ | ✅ |
| `sigmatrix-keiron` | Detection rule engine | ✅ | ✅ |
| `ghostpacket-keiron` | Packet analysis toolkit | ✅ | ✅ |
| `memoryhound-keiron` | Memory forensics | ✅ | ✅ |
| `redops-keiron` | Adversary emulation | ✅ | ✅ |

### Community & Web Repositories (3 repos)

| Repo | Purpose |
|------|---------|
| `orinlabs/website` | orinlabs.dev (GitHub Pages, Jekyll) |
| `orinlabs/community` | Matrix/Discord bridge config, issue templates, PR templates |
| `orinlabs/security` | Security advisories, CVE coordination, GPG keys |

---

## Total: 16 Repositories

```
orinlabs/
├── os/                  ← Main distro repo (ISO builds here)
├── Vale/              ← Rust Vale
├── bootloader/          ← UEFI bootloader
├── loom/           ← Package manager
├── atlas/           ← SDK + toolchain
├── anvil/           ← Build automation
├── keiron-docs/         ← All documentation
├── website/             ← Public website
├── community/           ← Templates + infra
└── security/            ← Security advisories

drift-keiron/           ← Standalone tool
termino-keiron/          ← Standalone tool
sigmatrix-keiron/        ← Standalone tool
ghostpacket-keiron/      ← Standalone tool
memoryhound-keiron/      ← Standalone tool
redops-keiron/           ← Standalone tool
```

---

## Maintainership Model

### Owner
**Keiron** (you) — founder, BDFL, final decision-maker on all repos.

### Roles

| Role | Responsibility | Count |
|------|--------------|-------|
| **Owner** | All repos. Can merge to any branch. | 1 (Keiron) |
| **Core Maintainer** | orinlabs/os, Vale, bootloader. Can merge without owner review. | 3 (recruit after Month 3) |
| **Tool Maintainer** | Own one standalone tool repo. Review PRs, cut releases. | 6 (recruit after Month 4) |
| **Docs Maintainer** | keiron-docs + website. Review docs PRs. | 1 (recruit after Month 3) |
| **Contributor** | Anyone who opens a PR. No merge rights until promoted. | Unlimited |

### Promotion Path

```
Contributor (opened PR) → Trusted Contributor (2+ merged PRs) →
Tool Maintainer (1+ tool at MVP, 3+ merged external PRs) →
Core Maintainer (Vale or os at MVP, mentored 1+ new contributor)
```

### Dormancy Rules

- **Tool:** If no commits for 30 days and no response to issues → tool marked "seeking maintainer" with community vote
- **Core repo:** If no commits for 14 days → owner notified, public status update issued
- **Abandoned repo:** Archived on GitHub with clear explanation. Can be forked.

---

## Branch Strategy

### Core Repos (os, Vale, bootloader)

```
main          — development (can force-push for rewrites)
stable        — current stable release (no force-push, tagged releases)
release/X.Y   — release branches (maintenance only, no new features)
```

### Standalone Tool Repos

```
main          — development
vX.Y.Z        — crates.io releases (tags only)
```

### Protection Rules

| Branch | Required Reviews | Required Checks | Force Push |
|--------|-----------------|-----------------|------------|
| main | 1 (owner or core maintainer) | CI green | ❌ blocked |
| stable | 2 (owner + 1 maintainer) | CI green + ISO test | ❌ blocked |
| release/X.Y | 1 | CI green | ❌ blocked |

---

## Release Model

### Semantic Versioning

- **MAJOR:** Breaking changes to Vale ABI, syscall interface, or Loom CLI
- **MINOR:** New features, new packages, Vale improvements (every 6 months)
- **PATCH:** Bug fixes, security patches (every 4 weeks)

### Release Cadence

| Type | Frequency | Trigger |
|------|-----------|---------|
| **Patch** | Every 4 weeks | Security fixes, bug fixes |
| **Minor** | Every 6 months | New features, Vale bump, new tools |
| **Major** | Yearly | Large architectural changes |

### Lifecycle Policy

- **Major version:** 18 months of security updates
- **Stable branch:** 1 active at a time. Old stable goes to LTS candidate.
- **End-of-life:** Announced 3 months in advance. Archive old branch.

### Nightly vs Stable

- **Nightly builds:** Every commit to `main`. For testers only. Not recommended for use.
- **Weekly builds:** Every merge to `stable`. For early adopters. May have bugs.
- **Release builds:** Every minor version tag. For production use.

---

## Communication Channels

| Channel | Purpose | Access |
|---------|---------|--------|
| GitHub Discussions | All repos | Public |
| Matrix: `#orinlabs:libera.chat` | Real-time chat | Public |
| Libera IRC: `#orinlabs` | IRC bridge | Public |
| GitHub Issues | Bug reports, feature requests | Public |
| security@orinlabs.dev | Private security disclosures | Private |
| blog.orinlabs.dev | Release notes, tutorials | Public |

---

## What Each Repo Must Have

### Core Repos (minimum bar before first public release)

```
.github/
  workflows/ci.yml       ← clippy + test on every PR
  workflows/iso.yml       ← ISO build on merge to main
  PULL_REQUEST_TEMPLATE.md
  ISSUE_TEMPLATE/        ← bug, feature, security

CONTRIBUTING.md          ← how to contribute
CODE_OF_CONDUCT.md       ← conduct rules
SECURITY.md              ← security disclosure process
LICENSE                  ← MIT (preferred)

README.md                ← what this repo does, quick start
ARCHITECTURE.md          ← technical architecture diagram
```

### Standalone Tool Repos (minimum bar before ISO inclusion)

```
.github/
  workflows/ci.yml       ← clippy + test on every PR
  workflows/release.yml  ← crates.io publish on tag

Cargo.toml              ← semver version
Cargo.lock              ← pinned deps

CONTRIBUTING.md
CODE_OF_CONDUCT.md
SECURITY.md
LICENSE (MIT)

README.md               ← what it does, installation, usage
ARCHITECTURE.md         ← technical design
tests/                  ← integration tests (≥70% coverage target)
```

---

## Build Environment

### Dependencies (what you need to build the ISO)

| Tool | Version | Purpose |
|------|---------|---------|
| Rust (nightly) | 2026-05 | Kernel + all Rust components |
| musl-gcc | latest | Static linking for userland |
| xorriso | 1.5.4+ | ISO9660 creation |
| grub2 | 2.06+ | UEFI bootloader |
| mtools | latest | FAT image creation |
| QEMU | 7.0+ | Boot testing |
| GPG | 2.4+ | Signing releases |

### Build Container

All builds run in a Docker container with locked versions. Contributors can reproduce exactly.

---

## Dependency Between Repos

```
bootloader → Vale → os
                        ↓
              anvil (builds the ISO)
              loom (packages tools)
              atlas (cross-compiler)

drift-keiron → standalone, used by Vale/networking
termino-keiron → standalone, used by os/loom
sigmatrix-keiron → standalone, used by os/loom
ghostpacket-keiron → standalone, used by os/loom
memoryhound-keiron → standalone, used by os/loom
redops-keiron → standalone, used by os/loom
```

---

*Last updated: May 2026*
*Org version: 1.0*