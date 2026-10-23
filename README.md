External Attack Surface Management (EASM) & Vulnerability Scanner

ApexPointer is a strategic risk governance framework designed to continuously monitor an organization's public-facing digital perimeter from an adversarial perspective. It automatically identifies technical exposures, visualizes attack paths using 3D graphs, and translates raw telemetry into executive-level risk metrics and automated remediation workflows.

---

## Core Capabilities and Modules

### 1. Asynchronous Dual-Lane Scanning Engine
- **Light Queue:** Optimized for rapid reconnaissance, including subdomain enumeration, quick HTTP probing, and core port checks (supports up to 10 concurrent user tasks).
- **Deep Queue:** Executes exhaustive profiling operations, such as deep administrative panel discovery and Nmap NSE script auditing (throttled to 2 parallel workers to protect host infrastructure).
- **CISA KEV Integration:** Automatically cross-references findings against the CISA Known Exploited Vulnerabilities catalog in real time.

### 2. Assets Management and Automated Remediation
- **Multi-Stage OSINT Pipeline:** Asynchronous discovery using Subfinder, Assetfinder, RapidDNS scraping, and Urlscan schemas.
- **Port Probing & CDN Resolution:** High-speed probing via Naabu configured to map alternative enterprise HTTP/HTTPS ports (e.g., 2052, 2053, 8080, 8443) behind Cloudflare proxies.
- **Service Fingerprinting & CVE Enrichment:** Banner-grabbing via Nmap XML parsing enriched passively with the Shodan InternetDB API.
- **Sensitive Data & Supply-Chain Auditing:** Regex-based secret scraping for configuration files (`.env`, `.git/config`) and Client-Side JavaScript auditing against an offline CVE database (Retire.js) for third-party libraries (jQuery, Firebase SDK, etc.).
- **Automated SSH Remediation:** Executes dynamic Bash scripts to apply kernel-level `iptables` `DROP` rules directly on target hosts or generates decoupled scripts for zero-trust environments. Features an intelligent Self-Lockout Prevention mechanism for critical ports like SSH (port 22).

### 3. Time Machine and Historical Snapshot Differencing
- Treats each scanning cycle as an immutable point-in-time snapshot.
- Compares any two historical scans to calculate asymmetric deltas, displaying dynamic change cards (New, Removed, Changed) to track asset drift (e.g., newly exposed services like `+port 6379`).

### 4. CISO Insights and Business Risk Analytics
- **Dynamic Risk Quantification:** Aggregates findings into a unified, board-ready Overall Risk Score (0-100 scale).
- **AI CISO Assistant:** Gemini AI integration providing interactive explanations of vulnerability metrics in plain language. Built with strict Context Isolation to prevent prompt injection.
- **SME Financial Loss & Compliance Gap Matrix:** Translates technical risks into estimated daily downtime financial losses ($1,000/day to $2,600/day across 7 industry sectors) and maps exposures directly to ISO/IEC 27001:2022 controls.

### 5. AI Attack Chain Visualization
- Interactive graph visualization (D3.js / node-based layout) simulating potential multi-step intrusion paths from initial Entry Pivots down to Critical Impact End-Nodes.
- Includes granular node inspection detailing CVSS scores, MITRE ATT&CK techniques (e.g., T1005), Time-to-Exploit (TTE) estimates, historical case study references, and tactical remediation steps.

### 6. Remote Honeypot Orchestration
- Deploys Low-Interaction strategic decoys (e.g., simulated MySQL on Port 3306) across exposed endpoints via automated Systemd service management.
- Captures stealth scanning telemetry, geo-locates threat actors (MaxMind GeoIP), and performs reverse DNS lookups in real time to deflect traffic from production assets.

### 7. Centralized Administrator Dashboard
- Real-time monitoring of asynchronous scan queues (Light and Deep).
- System-wide Global Threat Counter tracking critical and high severity exposures across all tenants.
- Execution controls including scan prioritization, task termination (Kill Switch), and user session management (User Ban).

---

## Architecture and Technology Stack

- **Backend & Orchestration:** Python, Celery, Redis (in-memory task queuing and real-time state management).
- **Database:** PostgreSQL (relational storage with strict multi-tenant data isolation enforced at the query level).
- **AI Engine:** Google Gemini API (encrypted server-side under a Bring-Your-Own-Key / BYOK execution model).
- **Frontend & Visualization:** D3.js interactive graph systems, dynamic Light/Dark interface mode.
- **Security & Privacy:** Zero-Knowledge architecture for host credentials and Article 17 GDPR-compliant hard data purging ("Purge All My Data").

---

---

## Documentation

The complete project report and technical documentation are available directly in the repository:
- Project Report (PDF): [report.pdf](./report.pdf)
