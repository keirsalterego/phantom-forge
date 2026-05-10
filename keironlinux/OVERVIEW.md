# Keiron Linux — Architecture Overview

> *"Memory safety isn't a feature. It's the baseline."*

---

## What Is Keiron Linux?

Keiron Linux is a bootable, installable cybersecurity operating system built entirely in Rust — from the bootloader to the userspace tools. It is not a Linux kernel fork. It is a from-scratch OS that draws inspiration from the Linux ecosystem (syscalls, VFS, toolchain) while being fundamentally memory-safe by default.

The goal: an OS that security researchers, red teamers, and sysadmins can boot from USB, use as their daily driver for offensive and defensive work, and trust because the entire stack — kernel to userland — is written in a language that eliminates entire classes of bugs.

---

## Design Philosophy

### 1. Memory Safety by Default

Rust's ownership model prevents:
- Use-after-free
- Buffer overflows
- Data races
- Null pointer dereferences

No other mainstream OS has this property at the kernel level. Linux, BSD, and Windows are written in C — a language where memory safety is the developer's responsibility, not the compiler's. Keiron Linux is the first serious attempt to build a production OS with Rust as the primary language.

### 2. Hardened by Default

Every security mitigation is on by default:
- KASLR (Kernel Address Space Layout Randomization)
- SMEP (Supervisor Mode Execution Prevention)
- SMAP (Supervisor Mode Access Prevention)
- W^X (Write xor Execute — no writable code pages)
- Noexec heap and stack
- seccomp-bpf on all daemons
- Stack canaries on all userland binaries
- RELRO (Relocation Read-Only) on all binaries

### 3. Reproducible by Default

Every ISO is built from source with a locked toolchain. The SHA256 hash of every release is published. Contributors can independently verify that the binary matches the source.

### 4. No Abandonware

SnakeSec built tools and stopped. Kali Linux ships and maintains. Keiron Linux follows Kali's model: nightly CI, security advisories, active maintainers, and a community that doesn't go dormant.

---

## Architecture Layers

```
┌─────────────────────────────────────────────────────┐
│                 USERNEL                             │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐    │
│  │ Keirox  │ │Termino  │ │SigMatrix│ │Ghost    │    │
│  │         │ │         │ │         │ │ Packet  │    │
│  └─────────┘ └─────────┘ └─────────┘ └─────────┘    │
│  ┌──────────────────────────────────────────────┐   │
│  │        KeironPkg (Package Manager)           │   │
│  └──────────────────────────────────────────────┘   │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐    │
│  │runit    │ │ musl    │ │ busybox │ │ binutils│    │
│  │ init    │ │ libc    │ │ utils   │ │         │    │
│  └─────────┘ └─────────┘ └─────────┘ └─────────┘    │
├─────────────────────────────────────────────────────┤
│                 KERNEL                              │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐    │
│  │IDT/APIC│ │ VFS     │ │ TCP/IP  │  │ Memory  |    │
│  │ interrupt│ │ ext2/FAT│ │ stack    │  mgmt   |    │
│  └─────────┐ └─────────┘ └─────────┘ └─────────┘    │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐                │
│  │Scheduler│ │Process  │ │ EDR     │                │
│  │         │ │ mgmt    │ │ hooks   │                │
│  └─────────┘ └─────────┘ └─────────┘                │
├─────────────────────────────────────────────────────┤
│                 BOOTLOADER                          │
│  ┌─────────┐ ┌─────────┐                            │
│  │Stage 1  │ │Stage 2  │  UEFI + Legacy BIOS        │
│  │ (UEFI)  │ │(kernel) │                            │
│  └─────────┘ └─────────┘                            │
├─────────────────────────────────────────────────────┤
│                 HARDWARE                            │
│  x86_64 (primary) | aarch64 (future)                │
└─────────────────────────────────────────────────────┘
```

---

## Kernel Architecture

The kernel is written in safe Rust with `no_std`. No standard library. No heap allocator by default. All memory management is explicit.

### Core Components

#### 1. Bootloader (Stage 1 + Stage 2)
- **Stage 1:** UEFI application in Rust. Parses FAT32/EFI system partition. Loads stage 2.
- **Stage 2:** Minimal loader that switches from protected mode to long mode (x86_64). Sets up page tables. Transfers control to kernel.
- **Legacy BIOS:** Also supported via a separate stage 1 BIOS-compatible loader.

#### 2. Interrupt Descriptor Table (IDT)
- Memory-safe interrupt handling
- APIC support for multi-core (SMP)
- IRQ routing and handling
- No unsafe blocks in interrupt handlers

#### 3. Memory Management
- Physical memory allocator (buddy system)
- Virtual memory manager (page tables)
- No dynamic allocation in hot paths
- Slab allocator for kernel objects

#### 4. Process Scheduler
- Preemptive multitasking
- Round-robin scheduling initially
- Process states: running, ready, blocked, zombie
- PID allocator (no reuse within session)

#### 5. VFS (Virtual File System)
- Mount abstraction layer
- Supported: ext2, FAT32, ISO9660
- Device file abstraction (/dev)
- Procfs and sysfs compatible layout
- Path resolution with symlink handling

#### 6. TCP/IP Stack
- Embedded, hardened network stack
- IPv4 + IPv6 (basic)
- TCP, UDP, ICMP
- Socket abstraction (Berkeley-like API)
- Used by: Keirox (red-team proxy), EDR hooks, package manager

#### 7. EDR (Endpoint Detection & Response)
- Syscall hooking (audit via seccomp)
- Process creation monitoring
- Network connection tracking
- File write monitoring
- Event log buffer (ring buffer, safe Rust)

---

## Userspace Architecture

### Init System

**runit** — lightweight, minimal, script-friendly. No systemd. No systemd drama.

- Stage 1: /etc/runit/boot
- Stage 2: /etc/runit/runlevel (default)
- Stage 3: /etc/runit/shutdown

### C Library

**musl** — lightweight, static linking, minimal attack surface. No glibc. No telemetry.

### Core Utilities

**Busybox** (embedded) + custom Rust replacements for security tools.

### Package Manager

**KeironPkg** — written in Rust, signed packages, SHA256 checksums, reproducible builds.

```
Commands:
  keironpkg install <package>    # Install a package
  keironpkg update               # Update package index
  keironpkg upgrade <package>    # Upgrade a package
  keironpkg remove <package>     # Remove a package
  keironpkg search <query>       # Search packages
  keironpkg verify <package>     # Verify package signature
```

Package format: `.kpkg` (tar.gz + signature + metadata)

### The 6 Security Tools (Standalone + Ship in ISO)

| Tool | Purpose | Standalone? | In ISO? |
|------|---------|-------------|---------|
| **Keirox** | Red-team proxy (HTTP/SOCKS5, TLS MITM) | ✅ crates.io | ✅ default |
| **Termino** | Secure terminal mesh (onion routing) | ✅ crates.io | ✅ default |
| **SigMatrix** | Detection rule engine (Sigma → backends) | ✅ crates.io | ✅ default |
| **GhostPacket** | Packet analysis (PCAP, dissectors) | ✅ crates.io | ✅ default |
| **MemoryHound** | Memory forensics (Windows dumps) | ✅ crates.io | ✅ default |
| **RedOps** | Adversary emulation (Atomic Red Team) | ✅ crates.io | ✅ default |

---

## Security Model

### Kernel Hardening
- KASLR: Kernel base address randomized on boot
- SMEP: Prevents kernel from executing userland code
- SMAP: Prevents kernel from reading userland memory
- W^X: Code pages are either writable or executable, never both
- kptr_restrict: Kernel pointers hidden from /proc
- lockdown module: Prevents modifying kernel state

### Userspace Hardening
- GCC stack protector on all binaries
- FORTIFY_SOURCE on all C code
- RELRO (Full) on all binaries
- PIE (Position Independent Executable) on all binaries
- seccomp-bpf on all daemons
- No privileged containers
- AppArmor profiles on all services
- UEFI Secure Boot (signed GRUB + kernel)

### Network Hardening
- No IPv6 router advertisements accepted
- SYN cookies enabled by default
- IP forwarding disabled by default
- Firewall: nftables rules locked after boot

---

## Build System

### ISO Build Pipeline

```
Source Code → Build Scripts → Reproducible ISO → Signed Release
     ↑                                              ↓
     └────────── Verification (contributors) ──────┘
```

1. **Build environment:** Docker container with locked toolchain (Rust nightly, musl, xorriso, grub2)
2. **Build process:** Fully scripted via `keironiso build` command
3. **Artifact:** ISO file + SHA256 hash + GPG signature
4. **Verification:** Any contributor can run `keironiso verify` and confirm binary == source

### CI/CD Pipeline (GitHub Actions)

| Trigger | Action |
|---------|--------|
| Every PR | Rustfmt + clippy + cargo test on all repos |
| Every PR on kernel | QEMU boot test (boots to login prompt) |
| Every merge to main | Nightly ISO build |
| Every merge to stable | Weekly ISO build |
| Every release tag | Signed release artifacts published |

---

## Comparison with Existing Distros

| Feature | Keiron Linux | Kali Linux | Tails | Qubes OS |
|---------|-------------|------------|-------|----------|
| Memory-safe kernel | ✅ Rust | ❌ C | ❌ Linux | ❌ Linux |
| Reproducible builds | ✅ | ❌ | ❌ | ❌ |
| Signed packages | ✅ | ✅ | ✅ | ✅ |
| Rust-first toolchain | ✅ | ❌ | ❌ | ❌ |
| Live USB | ✅ | ✅ | ✅ | ❌ |
| Hardened by default | ✅ | Partial | ✅ | ✅ |
| EDR built-in | ✅ | ❌ | ❌ | ❌ |
| No systemd | ✅ | ❌ | ❌ | ✅ |
| Custom package manager | ✅ | ❌ (apt) | ❌ (apt) | ❌ (dnf) |

---

## What Makes It Different

1. **Rust in the kernel.** Not a Linux distro with Rust tools. An actual OS with a Rust kernel. This is the hardest thing to build and the most impressive thing to have built.

2. **Reproducible builds.** The ISO you download is verifiable against the source anyone can build themselves.

3. **No abandoned tools.** Every tool ships with CI, tests, documentation, and an active maintainer.

4. **Production hardening from day one.** KASLR, SMEP, SMAP, seccomp, AppArmor — all on by default, not opt-in.

5. **Named after a person.** This is Keiron's OS. It carries a name, a reputation, and a direct connection to the builder.

---

*Last updated: May 2026*
*Architecture version: 1.0*