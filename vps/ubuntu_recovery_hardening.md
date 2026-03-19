# Ubuntu Server Recovery & Hardening Notes

## 1. Situation Overview

You had a **TransIP VPS** running **Ubuntu Server 24.04** and accessed it via **rescue mode**.  
You reset the **root password** and discovered there was **no normal user** on the system.

Relevant notes:

- Some VPS images ship with **only root**
- Some ship with a **default user** (e.g., `ubuntu`)
- Your system had **no users under `/home`**

---

## 2. Checking for Existing Users

### List all home directories:

```bash
ls -l /home
```

If empty → no normal interactive users.

### Find users with user IDs (UID) ≥ 1000:

```bash
awk -F: '$3>=1000 && $3<2000 {print $1}' /etc/passwd
```

Typical behavior:

- UID **1000** = first normal user
- UID **1001** = next normal user if 1000 is taken

In your case, the new user got **UID 1001**, which is **normal**.

---

## 3. Rescue Mode Context (TransIP)

If you boot into rescue & want to modify the real filesystem:

```bash
mount /dev/sda1 /mnt
mount --bind /dev /mnt/dev
mount --bind /proc /mnt/proc
mount --bind /sys /mnt/sys
chroot /mnt
```

After `chroot`, you are operating inside the **real** system.

---

## 4. Creating a Normal Admin User

### Case: `adduser` errors with `group admin already exists`

You can either:

#### A. Use a different username:

```bash
adduser sysadmin
usermod -aG sudo sysadmin
```

#### B. Reuse the group `admin` manually:

```bash
adduser --ingroup admin admin
usermod -aG sudo admin
```

### If `adduser` is missing

Use low-level `useradd`:

```bash
useradd -m admin
passwd admin
usermod -aG sudo admin
```

### Verify user & groups:

```bash
id admin
```

Expected output example:

```
uid=1001(admin) gid=1001(admin) groups=1001(admin),27(sudo)
```

---

## 5. Why UID=1001 is Normal

Linux allocates UIDs:

- `0` = `root`
- `1–999` = system/service accounts
- `1000+` = normal users

If UID `1000` is taken (even by a deleted user entry), next becomes `1001`.

Check who owns UID 1000:

```bash
awk -F: '$3==1000 {print $1}' /etc/passwd
```

---

## 6. VPS Hardening Checklist (Ubuntu 24.04)

Below is a practical hardening checklist for public VPS deployments.

---

### **6.1 SSH Access Hardening**

#### Use SSH Keys

Local machine:

```bash
ssh-keygen -t ed25519
```

Copy key:

```bash
ssh-copy-id <user>@<server-ip>
```

#### Disable password login

Edit:

```bash
sudo nano /etc/ssh/sshd_config
```

Set:

```
PasswordAuthentication no
PermitEmptyPasswords no
```

#### Disable root SSH login

In same file:

```
PermitRootLogin no
```

Restart SSH:

```bash
sudo systemctl restart ssh
```

---

### **6.2 Firewall (UFW)**

Install & configure:

```bash
sudo apt update
sudo apt install ufw
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp   # allow SSH
sudo ufw enable
```

Verify:

```bash
sudo ufw status verbose
```

---

### **6.3 Fail2ban**

Install:

```bash
sudo apt install fail2ban
```

Configure:

```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

In `/etc/fail2ban/jail.local`:

```
[sshd]
enabled = true
maxretry = 4
bantime = 1h
findtime = 10m
```

Restart:

```bash
sudo systemctl restart fail2ban
```

Check:

```bash
sudo fail2ban-client status sshd
```

---

### **6.4 System & Kernel Security**

Update:

```bash
sudo apt update && sudo apt upgrade -y
```

Enable unattended upgrades:

```bash
sudo apt install unattended-upgrades
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

Enable Canonical Livepatch (optional):

```bash
sudo snap install canonical-livepatch
```

---

### **6.5 Sysctl Hardening**

Create:

```bash
sudo nano /etc/sysctl.d/99-security.conf
```

Add:

```
kernel.kptr_restrict = 2
kernel.yama.ptrace_scope = 2
net.ipv4.conf.all.rp_filter = 1
net.ipv4.conf.default.rp_filter = 1
net.ipv4.tcp_syncookies = 1
net.ipv4.ip_forward = 0
```

Apply:

```bash
sudo sysctl --system
```

---

### **6.6 Optional Network Restrictions**

Allow only specific IP:

```bash
sudo nano /etc/hosts.allow
```

Example:

```
sshd: 203.0.113.42
```

Deny all others:

```bash
sudo nano /etc/hosts.deny
```

```
sshd: ALL
```

---

## 7. Validation Checklist

After changes, verify:

- [ ] SSH login works as unprivileged user
- [ ] Root SSH login is disabled
- [ ] Password SSH login is disabled
- [ ] UFW active and restrictive
- [ ] Fail2ban running
- [ ] Packages updated
- [ ] No unnecessary services running

SSH test:

```bash
ssh -i ~/.ssh/id_ed25519 <user>@<server-ip>
```

---

## 8. Tools & Logs

Useful commands:

| Purpose | Command |
|---|---|
| UFW logs | `/var/log/ufw.log` |
| SSH logs | `/var/log/auth.log` |
| Fail2ban logs | `/var/log/fail2ban.log` |

Optional monitoring tools:

```bash
sudo apt install htop iotop iftop net-tools
```

---

## End of Document
