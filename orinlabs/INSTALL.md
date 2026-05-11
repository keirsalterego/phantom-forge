# Orin Labs — Installation Guide

> *"Getting started should be the easiest step."*

---

## Prerequisites

### Hardware Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| CPU | x86_64 (64-bit) | x86_64 with APIC |
| RAM | 2 GB | 4 GB+ |
| Storage | 20 GB | 50 GB+ SSD |
| Network | Ethernet | Ethernet + WiFi (post-v1.1) |
| USB | 2 GB (for live boot) | 8 GB+ |

**Note:** aarch64 support is planned for v1.2. For now, x86_64 only.

**Confirmed working hardware (v1.0):**

| Model | CPU | Notes |
|-------|-----|-------|
| Dell Latitude 5490 | i5-8250U | Works out of box |
| Lenovo ThinkPad T480 | i5-8350U | Works out of box |
| HP EliteBook 840 G5 | i5-8365U | Works out of box |
| Lenovo ThinkPad X1 Carbon Gen 6 | i5-8250U | Works out of box |

**Known issues (v1.0):**

- Some older Intel iGPU (Skylake and earlier) may have display issues — use QEMU/KVM for testing
- NVIDIA GPUs: nouveau may be unstable, proprietary driver not included
- AMD GPU: amdgpu in Vale, should work

---

## Option 1: Live USB (Try Without Installing)

### What You Need

- USB drive (2 GB minimum, 8 GB recommended)
- balenaEtcher or `dd` on Linux/macOS
- orinlabs-v1.0.0-x86_64.iso

### Steps

**On Linux/macOS:**

```bash
# Find your USB device (be VERY careful — this will DESTROY data)
lsblk

# Example output:
# sda         8G   ← 8GB USB drive

# Write the ISO (replace sdX with your device, e.g., sdb)
sudo dd if=orinlabs-v1.0.0-x86_64.iso of=/dev/sdX bs=4M status=progress

# Sync to ensure all data is written
sync
```

**On Windows:**

1. Download balenaEtcher from https://etcher.balena.io
2. Open balenaEtcher
3. Click "Flash from file" → select the ISO
4. Click "Select target" → select your USB drive
5. Click "Flash!" — wait for it to complete
6. Remove USB drive safely

**On macOS:**

```bash
# Find the USB device
diskutil list

# Unmount (replace N with disk number)
diskutil unmountDisk /dev/diskN

# Write ISO (replace N with disk number)
sudo dd if=orinlabs-v1.0.0-x86_64.iso of=/dev/diskN bs=4m status=progress
```

### Boot from USB

1. Insert USB drive
2. Restart machine
3. Press the boot menu key (F12 on Dell/Lenovo, Esc on HP, F2 to enter setup)
4. Select USB device from boot menu
5. Orin Labs boots to a login prompt

**Default credentials (Live mode):**
```
Username: root
Password: keiron
```

> ⚠️ Change this password immediately on first boot: `passwd`

### Live Mode Features

- Full tool suite available (all 6 tools pre-installed)
- Changes persist to RAM (lost on reboot)
- To install packages: `loom update && loom install <package>`
- WiFi: `wpa_passphrase 'SSID' 'password' > /etc/wpa.conf && wpa_supplicant -B -i wlan0 -c /etc/wpa.conf && dhcpcd wlan0`

---

## Option 2: Install to Disk

### Option 2a: Full Disk Install (Erases Everything)

> ⚠️ This will delete all data on the target disk. Back up first.

1. Boot from Live USB (see above)
2. Login as root
3. Run the installer:

```bash
orin-install --full-disk
```

4. Select target disk (e.g., `/dev/sda`)
5. Confirm: type `YES` in all caps
6. Wait for installation to complete (5–15 minutes)
7. Remove USB drive
8. Reboot

**What the installer does:**
- Creates GPT partition table
- Creates EFI system partition (512 MB, FAT32)
- Creates root partition (rest of disk, ext4)
- Installs bootloader (GRUB2, UEFI)
- Installs Vale + initramfs
- Creates base userland (musl, busybox, runit)
- Installs default packages (all 6 tools)
- Sets up networking (DHCP on Ethernet)
- Creates first user account

### Option 2b: Dual Boot (Keep Existing OS)

> ⚠️ Dual boot is advanced. Only proceed if you know how to fix your bootloader.

1. Boot from Live USB
2. Login as root
3. Run the installer:

```bash
orin-install --dual-boot
```

4. Select target disk
5. Select or create partition (minimum 20 GB)
6. DO NOT install GRUB to MBR — install to the partition boot sector
7. Note the partition UUID
8. From your existing OS (Linux), add Orin Labs to GRUB:

```bash
# In your existing Linux (e.g., Ubuntu)
sudo nano /etc/grub.d/40_custom

# Add this entry (replace UUID with your actual root partition UUID):
menuentry 'Orin Labs' {
    set root='hd0,gpt2'  # adjust to your partition
    linux /boot/vmlinuz root=UUID=YOUR-UUID-HERE ro
    initrd /boot/initramfs
}

# Update GRUB
sudo update-grub
```

### Option 2c: Virtual Machine (QEMU/KVM)

**QEMU (fastest setup):**

```bash
# Install QEMU
sudo apt install qemu-system-x86_64

# Download the ISO (or use local file)
# Run the VM
qemu-system-x86_64 \
    -m 4G \
    -cdrom orinlabs-v1.0.0-x86_64.iso \
    -boot d \
    -enable-kvm \
    -cpu host \
    -smp 4
```

**Libvirt/Virt-Manager:**

1. Open Virt-Manager
2. File → New Virtual Machine
3. Select "Import existing disk image"
4. Browse → select the ISO (or create a Storage Pool pointing to the ISO location)
5. OS type: Linux / Generic / Generic 64-bit
6. Allocate RAM and CPU
7. Finish → Start VM

**VirtualBox:**

1. New → Linux → Other Linux (64-bit)
2. Allocate RAM (4 GB recommended)
3. Do not add virtual disk (use live ISO)
4. Settings → Storage → IDE Controller → Add CD/DVD Device → Select ISO
5. Start VM

---

## First Boot (Installed System)

1. On first boot, you will see the Orin Labs welcome screen
2. Create your user account:

```bash
# As root, create your user
adduser keiron
usermod -aG wheel,adm,audio,video,usb keiron

# Configure sudo (vi editor opens)
visudo
# Uncomment: %wheel ALL=(ALL) ALL
```

3. Set your timezone:

```bash
ln -sf /usr/share/zoneinfo/Europe/London /etc/localtime
```

4. Configure hostname:

```bash
echo "keiron-laptop" > /etc/hostname
# Edit /etc/hosts to add: 127.0.1.1 keiron-laptop
nano /etc/hosts
```

5. Configure networking:

```bash
# Ethernet (DHCP — usually works automatically)
dhcpcd

# Or static IP:
nano /etc/network.conf
# Add:
# interface eth0
# static ip=192.168.1.100/24
# gateway=192.168.1.1
# dns=1.1.1.1

# Restart networking
rc-service networking restart
```

6. Update packages:

```bash
loom update
loom upgrade
```

---

## Post-Installation Checklist

- [ ] Changed root password
- [ ] Created user account with sudo access
- [ ] Set timezone correctly
- [ ] Configured hostname
- [ ] Configured network (Ethernet or WiFi)
- [ ] Updated all packages (`loom upgrade`)
- [ ] Configured firewall (nftables defaults are fine for most):
  ```bash
  # Default: deny incoming, allow outgoing
  nft list ruleset
  # To allow SSH:
  nft add rule inet filter input tcp dport 22 accept
  ```
- [ ] Enabled audit daemon:
  ```bash
  rc-update add auditd default
  rc-service auditd start
  ```
- [ ] Verified tools are working:
  ```bash
  drift --help
  terminokeiron --help
  sigmatrix --help
  ghostpacket --help
  memoryhound --help
  redops --help
  ```

---

## Troubleshooting

### "No bootable device found"

- Check if USB is set as first boot device in BIOS
- Check if Secure Boot is blocking the bootloader — disable it in BIOS
- If using QEMU: ensure you're booting in UEFI mode (OVMF)

### "Kernel panic — VFS: unable to mount root fs"

- Live boot only: the ISO was not written correctly. Re-write with `dd`
- Installed system: run `orin-checkboot` from the live USB to fix

### "Display not working"

- Try: `GRUB_CMDLINE_LINUX="nomodeset"` in /etc/default/grub, then `update-grub`
- If Intel iGPU on Skylake or earlier: this is a known issue. Use external GPU or QEMU.

### "Cannot connect to WiFi"

- WiFi driver not included in v1.0 (planned for v1.1). Use Ethernet for now.
- If on a machine with no Ethernet: the Live ISO will not work for you yet. Wait for v1.1.

### "Package installation fails"

- Check: `loom update` — index may be out of date
- Check: `curl -I https://packages.orinlabs.dev/` — network may be down
- Check: `dmesg | grep loom` — Vale log may have errors

### "Kernel OOM (Out of Memory)"

- Add more RAM in QEMU settings
- On real hardware: consider adding swap
  ```bash
  # Create 2GB swap file
  dd if=/dev/zero of=/swap bs=1M count=2048
  mkswap /swap
  swapon /swap
  # Make permanent:
  echo "/swap none swap sw 0 0" >> /etc/fstab
  ```

---

## Uninstallation

### Remove Orin Labs (keep other OS)

1. Boot from Live USB of another Linux distro
2. Use `gdisk` or `parted` to delete Orin Labs partitions
3. Run `grub-install` from your remaining OS to restore its bootloader
4. Resize remaining partitions to reclaim space

### Remove everything (clean disk)

From any Linux Live USB:

```bash
# Delete all partitions (replace sdX with your disk)
gdisk /dev/sdX
# Command: d (delete partition) — repeat until no partitions remain
# Command: w (write changes)

# Now disk is empty, use it as you like
```

---

## Upgrading

To upgrade from vX to vY (e.g., v1.0 to v1.1):

```bash
# Backup your data first!
loom update
loom install orin-upgrade
orin-upgrade --version v1.1.0
```

Or manual:

```bash
# Download new ISO
# Mount new ISO
# Copy Vale + initramfs to /boot
# Update /boot/grub/grub.cfg
# Reboot
```

---

*Last updated: May 2026*
*Installation version: 1.0*