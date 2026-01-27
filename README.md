## Lab Setup Progress

### Infrastructure Setup

- Installed and configured 4 virtual machines:
  - Ubuntu Server (SIEM)
  - Windows 7 (vulnerable endpoint)
  - Windows 10 (modern endpoint)
  - Kali Linux (attacker)
    
- Allocated VM resources based on host hardware constraints
- Took clean baseline snapshots of Windows VMs
- Designed lab with attack simulation and telemetry collection in mind

Networking, attack simulation, and log analysis will be added incrementally.

> See `/screenshots/day1-infra/` for validation evidence.

## Internal Network Configuration

- Created an isolated internal network for the SOC lab environment
- Assigned static IP addresses on a dedicated subnet (10.10.10.0/24)
- Configured:
  - Ubuntu Server (SIEM) – static IP
  - Windows 10 endpoint – static IP
  - Kali Linux attacker – static IP
- Verified full host-to-host connectivity using ICMP
- Enabled ICMP echo requests on Windows for network validation
- Confirmed isolation from external networks during internal testing

This establishes a controlled lateral-movement and monitoring environment for future attack simulations and log collection.

> See `/screenshots/day2-internal-network/` for validation evidence.

## Splunk SIEM Deployment & Log Ingestion

- Installed Splunk Enterprise on Ubuntu Server (SIEM node)
- Accepted license and initialized Splunk services
- Resolved service startup issues related to privileged execution
- Enabled TCP data receiving on port **9997**
- Verified Splunk web interface accessibility

- Installed Splunk Universal Forwarder on Windows 10 endpoint
- Configured forwarder to send telemetry to Ubuntu SIEM
- Validated active forwarding connection between Windows and Ubuntu

- Identified and resolved indexing failures caused by:
  - Insufficient disk allocation
  - Missing input definitions

- Created and configured `inputs.conf` on the Windows forwarder to collect:
  - Application logs  
  - Security logs  
  - System logs  

- Restarted forwarder services and confirmed successful event ingestion

- Validated SIEM pipeline by:
  - Searching Windows event logs in Splunk
  - Detecting a failed authentication event (Event ID 4625)
  - Simulated an authentication failure on the Windows endpoint to validate security event ingestion and detection capability
  - Successfully observed and analyzed Event ID **4625 (Failed Logon)** in the SIEM
  - Confirming host attribution and index population

This establishes the core SIEM telemetry pipeline for the SOC lab and enables future detection engineering and attack simulation.

> See `/screenshots/day3-splunk-installation-ubuntu/` for validation evidence.

## Advanced Telemetry & Service Hardening
Enhanced endpoint visibility beyond standard Windows logs to detect sophisticated techniques.

* **Sysmon Deployment:**
    * Installed Sysmon on Windows 10 Endpoint to capture granular process and network telemetry.
    * Applied the **SwiftOnSecurity** configuration profile to filter noise and prioritize high-value security events.
* **Service Configuration:**
    * Reconfigured the Splunk Universal Forwarder service to execute as a specific **Local User** rather than Local System.
    * Validated service stability and persistence across reboots.
* **Ingestion Verification:**
    * Confirmed Sysmon event indexing in Splunk.
    * Validated visibility of advanced fields (ParentProcessID, CommandLine, Hashes) on the dashboard.
    * Telemetry pipeline is active with Sysmon enrichment.

> See `/screenshots/day4-sysmon-telemetry/` for validation evidence.

