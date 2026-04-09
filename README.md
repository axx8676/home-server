# Home Server Setup Guide (Ubuntu + Docker + Tailscale)

This guide documents the full process to rebuild your home server from scratch. It covers hardware prep, OS installation, networking, storage, Docker, and Tailscale.

---

# 1. Prerequisites

## Hardware

* Server machine (Intel NUC or similar)
* SSD installed
* USB flash drive (8GB+)
* Another computer for setup
* Network access (Ethernet preferred for setup)

---

## Software to Download (on your main PC)

### 1. Ubuntu Server ISO

* Go to: https://ubuntu.com/download/server
* Download latest LTS (e.g., 24.04 LTS)

---

### 2. Rufus (for creating boot USB)

* Go to: https://rufus.ie
* Download portable version

---

# 2. Create Bootable USB

1. Insert USB drive
2. Open Rufus
3. Select:

   * Device: your USB
   * Boot selection: Ubuntu ISO
4. Click **Start**
5. Use default settings

---

# 3. Install Ubuntu Server

## Boot into installer

1. Insert USB into server
2. Power on
3. Enter boot menu (usually F2/F10/F12) <-- fix when i find out which it is
4. Select USB device

---

## Installation steps

---

### Network setup (IMPORTANT)

If using Ethernet:

* It should auto-connect → continue

If using WiFi:

* Select WiFi network - axx8676
* Enter password - elect3524bottle

---

### Storage setup

Choose:

```
Use entire disk
```

Then:

```
Use LVM (recommended)
```

This creates:

* `/boot`
* `/boot/efi`
* LVM partition

---

### User setup

Create:

* Username (axx8676)
* Password (same as work pw)
* Hostname (`axel-home-server`)

---

### SSH setup

* Install OpenSSH server → YES

---

### Finish install

* Remove USB when prompted
* Reboot

---

# 4. First Boot Setup

Login with your user.

---

## Update system

```bash
sudo apt update
sudo apt upgrade -y
```

---

## Install basic tools

```bash

```

---

# 5. Fix Disk Space (LVM Expansion)

After install, Ubuntu may only use part of the disk.

## Check layout

```bash
lsblk
```

---

## Expand LVM to full disk

### Step 1: Expand logical volume

```bash
sudo lvextend -l +90%FREE /dev/ubuntu-vg/ubuntu-lv
```

### Step 2: Resize filesystem

```bash
sudo resize2fs /dev/ubuntu-vg/ubuntu-lv
```

---

## Verify

```bash
df -h
```

---

# 6. Set Up Networking (WiFi if needed)

If WiFi wasn’t configured:

Edit netplan config:

```bash
sudo nano /etc/netplan/*.yaml
```

Example:

```yaml
network:
  version: 2
  wifis:
    wlan0:
      dhcp4: true
      access-points:
        "YOUR_WIFI_NAME":
          password: "YOUR_PASSWORD"
```

Apply:

```bash
sudo netplan apply
```

Restart to ensure changes have applied

---

# 7. Setup Drives

```bash
blkid
```

Edit:

```bash
sudo nano /etc/fstab
```

Add:

```
UUID=xxxx /mnt/storage ext4 defaults 0 2
```

Install ZFS
```bash
sudo apt install zfsutils-linux
```

Identify Drives
```bash
lsblk
```
Example: /dev/sdb

Create the mirror pool
```bash
sudo zpool create tank mirror /dev/sdX /dev/sdY
```

Create folders for dockers
```bash
sudo zfs create tank/media
sudo zfs create tank/media/movies
sudo zfs create tank/media/shows
sudo zfs create tank/media/music
sudo zfs create tank/nextcloud
sudo zfs create tank/nextcloud/pictures
sudo zfs create tank/downloads
```

Check status
```bash
zpool status
```

# 8. Install Docker

## Install Docker

Add Docker's official GPG key:
```bash
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Add the repository to Apt sources:
```bash
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
```

Install latest packages:
```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Verify Docker is running:
```bash
sudo systemctl status docker
```
If not running:
```bash
sudo systemctl start docker
```

Verify installation is successful:
```bash
sudo docker run hello-world
```

Install docker-compose plugin:
```bash
sudo apt-get update
sudo apt-get install docker-compose-plugin
```

Verify installation is successful:
```bash
docker compose version
```

---

## Add user to docker group

```bash
sudo usermod -aG docker $USER
```

Then log out and back in.

---

# 9. Restore Your GitHub Repo

## Clone your repo

```bash
git clone <YOUR_GITHUB_REPO_URL>
cd <repo-folder>
```

---

## Start containers

```bash
docker compose up -d
```

---

## Verify containers

```bash
docker ps
```

---

# 10. Install Tailscale

## Install

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

---

## Start service

```bash
sudo systemctl enable tailscaled
sudo systemctl start tailscaled
```

---

## Authenticate

```bash
sudo tailscale up
```

* Follow login link
* Approve device

---

## Verify connection

```bash
tailscale status
```

---

# 12. Recommended Settings

## Enable Tailscale on boot

```bash
sudo systemctl enable tailscaled
```

---

## Enable Docker on boot

```bash
sudo systemctl enable docker
```

---

## BIOS setting (IMPORTANT)

Set:

```
Restore on AC Power Loss → Power On
```

---

# 13. Troubleshooting

## Check logs

```bash
journalctl -xe
```

---

## Check previous boot (crash debugging)

```bash
journalctl -b -1
```

---

## Check Tailscale logs

```bash
journalctl -u tailscaled
```

---

## Check disk usage

```bash
df -h
```

---

# 15. Quick Rebuild Checklist

1. Flash Ubuntu USB
2. Install OS (LVM enabled)
3. Update system
4. Expand SSD if needed (lvextend + resize2fs)
5. Setup drives and mirroring
6. Install Docker + Compose
7. Clone repo
8. Start containers
9. Install Tailscale
10. Verify remote access

---

# End
