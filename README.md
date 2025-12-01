
# Zero-Trust-Security-Lab---Server-Hardering-
Zero-Trust security lab with Tailscale access, hardened SSH, strict firewall rules, a port 22 honeypot for brute-force monitoring, and an isolated web exploitation environment using BeEF. Built for safe offensive-security, logging, and detection practice.

## What You Get

| Feature                        | Status     | Description |
|--------------------------------|------------|-----------|
| Zero public SSH                | Complete   | Only reachable via Tailscale (100.x.x.x) |
| Key-only authentication       | Complete   | `PasswordAuthentication no`, root disabled |
| Port 22 honeypot               | Complete   | Cowrie in Docker – full bot trap |
| Strict UFW firewall            | Complete   | Default deny + Tailscale interface allowed |
| Auto security updates          | Complete   | unattended-upgrades |
| Tailscale exit-node ready      | Complete   | Optional full-tunnel VPN |
| BeEF / Web lab (optional)      | Complete   | Isolated on port 80/3000 |


## How it Works? 


```
[ PC/Laptop/Mobile ] --- Tailscale ---> [ Server (100.x.x.x) ]
      |                           |
      | (NO public SSH)           |-- Port 80 → Website / BeEF
      |                           |-- Port 22 → Honeypot
```

## Verification (Nmap Scans)

<img width="636" height="315" alt="nmap scan" src="https://github.com/user-attachments/assets/034e0a3b-6ab8-467a-8592-9f3bbfcebc0f" />

---

<img width="860" height="401" alt="fiinal nmap" src="https://github.com/user-attachments/assets/684cb2b8-7951-41b7-a3b4-8d53f3aa8042" />
