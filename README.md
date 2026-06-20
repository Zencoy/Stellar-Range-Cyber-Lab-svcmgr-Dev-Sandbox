🛡️ Stellar Range — Cyber Lab + svcmgr Dev Sandbox


Dual-track build log: an isolated VMware cyber range for offensive/defensive security training, paired with native development of svcmgr (Stellar Service Manager) — a Go/Cobra CLI for encrypted server management, SSH tunneling, and structured logging.

https://img.shields.io/badge/license-MIT-lightgrey
https://img.shields.io/badge/platform-VMware%20%2B%20WSL2-blue
https://img.shields.io/badge/Go-1.22-00ADD8?logo=go&logoColor=white
https://img.shields.io/badge/status-active--development-yellow

📡 Overview

Operator TrackBuild and operate an isolated cybersecurity home lab — offensive (Kali), vulnerable targets (Metasploitable, DVWA, Juice Shop, WebGoat), and SOC monitoring (Wazuh)Developer TrackBuild svcmgr, a Go/Cobra CLI for secure server management — AES-256 encrypted local config (~/.config/svcmgr/), SSH tunneling, structured JSON loggingWhy combinedThe lab VMs double as safe, isolated SSH targets for testing svcmgr's tunneling features without touching production infrastructure

🗺️ Network Topology

#mermaid-rol-r1 { font-family: "Anthropic Sans", system-ui, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; font-size: 16px; fill: rgb(229, 229, 229); }
#mermaid-rol-r1 .edge-animation-slow { stroke-dashoffset: 900; animation: 50s linear 0s infinite normal none running dash; stroke-linecap: round; stroke-dasharray: 9, 5 !important; }
#mermaid-rol-r1 .edge-animation-fast { stroke-dashoffset: 900; animation: 20s linear 0s infinite normal none running dash; stroke-linecap: round; stroke-dasharray: 9, 5 !important; }
#mermaid-rol-r1 .error-icon { fill: rgb(204, 120, 92); }
#mermaid-rol-r1 .error-text { fill: rgb(51, 135, 163); stroke: rgb(51, 135, 163); }
#mermaid-rol-r1 .edge-thickness-normal { stroke-width: 1px; }
#mermaid-rol-r1 .edge-thickness-thick { stroke-width: 3.5px; }
#mermaid-rol-r1 .edge-pattern-solid { stroke-dasharray: 0; }
#mermaid-rol-r1 .edge-thickness-invisible { stroke-width: 0; fill: none; }
#mermaid-rol-r1 .edge-pattern-dashed { stroke-dasharray: 3; }
#mermaid-rol-r1 .edge-pattern-dotted { stroke-dasharray: 2; }
#mermaid-rol-r1 .marker { fill: rgb(161, 161, 161); stroke: rgb(161, 161, 161); }
#mermaid-rol-r1 .marker.cross { stroke: rgb(161, 161, 161); }
#mermaid-rol-r1 svg { font-family: "Anthropic Sans", system-ui, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; font-size: 16px; }
#mermaid-rol-r1 p { margin: 0px; }
#mermaid-rol-r1 .label { font-family: "Anthropic Sans", system-ui, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; color: rgb(229, 229, 229); }
#mermaid-rol-r1 .cluster-label text { fill: rgb(51, 135, 163); }
#mermaid-rol-r1 .cluster-label span { color: rgb(51, 135, 163); }
#mermaid-rol-r1 .cluster-label span p { background-color: transparent; }
#mermaid-rol-r1 .label text, #mermaid-rol-r1 span { fill: rgb(229, 229, 229); color: rgb(229, 229, 229); }
#mermaid-rol-r1 .node rect, #mermaid-rol-r1 .node circle, #mermaid-rol-r1 .node ellipse, #mermaid-rol-r1 .node polygon, #mermaid-rol-r1 .node path { fill: transparent; stroke: rgb(161, 161, 161); stroke-width: 1px; }
#mermaid-rol-r1 .rough-node .label text, #mermaid-rol-r1 .node .label text, #mermaid-rol-r1 .image-shape .label, #mermaid-rol-r1 .icon-shape .label { text-anchor: middle; }
#mermaid-rol-r1 .node .katex path { fill: rgb(0, 0, 0); stroke: rgb(0, 0, 0); stroke-width: 1px; }
#mermaid-rol-r1 .rough-node .label, #mermaid-rol-r1 .node .label, #mermaid-rol-r1 .image-shape .label, #mermaid-rol-r1 .icon-shape .label { text-align: center; }
#mermaid-rol-r1 .node.clickable { cursor: pointer; }
#mermaid-rol-r1 .root .anchor path { stroke-width: 0; stroke: rgb(161, 161, 161); fill: rgb(161, 161, 161) !important; }
#mermaid-rol-r1 .arrowheadPath { fill: rgb(11, 11, 11); }
#mermaid-rol-r1 .edgePath .path { stroke: rgb(161, 161, 161); stroke-width: 1px; }
#mermaid-rol-r1 .flowchart-link { stroke: rgb(161, 161, 161); fill: none; }
#mermaid-rol-r1 .edgeLabel { background-color: transparent; text-align: center; }
#mermaid-rol-r1 .edgeLabel p { background-color: transparent; }
#mermaid-rol-r1 .edgeLabel rect { opacity: 0.5; background-color: transparent; fill: transparent; }
#mermaid-rol-r1 .labelBkg { background-color: rgba(0, 0, 0, 0.5); }
#mermaid-rol-r1 .cluster rect { fill: rgb(204, 120, 92); stroke: rgb(138, 115, 107); stroke-width: 1px; }
#mermaid-rol-r1 .cluster text { fill: rgb(51, 135, 163); }
#mermaid-rol-r1 .cluster span { color: rgb(51, 135, 163); }
#mermaid-rol-r1 div.mermaidTooltip { position: absolute; text-align: center; max-width: 200px; padding: 2px; font-family: "Anthropic Sans", system-ui, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; font-size: 12px; background: rgb(204, 120, 92); border: 1px solid rgb(138, 115, 107); border-radius: 2px; pointer-events: none; z-index: 100; }
#mermaid-rol-r1 .flowchartTitleText { text-anchor: middle; font-size: 18px; fill: rgb(229, 229, 229); }
#mermaid-rol-r1 rect.text { fill: none; stroke-width: 0; }
#mermaid-rol-r1 .icon-shape, #mermaid-rol-r1 .image-shape { background-color: transparent; text-align: center; }
#mermaid-rol-r1 .icon-shape p, #mermaid-rol-r1 .image-shape p { background-color: transparent; padding: 2px; }
#mermaid-rol-r1 .icon-shape .label rect, #mermaid-rol-r1 .image-shape .label rect { opacity: 0.5; background-color: transparent; fill: transparent; }
#mermaid-rol-r1 .label-icon { display: inline-block; height: 1em; overflow: visible; vertical-align: -0.125em; }
#mermaid-rol-r1 .node .label-icon path { fill: currentcolor; stroke: revert; stroke-width: revert; }
#mermaid-rol-r1 .node .neo-node { stroke: rgb(161, 161, 161); }
#mermaid-rol-r1 [data-look="neo"].node rect, #mermaid-rol-r1 [data-look="neo"].cluster rect, #mermaid-rol-r1 [data-look="neo"].node polygon { stroke: url("#mermaid-rol-r1-gradient"); filter: drop-shadow(rgb(185, 185, 185) 1px 2px 2px); }
#mermaid-rol-r1 [data-look="neo"].node path { stroke: url("#mermaid-rol-r1-gradient"); stroke-width: 1px; }
#mermaid-rol-r1 [data-look="neo"].node .outer-path { filter: drop-shadow(rgb(185, 185, 185) 1px 2px 2px); }
#mermaid-rol-r1 [data-look="neo"].node .neo-line path { stroke: rgb(161, 161, 161); filter: none; }
#mermaid-rol-r1 [data-look="neo"].node circle { stroke: url("#mermaid-rol-r1-gradient"); filter: drop-shadow(rgb(185, 185, 185) 1px 2px 2px); }
#mermaid-rol-r1 [data-look="neo"].node circle .state-start { fill: rgb(0, 0, 0); }
#mermaid-rol-r1 [data-look="neo"].icon-shape .icon { fill: url("#mermaid-rol-r1-gradient"); filter: drop-shadow(rgb(185, 185, 185) 1px 2px 2px); }
#mermaid-rol-r1 [data-look="neo"].icon-shape .icon-neo path { stroke: url("#mermaid-rol-r1-gradient"); filter: drop-shadow(rgb(185, 185, 185) 1px 2px 2px); }
#mermaid-rol-r1 :root { --mermaid-font-family: "Anthropic Sans",system-ui,"Segoe UI",Roboto,Helvetica,Arial,sans-serif; }VMnet8 — NAT (Internet + Inter-VM)Windows Host (Bare Metal)SSH tunnel test trafficscans / exploitsscans / exploitsNO bridge to physical NICVMnet1 — Host-Only(Mgmt/SSH only)WSL2 — Go Dev Envsvcmgr build + testKali LinuxAttacker · 4GB RAMMetasploitable 2Target · 512MB RAMUbuntu Server 24.04Docker Host · 4GB RAMDVWA :8080Juice Shop :3000WebGoat :8081Wazuh SIEM :443Physical LAN / Internet

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
