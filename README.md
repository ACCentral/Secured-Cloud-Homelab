# Secure Cloud Homelab — Oracle Cloud Always Free

Infrastructure-as-Code and complete documentation for a highly secured, self-hosted ecosystem deployed on Oracle Cloud Infrastructure (OCI).

Operating at a strict **€0/month** cost (Always Free tier), this project demonstrates DevSecOps practices, strict network isolation, and immutable infrastructure principles.

## 🛡️ Architecture & Philosophy

*   **Zero Public Exposure:** The only open port to the public internet is a single WireGuard UDP port (47480).
*   **Cryptographic Filtering:** The server silently drops all packets that are not signed with a known WireGuard private key.
*   **State Separation:** Storage is strictly divided. The boot volume (`/var/lib/docker`, `/opt/stacks`) is treated as ephemeral/disposable, while application data is persisted on a dedicated, hardened `/srv` volume.
*   **Defense in Depth:** Security is layered across the OS, the firewall, and the container runtime.

## ⚙️ Technical Specifications

*   **Cloud Provider:** Oracle Cloud Infrastructure (OCI)
*   **Compute:** VM.Standard.A1.Flex (ARM Ampere, 2 OCPU, 12 GB RAM)
*   **OS:** Oracle Linux 9 (aarch64)
*   **Network:** Caddy Reverse Proxy (Port-based routing over VPN IP without DNS/TLS)
*   **Backups:** Restic (Encrypted, Deduplicated) targeting OCI Object Storage

## 🔒 Hardening Stance

*   **OS Level:** SELinux `Enforcing`, zero-downtime kernel patching (Ksplice), strict `auditd` logging covering 10 specific critical keys.
*   **Network Level:** Firewalld set to `drop` zone by default. A custom `DOCKER-USER` iptables chain prevents Docker daemon from bypassing system firewall rules.
*   **Container Level:** Containers are stripped of privileges (`cap_drop: [ALL]`), forced with `security_opt: [no-new-privileges:true]`, strictly memory-limited, and use a read-only Docker socket proxy.

## 🛠️ Stack Overview

*   **Tools:** IT-Tools, Memos, Stirling-PDF, SearXNG, CyberChef, n8n
*   **Storage & Media:** FileBrowser, MeTube
*   **Ops & Monitoring:** Dockge, Beszel, WUD (automated update tracking)

## 📚 Documentation

The complete step-by-step build guide (Phases 0 to 17), architectural decision records, and incident response runbooks are detailed in the main document:

👉 **[Read the Full Architecture Documentation (hub-documentation.md)](./hub-documentation.md)**
