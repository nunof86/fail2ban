# Documentation

## See the full documentation on https://documentation-com.gitbook.io/fail2ban-installation/

# Prerequisites

## System Update

```bash
sudo apt update && sudo apt full-upgrade -y
```

## Fail2ban Installation

```bash
sudo apt install fail2ban -y
```

## Ansible Installation

```bash
sudo apt install ansible -y
```

# Fail2ban Configuration

## Backup the Configuration Files

```bash
sudo cp /etc/fail2ban/fail2ban.conf /etc/fail2ban/fail2ban.local
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

## Changing the Bantime in the jail.conf Configuration File

1. Edit the file with <mark style="color:red;">`nano /etc/fail2ban/jail.conf`</mark>.
2. Change the <mark style="color:red;">`bantime  = 10m`</mark> to <mark style="color:red;">`bantime  = 60m`</mark>.

```
bantime  = 60m
```

## Changing the Maxretry in the jail.conf Configuration File

1. Edit the file with <mark style="color:red;">`nano /etc/fail2ban/jail.conf`</mark>.
2. Change the <mark style="color:red;">`maxretry = 5`</mark> to <mark style="color:red;">`maxretry = 5`</mark>.

## Enable and Start the Fail2ban service

```bash
systemctl enable fail2ban
systemctl restart fail2ban
```
