# Azure Security Lab – From Exposure to Hardening

I built this lab to get hands on experience with Azure, Windows security, and basic SOC workflows. I followed a general structure from an online guide, but I customized the setup and worked through the incident myself. The goal was simple: deploy a Windows VM, expose it, see what happens, and then secure it properly.

## What I Set Up
I deployed a Windows Server VM in Azure with a public IP, created a VNet and subnet, and attached an NSG. I also connected the VM to a Log Analytics Workspace so I could collect Windows event logs. Defender for Cloud was enabled to surface recommendations and security alerts.

## What Happened
Once the VM was online, I left RDP open to the internet. It didn’t take long before the failed logons started piling up. Eventually, someone brute‑forced the login and changed the local admin password. I lost access completely, which gave me a real incident to work through.

## How I Recovered
I used Azure’s Reset Password feature to regain access. After that, I reviewed the NSG rules, removed the overly permissive inbound rule, and restricted RDP to my home IP. I also re‑enabled the Windows Firewall inside the VM and restored the default rules.

## What I Analyzed
With log collection already running, I was able to look at SecurityEvent logs (4625, 4624, etc.) to see the brute‑force attempts and the successful login. I also experimented with Sentinel workbooks and KQL queries to visualize the activity.

## What I Improved
After recovering the VM, I hardened it:
- Locked down RDP to a single trusted IP
- Removed unnecessary public exposure
- Re-enabled the firewall
- Cleaned up NSG rules
- Enabled Defender for Cloud recommendations
- Connected everything to Log Analytics for monitoring

## Why This Project Matters
This wasn’t just a lab, it turned into a real compromise and recovery scenario. It gave me experience with Azure administration, incident response, log analysis, and security hardening. It also helped me understand how quickly exposed services get targeted in the real world.
