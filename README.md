## Lab Setup Progress

### Day 1 – Infrastructure Setup

- Installed and configured 4 virtual machines:
  - Ubuntu Server (SIEM)
  - Windows 7 (vulnerable endpoint)
  - Windows 10 (modern endpoint)
  - Kali Linux (attacker)
    
- Allocated VM resources based on host hardware constraints
- Took clean baseline snapshots of Windows VMs
- Designed lab with attack simulation and telemetry collection in mind

Networking, attack simulation, and log analysis will be added incrementally.

> See `/screenshots/day1-infra/ for validation evidence.

## Day 2 – Internal Network Configuration

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
