# Secure Infrastructure Architecture & Automated ChatOps Provisioning Blueprint

## 📋 Architectural Overview
This repository outlines the secure, automated, bare-metal and mesh-networked production infrastructure designed to support a distributed, cross-platform video game development studio. 

The core directive of this architecture is to provide high-throughput asset pipeline access (Perforce), secure directory management, and zero-trust remote access for a cross-platform team (Windows and macOS) while automating routine administrative overhead via decentralized ChatOps.

---

## 🏗️ Core Infrastructure Stack

### 1. Compute & Storage Baseline (Bare-Metal)
* **Hypervisor Layer:** High-availability Type-1 hypervisors managing isolated virtual instances for directory services, version control, and automation engines.
* **Storage Architecture:** Dedicated local hardware RAID storage arrays optimized for high-sustained sequential read/write targets, ensuring data integrity and rapid recovery capabilities for large binary assets.
* **Sovereign Data Storage:** Deployed a self-hosted Nextcloud instance to manage secure, internal file sharing, collaboration, and private cloud storage pipelines across the distributed team.
* **Asset Pipeline:** Multi-user dedicated version control repository (Perforce Helix Core) running on a hardened internal instance, optimized for large-file game engine transactions.

### 2. Private Networking & Self-Hosted Mesh Control Plane
* **Edge Security Gateway:** Deployed a hardened **pfSense** firewall architecture at the network perimeter, managing line-rate stateful packet inspection, strict NAT configurations, and local VLAN segmentation.
* **Independent SDN Controller:** Deployed and configured a self-hosted **ztnet** instance, establishing full sovereign administrative control over our own private ZeroTier network control plane.
* **Zero-Trust Overlay:** Managed encrypted, peer-to-peer layer-2 network overlays across all distributed endpoints via our independent controller infrastructure.
* **Cross-Platform Bridging:** Specialized network routing and bridging configurations implemented to ensure seamless, low-latency repository access for remote macOS workstations (e.g., audio and sound design teams) interacting with the core infrastructure.
* **Perimeter Hardening:** Inbound traffic rules on the pfSense perimeter are set to block all untrusted public WAN ingress, allowing remote access *only* via authenticated, cryptographic mesh identities.

### 3. Ephemeral Sandbox Environments & Browser Isolation
* **Containerized VDI Engine:** Deployed Kasm Workspaces to provide the distributed team with on-demand, containerized streaming desktops and isolated browser environments.
* **Malware Insulation & RBI:** Configured disposable Kasm containers to execute Remote Browser Isolation (RBI). This ensures team members can interact with untrusted external assets, web resources, or attachments inside an ephemeral, sandboxed container that destroys itself upon session termination—completely insulating the core bare-metal infrastructure from web-borne execution vectors.

### 4. Container Management & High-Availability Monitoring
* **Private Container Registry:** Operationalized a dedicated internal Docker Repository/Registry to securely build, store, and distribute customized container images across our hypervisor and VDI nodes.
* **Infrastructure Observability:** Integrated **Uptime Kuma** for real-time monitoring of all critical network nodes, internal services, and asset pipelines, configuring automated alert routing to track infrastructure state and ensure high availability.

### 5. Identity Management & ChatOps Automation
* **Active Directory Services:** Centralized access control leveraging Active Directory (AD) to systematically manage studio credentials, user authentication, and domain group policies for repository and network access.
* **Automation Engine:** Event-driven workflow automation (n8n) hosting custom pipelines that sit between communication channels and core infrastructure management.
* **ChatOps Integration:** Secure integration with team communication nodes (Discord). Approved administrators can trigger the automated backend pipeline via isolated bot commands to securely provision Active Directory credentials and instantly authorize new ZeroTier nodes without manual hypervisor intervention.

---

## 🔒 Security & Operational Safeguards (OpSec Statement)
To maintain the security of the active production environment, all explicit configuration scripts, live workflow definitions, cryptographic keys, network IDs, and deployment code are strictly omitted from this public documentation. This blueprint serves purely as a conceptual and structural reference for enterprise infrastructure design.
