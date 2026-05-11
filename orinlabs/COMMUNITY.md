# Orin Labs — Community Infrastructure

> *"A community is infrastructure. Build it like you build the OS."*

---

## Communication Channels

### Primary: GitHub

**Every repository has:**
- GitHub Discussions (for questions, ideas, support)
- GitHub Issues (for bugs and feature requests)
- Pull Requests (for code contributions)

**Rules:**
- Every issue gets a response within 48h (even if just "we're looking at it")
- Every PR gets reviewed within 72h
- Closed issues: always explain why (won't fix, duplicate, fixed in other version)

### Real-Time: Matrix + IRC

**Matrix:** `#orinlabs:libera.chat`
**IRC:** `irc.libera.chat/#orinlabs` (bridged to Matrix)

**Channel structure:**

| Channel | Purpose | Moderated? |
|---------|---------|-----------|
| `#orinlabs:libera.chat` | General chat, support | Yes |
| `#orinlabs-dev:libera.chat` | Development discussion | Yes |
| `#orinlabs-offtopic:libera.chat` | Off-topic chat | Yes |
| `#orinlabs-announce:libera.chat` | Release announcements | No (read-only for most) |

**Moderation rules:**
1. Be respectful. No harassment, no discrimination.
2. Stay on topic in each channel.
3. No spam, no advertising.
4. Security disclosures go to security@orinlabs.dev, not the public channel.
5. English only in main channels.

**Moderators:** Keiron (owner) + 2 recruited community moderators after Month 3.

### Website: orinlabs.dev

Built with Jekyll, hosted on GitHub Pages.

**Structure:**

```
orinlabs.dev/
├── index.html         ← Landing page (brief, screenshot, download link)
├── download/          ← ISO download + checksums + signatures
├── docs/              ← Documentation (mkdocs-material)
├── blog/              ← Jekyll blog (release notes, tutorials, community posts)
├── community/         ← Contributing guide, code of conduct, FAQ
└── security/          ← Security policy, advisories archive
```

**CMS:** None. Pure Jekyll + Markdown. Every team member can edit via PR.

---

## Issue Templates

All repos use standardized issue templates in `.github/ISSUE_TEMPLATE/`:

### Bug Report

```markdown
---
name: Bug Report
about: Something isn't working as expected
labels: bug
---

## Description
[Clear and concise description of the bug]

## Steps to Reproduce
1. Go to '...'
2. Click on '...'
3. See error

## Expected Behavior
[What you expected to happen]

## Actual Behavior
[What actually happened]

## Environment
- Orin Labs version:
- Hardware (if applicable):
- Installation method (ISO/live/installed):

## Logs
```
[Paste relevant log output here]
```

## Additional Context
[Any other context about the problem]
```

### Feature Request

```markdown
---
name: Feature Request
about: Suggest an idea for this project
labels: enhancement
---

## Problem
[What problem does this solve?]

## Proposed Solution
[Describe the solution you'd like]

## Alternatives Considered
[Any alternative solutions you've considered]

## Use Cases
[Who would use this? When?]

## Additional Context
[Screenshots, mockups, links to similar features]
```

### Security Advisory

```markdown
---
name: Security Advisory
about: Report a security vulnerability (PRIVATE — DO NOT post publicly)
labels: security
---

**STOP:** If this is an active exploit, do not file a GitHub issue. Email security@orinlabs.dev directly.

## Vulnerability Type
[e.g., buffer overflow, privilege escalation, information disclosure]

## Affected Component
[Vale/bootloader/tool name]

## Severity
[Critical/High/Medium/Low — with justification]

## Description
[Full description of the vulnerability]

## Proof of Concept
[Code, commands, or steps to reproduce]

## Suggested Fix
[If known, how to fix it]
```

---

## Pull Request Template

```markdown
## Description
[What does this PR do? Why?]

## Type
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation
- [ ] Refactor
- [ ] Test

## Testing
[How was this tested? What cases were covered?]

## Checklist
- [ ] My code follows the style guidelines (clippy passes, rustfmt clean)
- [ ] I have self-reviewed my own code
- [ ] I have added tests that prove the fix is effective
- [ ] All new code has doc comments on public functions
- [ ] I have checked that CI passes on this PR
- [ ] I have not introduced any new warnings or errors
- [ ] If this changes a user-facing interface, I have updated relevant documentation
- [ ] If this is a security fix, I have followed the security advisory template

## Screenshots (if applicable)
[If the change affects UI or produces visible output]

## Additional Context
[Any other relevant context]
```

---

## Code of Conduct

### Our Pledge

We as members, contributors, and leaders pledge to make participation in our community a harassment-free experience for everyone, regardless of age, body size, disability, ethnicity, gender identity and expression, level of experience, nationality, personal appearance, race, religion, or sexual identity and orientation.

### Our Standards

**Examples of behavior that contributes to a positive environment:**
- Using welcoming and inclusive language
- Being respectful of differing viewpoints and experiences
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards other community members

**Examples of unacceptable behavior:**
- The use of sexualized language or imagery and unwelcome sexual attention
- Trolling, insulting/derogatory comments, and personal or political attacks
- Public or private harassment
- Publishing others' private information without explicit permission
- Other conduct which could reasonably be considered inappropriate

### Enforcement

Instances of abusive, harassing, or otherwise unacceptable behavior may be reported to:
- **Public:** Open a GitHub issue with label `conduct`
- **Private:** Email keiron@orinlabs.dev

All complaints will be reviewed and investigated. The maintainer team will respond in a way that is deemed necessary and appropriate to the circumstances.

---

## Contributor Journey

### Level 1 — First Contribution

1. Read CONTRIBUTING.md in any repo
2. Find a `good first issue` label
3. Fork → fix → PR
4. Response within 72h, merge within 1 week

### Level 2 — Regular Contributor

- 3+ merged PRs across repos
- Responds to issues with useful information
- Participates in discussions

### Level 3 — Trusted Contributor

- 10+ merged PRs
- Reviews PRs in their area of expertise
- Can label issues and close duplicates

### Level 4 — Maintainer

- Nominated by owner (Keiron)
- Has merge rights on ≥1 repo
- Responds to all issues/PRs within 48h
- Cuts releases when needed
- Writes release notes
- Represents the project in public

### Removing Maintainers

- If a maintainer is inactive for 60+ days without notice → demoted to contributor
- If a maintainer violates the code of conduct → removed immediately
- If a maintainer consistently breaks CI or ignores review standards → warned, then removed

---

## Contributor Recognition

### Release Notes

Every minor/major release notes section:

```markdown
## Contributors
Thank you to the following contributors who merged PRs in v1.2.0:

- @username — [PR #123](link) — Fixed memory leak in TCP/IP stack
- @anotheruser — [PR #124](link) — Added aarch64 support
```

### Contributor Spotlight Blog

Bi-monthly blog post featuring 1–2 external contributors:
- What they contributed
- Why they chose Orin Labs
- What they're working on next

### Hall of Fame

A permanent page on orinlabs.dev listing every contributor who has had ≥3 PRs merged, organized by year.

---

## Support Channels

### Community Support (Free)

- GitHub Discussions — questions about usage, installation, tooling
- Matrix/IRC — real-time chat for support
- GitHub Issues — bugs and feature requests

### Professional Support (Future, Year 2+)

If there's demand, a paid support tier may be offered via:
- keiron@orinlabs.dev
- Response within 24h, 5-day SLA

**Rule:** Free community support never gets deprioritized for paid support. Paid is for enterprise SLA guarantees.

---

## Governance

### Decision Making

- **Technical decisions:** Made by maintainers, discussed in GitHub Discussions or Matrix
- **Major architectural changes:** RFC process (open a GitHub Discussion titled "RFC: [topic]")
- **Release decisions:** Owner (Keiron) has final say
- **Community disputes:** Owner mediates, their decision is final

### RFC Process

For significant changes:

1. Open a GitHub Discussion: "RFC: [short description]"
2. Describe the problem, proposed solution, alternatives
3. Allow 2 weeks of discussion
4. Owner makes final decision (merge, defer, or reject)
5. If merged: implement in a branch, PR when ready

### Versioning Policy

- All repos use semantic versioning
- Breaking changes only in major versions
- Changelog maintained in CHANGELOG.md per repo
- Deprecation notices given 1 minor version in advance

---

## Security Disclosure

### Private Disclosure

Email: security@orinlabs.dev

Response time:
- Critical: 24h acknowledgment, 7-day fix or disclosure
- High: 48h acknowledgment, 30-day fix or disclosure
- Medium: 72h acknowledgment, 90-day fix or disclosure
- Low: 1-week acknowledgment, next release fix

### Public Disclosure

After the fix is released, a security advisory is posted on GitHub:
- `.github/SECURITY.md` links to this process
- GitHub Security Advisories (GHSAs) used for CVEs
- Advisories emailed to security@lists.orinlabs.dev subscribers

### CVE Coordination

- Orin Labs CVEs are filed with MITRE via GitHub's CVE request process
- Format: `KL-YYYY-XXXX` (Orin Labs, year, number)
- Example: `KL-2026-0001`

---

## Metrics

Track community health monthly:

| Metric | Target (Month 3) | Target (Month 6) | Target (Year 1) |
|--------|-----------------|-----------------|-----------------|
| GitHub stars (all repos) | 200 | 500 | 2,500 |
| GitHub discussions (monthly) | 10 | 30 | 100 |
| GitHub issues resolved (monthly) | 20 | 50 | 200 |
| External contributors (cumulative) | 3 | 10 | 30 |
| Matrix/IRC active users (weekly) | 5 | 15 | 50 |
| Blog subscribers | 20 | 100 | 500 |

---

## Meeting Structure

### Weekly Dev Sync (Optional, Matrix)

- When: Every Friday 18:00 UTC (drop-in, not mandatory)
- Where: `#orinlabs-dev:libera.chat`
- Format: What shipped this week, what's blocked, what's next
- Not recorded. No minutes. Low-commitment.

### Monthly Community Call (Future, Month 6+)

- When: First Thursday of each month, 19:00 UTC
- Where: Jitsi (link posted in `#orinlabs:libera.chat` one week before)
- Format: 30min: Owner update (10min) + Q&A (20min)
- Recorded and posted to YouTube (unlisted)

---

*Last updated: May 2026*
*Community version: 1.0*