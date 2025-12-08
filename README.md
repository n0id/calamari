# Calamari - Host Internet Access Lockdown System

A security-focused tool that implements an **extremely restrictive** network environment where **nothing on the host can access the internet by default**. All outbound internet access must be explicitly configured to use the Squid proxy, creating a "default deny" posture where applications cannot phone home without permission.

## 🚨 Security Philosophy

Unlike transparent proxy setups, Calamari takes a **hardened approach**:
- **Default Deny**: No process can reach the internet unless explicitly configured
- **No Leaks**: Even if malware executes, it cannot discover or access internet connectivity
- **Intentional Access**: Applications must be explicitly configured with proxy settings (e.g., `http_proxy`, `https_proxy` environment variables)
- **Process Isolation**: Only specific service users (proxy, dnsmasq, chrony) have raw network access

This is ideal for:
- Malware analysis sandboxes
- Security research environments  
- High-security workstations
- Preventing software telemetry/data exfiltration

## ⚠️ Critical Warning

This tool will **block all outgoing internet access** except through the configured proxy. Before enabling:
1. Ensure you have console/local access
2. Understand how to configure applications to use the proxy
3. Test in a non-production environment first
4. Have a recovery plan (script includes `off` command to remove rules)

## ✨ Features

- **Total Outbound Block**: All processes denied internet access by default
- **Proxy-Only Internet**: Internet access ONLY via explicit proxy configuration
- **DNS Control**: All DNS forced through local DNSMasq
- **Service Isolation**: Only proxy, DNS, and NTP service users can make outbound connections
- **Selective Exceptions**: Optionally allow SSH for specific users
- **Domain Blacklisting**: Granular control over what domains Squid permits
- **Audit Logging**: Full visibility into all internet access attempts
- **Temporary Testing**: Apply rules temporarily or commit permanently

## 📦 Prerequisites

- Debian-based Linux distribution
- Root/sudo access
- Basic understanding of proxy configuration

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/n0id/calamari.git
cd calamari

# Make script executable
chmod +x calamari

# Install dependencies and apply temporary rules
sudo ./calamari on
