<!-- Test: Dit is een private wijziging -->
# TransIP VPS Configuration

## Document Information

| Item | Details |
|------|---------|
| **Version** | 1.0.0 |
| **Last Updated** | 2026-01-29 |
| **Author** | Willem de Vries |
| **Status** | Active |
| **Versioning** | Semantic Versioning (Major.Minor.Patch) |

**Version Numbering Guidelines:**
- **Major (X.0.0)** - Major changes, restructuring, new major sections
- **Minor (0.X.0)** - Additions, new subsections, significant content updates
- **Patch (0.0.X)** - Minor corrections, typos, formatting improvements

## Version History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0.0 | 2026-01-29 | Willem de Vries | Initial documentation: VPS setup, SSH access, Nginx configuration, DNS setup, SSL/HTTPS with Let's Encrypt, firewall configuration, and decommissioning procedures |

[TOC]

## VPS Details

- **Provider:** TransIP
- **Operating System:** Ubuntu 24.04
- **IP Address:** 37.97.201.75
- **Main User:** Configured during installation (name provided)
- **Authentication:** SSH key authentication configured during VPS initialization (no password set)

## VPS Access

### SSH Authentication

TransIP does **not install a default password** for the user with Ubuntu VPS installations. Instead, they work with **SSH key authentication**.

### Configuring SSH Access

**Access options:**

1. **Add SSH key via TransIP control panel:**
   - Log in to your TransIP account
   - Go to your VPS in the control panel
   - Look for the "SSH Keys" or "Access" section
   - Add your public SSH key there

2. **Alternative: Root access via console:**
   - TransIP usually offers web-based console/VNC access in the control panel
   - This allows you to log in without SSH
   - Through this console you can then set a password or configure SSH keys

3. **Set password (if needed):**
   Once logged in via console or SSH key:
   ```bash
   sudo passwd yourmainuser
   ```

### Starting SSH Session with Specific Key File

You can start an SSH session with a specific key file using the `-i` option:

```bash
ssh -i /path/to/your/private_key username@hostname
```

For example:

```bash
ssh -i ~/.ssh/my_special_key ubuntu@37.97.201.75
```

**Some tips:**

- The key file must have the correct permissions (only readable by you):
  ```bash
  chmod 600 ~/.ssh/your_private_key
  ```

- If you regularly use the same key for the same host, you can configure this in `~/.ssh/config`:
  ```
  Host myserver
      HostName 37.97.201.75
      User ubuntu
      IdentityFile ~/.ssh/my_special_key
  ```
  Then you can simply use `ssh myserver`.

- You can also try multiple keys by adding multiple `-i` options:
  ```bash
  ssh -i ~/.ssh/key1 -i ~/.ssh/key2 user@host
  ```

## Resolving SSH Host Key Problem

### Error Message

During first login attempt after VPS installation:

```
The fingerprint for the ED25519 key sent by the remote host is
SHA256:0FlK9AFavj+jfqRQBwH5yH4q0Lg4DfCwssWsdINXKkU.
Please contact your system administrator.
Add correct host key in C:\Users\WillemdeVries/.ssh/known_hosts to get rid of this message.
Offending ED25519 key in C:\Users\WillemdeVries/.ssh/known_hosts:11
Host key for 37.97.201.75 has changed and you have requested strict checking.
Host key verification failed.
```

### Solution

This error message means that the SSH host key of your server has changed. This often happens when you have reinstalled a VPS or received a new VPS on the same IP address.

You need to remove the old host key from your `known_hosts` file. There are two ways:

**Option 1: Remove specific entry (recommended)**
```bash
ssh-keygen -R 37.97.201.75
```

**Option 2: Manual editing**
Open `C:\Users\WillemdeVries\.ssh\known_hosts` in a text editor and delete line 11 (as indicated in the error message).

**Afterwards:**
Try logging in again:
```bash
ssh username@37.97.201.75
```

You will now get a question whether you want to accept the new fingerprint:
```
The authenticity of host '37.97.201.75' can't be established.
ED25519 key fingerprint is SHA256:0FlK9AFavj+jfqRQBwH5yH4q0Lg4DfCwssWsdINXKkU.
Are you sure you want to continue connecting (yes/no)?
```

Type `yes` and press Enter.

**Note:** This error message can also be a sign of a "man-in-the-middle" attack, but in this case it is most likely simply because TransIP performed a new Ubuntu installation.

## System Updates

### APT Update and Upgrade

Updating the operating system:

```bash
sudo apt update
sudo apt upgrade
```

### Phased Updates Message

After the command `sudo apt upgrade` the following message appeared:

```
The following upgrades have been deferred due to phasing:
  fwupd libfwupd2
```

**What does this mean?**

This message is normal and nothing to worry about. It concerns Ubuntu's **phased updates** system.

Ubuntu rolls out some updates in phases ("phasing"). This means that updates first go to a small percentage of users, and are gradually rolled out to more systems. This helps detect problems with updates early before they reach everyone.

**What can you do?**

**Option 1: Just wait (recommended)**
The updates will automatically become available for your system within a few days/weeks.

**Option 2: Force installation now**
If you want the updates immediately:
```bash
sudo apt install fwupd libfwupd2
```

Or for all deferred updates:
```bash
sudo apt upgrade --with-new-pkgs
```

**Option 3: Disable phasing permanently**
If you always want all updates immediately (less safe):
```bash
sudo apt install apt-listchanges
```
And add to `/etc/apt/apt.conf.d/99-phasing`:
```
APT::Get::Always-Include-Phased-Updates "true";
```

For a VPS it is usually fine to just choose option 1 and wait. The packages `fwupd` and `libfwupd2` are firmware update tools that are usually not very relevant on a VPS anyway.

## Nginx Web Server

### Installation

Nginx is installed as web server.

### Useful First Steps

**1. Check if Nginx is running:**
```bash
sudo systemctl status nginx
```

**2. Make sure Nginx starts automatically on reboot:**
```bash
sudo systemctl enable nginx
```

**3. Configure firewall (if ufw is active):**
```bash
sudo ufw allow 'Nginx Full'
# Or specifically:
sudo ufw allow 80/tcp    # HTTP
sudo ufw allow 443/tcp   # HTTPS
```

**4. Test in your browser:**
Go to `http://37.97.201.75` - you should see the default Nginx welcome page.

**5. Important locations:**
- Config: `/etc/nginx/nginx.conf`
- Site configs: `/etc/nginx/sites-available/` and `/etc/nginx/sites-enabled/`
- Webroot (default): `/var/www/html/`
- Logs: `/var/log/nginx/`

**6. Useful commands:**
```bash
sudo nginx -t                    # Test configuration
sudo systemctl reload nginx      # Reload config (without downtime)
sudo systemctl restart nginx     # Restart service
```

## DNS and Domain Configuration

### Domain Information

- **Domain:** motoppdemo.nl
- **Existing entry:** www-entry pointing to another VPS
- **New subdomain:** eap-it32.motoppdemo.nl
- **Target IP:** 37.97.201.75

### DNS Configuration

**Step 1: Add DNS A-record at TransIP**

Log in to TransIP DNS management and add:
- **Type:** A
- **Name:** eap-it32
- **Value:** 37.97.201.75
- **TTL:** 3600 (or default)

### Nginx Virtual Host Configuration

**Step 2: Create new server block configuration**

Create a new server block configuration:

```bash
sudo nano /etc/nginx/sites-available/eap-it32.motoppdemo.nl
```

Add:
```nginx
server {
    listen 80;
    listen [::]:80;
    
    server_name eap-it32.motoppdemo.nl;
    
    root /var/www/eap-it32.motoppdemo.nl;
    index index.html index.htm;
    
    location / {
        try_files $uri $uri/ =404;
    }
}
```

**Step 3: Create webroot**

```bash
sudo mkdir -p /var/www/eap-it32.motoppdemo.nl
sudo chown -R $USER:$USER /var/www/eap-it32.motoppdemo.nl
```

**Step 4: Create test page**

```bash
echo '<h1>eap-it32.motoppdemo.nl werkt!</h1>' > /var/www/eap-it32.motoppdemo.nl/index.html
```

**Note:** Use single quotes (`'`) instead of double quotes (`"`) to avoid bash history expansion issues with the exclamation mark. In double quotes, bash tries to interpret `!` as a history expansion command.

**Step 5: Activate site**

```bash
sudo ln -s /etc/nginx/sites-available/eap-it32.motoppdemo.nl /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

Wait 5-10 minutes until DNS has propagated, then `http://eap-it32.motoppdemo.nl` should work.

## SSL/HTTPS Configuration with Let's Encrypt

### Installing Certbot

**Step 1: Install Certbot and Nginx plugin**

```bash
sudo apt update && sudo apt install certbot python3-certbot-nginx -y
```

### Obtaining SSL Certificate

**Step 2: Request SSL certificate and automatically configure Nginx**

```bash
sudo certbot --nginx -d eap-it32.motoppdemo.nl
```

During the process you will be asked:
1. **Email address** (for important notifications and certificate expiration warnings)
2. **Accept Terms of Service** - type `Y`
3. **Share email with EFF** (optional) - type `Y` or `N`
4. **Redirect HTTP to HTTPS** - choose `2` (redirect, recommended)

### Nginx Configuration After SSL Installation

After Certbot completes, the Nginx configuration is automatically updated to:

```nginx
server {
    server_name eap-it32.motoppdemo.nl;
    root /var/www/eap-it32.motoppdemo.nl;
    index index.html index.htm;
    location / {
        try_files $uri $uri/ =404;
    }
    listen [::]:443 ssl ipv6only=on; # managed by Certbot
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/eap-it32.motoppdemo.nl/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/eap-it32.motoppdemo.nl/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}
server {
    if ($host = eap-it32.motoppdemo.nl) {
        return 301 https://$host$request_uri;
    } # managed by Certbot
    listen 80;
    listen [::]:80;
    server_name eap-it32.motoppdemo.nl;
    return 404; # managed by Certbot
}
```

**What Certbot automatically configured:**
1. Added port 443 (HTTPS) for both IPv4 and IPv6
2. Configured SSL certificates
3. Set up HTTP to HTTPS redirect (301 permanent redirect)
4. Applied secure SSL settings

### Certificate Renewal

**Step 3: Test automatic renewal**

Let's Encrypt certificates are valid for 90 days. Certbot automatically installs a cronjob for renewal. Test if this works:

```bash
sudo certbot renew --dry-run
```

Expected output:
```
Saving debug log to /var/log/letsencrypt/letsencrypt.log
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/eap-it32.motoppdemo.nl.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Account registered.
Simulating renewal of an existing certificate for eap-it32.motoppdemo.nl
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Congratulations, all simulated renewals succeeded:
  /etc/letsencrypt/live/eap-it32.motoppdemo.nl/fullchain.pem (success)
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```

### Firewall Configuration

**Step 4: Verify firewall settings**

Check firewall status:

```bash
sudo ufw status
```

Current firewall configuration:
```
Status: active
To                         Action      From
--                         ------      ----
80/tcp                     ALLOW       Anywhere
443/tcp                    ALLOW       Anywhere
OpenSSH                    ALLOW       Anywhere
Nginx Full                 ALLOW       Anywhere
80/tcp (v6)                ALLOW       Anywhere (v6)
443/tcp (v6)               ALLOW       Anywhere (v6)
OpenSSH (v6)               ALLOW       Anywhere (v6)
Nginx Full (v6)            ALLOW       Anywhere (v6)
```

The firewall is active and correctly configured with:
- SSH (OpenSSH) access
- HTTP (port 80) for both IPv4 and IPv6
- HTTPS (port 443) for both IPv4 and IPv6
- Nginx Full profile (covers both HTTP and HTTPS)

**Note:** If firewall was inactive, you would enable it with:
```bash
sudo ufw allow OpenSSH
sudo ufw allow 'Nginx Full'
sudo ufw enable
```

### Verification

After SSL installation, `https://eap-it32.motoppdemo.nl` should work with a valid SSL certificate and automatic redirect from HTTP to HTTPS.

## Decommissioning a VPS

When you need to permanently shut down a VPS, follow these steps:

### At the VPS Provider (TransIP)

1. **Create snapshot/backup** if you want to preserve any data
   - Do this through the TransIP control panel before canceling
   
2. **Remove SSH keys from TransIP control panel**
   - Remove SSH keys of users who have left or no longer need access
   - Go to the VPS settings in TransIP control panel
   - Remove all SSH keys that were added for this VPS
   
3. **Cancel/delete the VPS** via the control panel
   - Without this step, you will continue to be charged
   
4. **IP address release** (usually happens automatically upon cancellation)

### DNS Configuration

5. **Remove or modify DNS records** in TransIP DNS management
   - Remove A records pointing to the old VPS IP
   - Remove AAAA records pointing to the old VPS IP
   - Otherwise these will continue pointing to a non-existent IP address

### SSL Certificates

6. **Certificates are automatically removed** when the VPS is deleted
7. No further action needed - Let's Encrypt certificates will expire automatically

### Optional - If Sensitive Data Present

8. **Wipe data** before deleting the VPS (though TransIP normally does this)
9. **Revoke SSH keys** that were specific to that VPS

### Checklist Before Decommissioning

Before shutting down a VPS, ensure:
- ✓ All services you want to keep have been migrated to another VPS
- ✓ Backup/snapshot created if data needs to be preserved
- ✓ DNS records removed or updated to point to new locations
- ✓ Users/stakeholders notified if services will be unavailable
- ✓ VPS cancellation submitted through TransIP control panel

## Next Steps

Possible next configuration steps:

- Further security configuration
- Deploy applications
