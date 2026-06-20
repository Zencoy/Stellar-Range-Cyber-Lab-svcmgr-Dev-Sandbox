🛡️ Stellar Range — Cyber Lab + svcmgr Dev Sandbox


Dual-track build log: an isolated VMware cyber range for offensive/defensive security training, paired with native development of svcmgr (Stellar Service Manager) — a Go/Cobra CLI for encrypted server management, SSH tunneling, and structured logging.

https://img.shields.io/badge/license-MIT-lightgrey
https://img.shields.io/badge/platform-VMware%20%2B%20WSL2-blue
https://img.shields.io/badge/Go-1.22-00ADD8?logo=go&logoColor=white
https://img.shields.io/badge/status-active--development-yellow

📡 Overview

Operator TrackBuild and operate an isolated cybersecurity home lab — offensive (Kali), vulnerable targets (Metasploitable, DVWA, Juice Shop, WebGoat), and SOC monitoring (Wazuh)Developer TrackBuild svcmgr, a Go/Cobra CLI for secure server management — AES-256 encrypted local config (~/.config/svcmgr/), SSH tunneling, structured JSON loggingWhy combinedThe lab VMs double as safe, isolated SSH targets for testing svcmgr's tunneling features without touching production infrastructure

🗺️ Network Topology

<img width="1454" height="514" alt="image" src="https://github.com/user-attachments/assets/9d896ca0-fea2-4415-a37d-e725ea80839b" />


Isolation guarantee: no VM adapter is ever set to Bridged. All lab traffic stays inside VMware's virtual NAT/Host-only switches — it never reaches the home/employer physical network.

💻 Resource Allocation

ComponentRAMDiskNetworkStatusKali Linux4 GB25 GBNAT (VMnet8)✅ ActiveUbuntu Server (Docker host)4 GB20 GBNAT + Host-only⬜ PlannedMetasploitable 20.5 GB3 GBNAT (VMnet8)⬜ PlannedWSL2 (Go dev env)dynamic~5 GBWindows host⬜ PlannedpfSense1 GB8 GB—⏸ Deferred (Phase 2)Windows Server DC4 GB30 GB—⏸ Deferred (Phase 2)Windows 10 Client4 GB40 GB—⏸ Deferred (Phase 2)

Host baseline assumed: 16 GB RAM / 189 GB free storage — update with your actual msinfo32 numbers.

🎯 Mission

Operator Track


 Network fundamentals (IP/ports/protocols)
 SSH key-based auth + tunneling
 First Nmap scan, Kali → Metasploitable
 DVWA / Juice Shop walkthroughs
 Wazuh SIEM live, alerting on Kali scans


Developer Track


 Go fundamentals (structs, interfaces, error handling)
 Cobra CLI structure (commands, flags, subcommands)
 Read svcmgr source top-down
 First contribution (flag, log field, or test)
 svcmgr SSH tunnel verified against isolated lab VM


✅ Milestone Log

DatePhaseMilestoneNotesSetupKali Linux importedSetupVMware NAT + Host-only configuredReplaces pfSense for nowSetupWSL2 + Go toolchain installedLabUbuntu Docker host deployedLabDVWA / Juice Shop / WebGoat runningDevsvcmgr builds cleanly (go build ./...)DevFirst SSH tunnel test (WSL2 → lab VM)Phase 2pfSense reintroduced (RAM permitting)Phase 2Windows AD lab (DC + client) online

📁 Repository Structure

svcmgr/
├── cmd/                # Cobra command definitions
├── internal/
│   ├── config/          # AES-256 config storage logic
│   ├── ssh/              # Tunneling implementation
│   └── logging/        # Structured JSON logger
├── docs/
│   └── lab-notes/      # Cyber lab build logs, this README
├── go.mod
├── go.sum
└── README.md

🧰 Tech Stack

LayerToolsHypervisorVMware WorkstationOffenseKali LinuxTargetsMetasploitable 2, DVWA, OWASP Juice Shop, WebGoatSOCWazuh SIEMDev environmentWSL2 (Ubuntu), Go, VS Code (Remote-WSL)CLI frameworkCobraSecurityAES-256 (config-at-rest), SSH (transport)

🚀 Getting Started

bash# Clone
git clone https://github.com/<your-username>/svcmgr.git
cd svcmgr

# Build (inside WSL2)
go build ./...

# Run tests
go test ./...

🔒 Isolation & Safety Notes


All lab VM adapters use NAT (VMnet8) or Host-only (VMnet1) — never Bridged.
svcmgr's SSH tunneling is tested exclusively against the isolated Ubuntu lab VM, not external hosts.
Encryption keys for ~/.config/svcmgr/ are never committed to this repo.
