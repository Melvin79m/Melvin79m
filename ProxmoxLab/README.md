# Proxmox VE Homelab

**A production-style virtualization platform running on bare-metal hardware — 14 LXC containers, 2 VMs, dual network bridges, and a full services stack with remote access, monitoring, and security.**

---

## Hardware

| Component | Spec |
|-----------|------|
| Host | Lenovo ThinkCentre M920Q Tiny |
| CPU | Intel Core i7-8700T (6-core, 12-thread) |
| RAM | 32GB DDR4 |
| Boot Drive | 512GB NVMe SSD |
| Data Drive | 14TB Seagate HDD (USB, ext4, mounted at `/mnt/data`) |
| OS | Proxmox VE 9.1.0 — kernel 6.17.2-1-pve |

---

## Network Architecture

### Bridges

| Bridge | Subnet | Role |
|--------|--------|------|
| vmbr0 | 10.10.10.0/24 | Physical VLAN trunk — internet-facing containers, gateway via R1 |
| vmbr1 | 10.40.40.0/24 | Internal NAT bridge — private services, no direct WAN exposure |

vmbr0 connects to a Cisco 3750X trunk port carrying VLANs 10, 20, and 30. All internet-facing containers live on vmbr0. Internal containers on vmbr1 reach the internet via NAT through the PVE host.

### Cross-Subnet Routing (vmbr0 ↔ vmbr1)

Internal containers (10.40.40.0/24) can reach vmbr0 services and the physical network through three configuration layers:

- `net.ipv4.ip_forward=1` enabled on the PVE host
- Static route `10.40.40.0/24 via 10.10.10.11` on all vmbr0 containers
- `iptables FORWARD ACCEPT` between vmbr0 and vmbr1 interfaces

---

## Containers & VMs

### Infrastructure & Security

| ID | Name | IP | Purpose |
|----|------|----|---------|
| CT150 | adguard-home | 10.10.10.50 | Network-wide DNS adblocker + upstream DNS resolver |
| CT204 | uptime-kuma | 10.40.40.4 | Uptime monitoring — 10+ service monitors with alerting |
| CT205 | vaultwarden | 10.40.40.6 | Self-hosted Bitwarden-compatible password manager (Docker) |
| CT206 | wazuh | 10.40.40.7 | SIEM — log aggregation, file integrity monitoring, 7 agents |
| CT207 | dashy | 10.40.40.8 | Centralized command-center dashboard for all services |
| CT209 | syncthing | 10.10.10.34 | Peer-to-peer file sync across all lab machines |
| CT210 | nextcloud | 10.10.10.35 | Self-hosted cloud storage (Nextcloud AIO, Docker) |

### Storage & Productivity

| ID | Name | IP | Purpose |
|----|------|----|---------|
| CT202 | couchdb | 10.40.40.3 | Obsidian LiveSync backend — real-time note sync |
| CT208 | immich | 10.10.10.33 | Self-hosted photo management (Docker stack) |

### Automation & AI

| ID | Name | IP | Purpose |
|----|------|----|---------|
| CT200 | hermes-core | 10.10.10.62 | Thomas AI resident engineer — Ollama (mistral), custom agent framework |
| CT201 | n8n | 10.40.40.2 | No-code workflow automation with Telegram/webhook integrations |
| CT203 | crewai | 10.40.40.5 | CrewAI multi-agent framework for AI task pipelines |

### Active Directory Lab

| ID | Name | IP | Purpose |
|----|------|----|---------|
| VM101 | MEL-DC-01 | — | Windows Server 2022 — Primary Domain Controller |
| VM108 | MEL-CL-01 | — | Windows 11 — Domain-joined client workstation |

---

## Storage Layout

| Location | Type | Contents |
|----------|------|----------|
| local-lvm | LVM-thin | Container rootfs volumes, VM disks |
| local (`/var/lib/vz`) | Directory | ISO images, container templates |
| `/mnt/data` | ext4 (14TB HDD) | Media, Immich photos, Nextcloud data, downloaded files |

Key bind mounts from the 14TB drive into containers:
- `/mnt/data/immich` → CT208 `/mnt/data/immich`
- `/mnt/data/nextcloud` → CT210 data volume

---

## Remote Access Stack

### Tailscale Mesh VPN

The PVE host runs as a Tailscale node in a 9-node WireGuard mesh that includes all lab containers, user devices, and mobile. Services are exposed externally via **Tailscale Serve** (tailnet-only) and **Tailscale Funnel** (public HTTPS) — no port forwarding required on the home router.

### Caddy Reverse Proxy

Caddy runs on the PVE host and handles all TLS termination. Traffic is routed to internal services via:

- **Path-based routing** (e.g., `/hermes/*`, `/vaultwarden/*`, `/couchdb/*`)
- **Port-based routing** (dedicated ports for each major service)

Caddy binds on loopback (`bind 127.0.0.1`) to avoid conflicts with Tailscale Serve, which holds the external-facing ports on the Tailscale IP.

### Wazuh SIEM

Wazuh v4.14.5 deployed in CT206 with agents on 7 hosts:

`hermes-core` · `couchdb` · `vaultwarden` · `crewai` · `n8n` · `uptime-kuma` · `pve-host`

Provides centralized log collection, real-time file integrity monitoring, and security alerting across the entire lab.

---

## Skills Demonstrated

`Proxmox VE` `LXC Containers` `KVM/QEMU VMs` `Linux Networking` `iptables` `Network Bridges` `NAT` `Bind Mounts` `LVM-thin` `Docker` `Tailscale` `WireGuard` `Caddy` `Reverse Proxy` `TLS` `Wazuh SIEM` `DNS` `Self-Hosted Services` `bash`
