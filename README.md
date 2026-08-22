## AutoCred

AutoCred is a Grey Hack compatibility rewrite for classic Mission Contract credential jobs. It reads compatible contract mail, identifies credential targets, tries available exploit paths, and reports any recovered password for manual mission submission. It supports Grey Hack Public version 0.9.6773 and Nightly version 0.9.7052 with optional bounded system-log cleanup after a successful recovery.

## FullTree

FullTree is a read-only Grey Hack terminal utility that prints a detailed, sorted filesystem tree. It can scan from / or a chosen path, supports paged output for large directories, and displays symlinks without following them when supported by the runtime.

## Watchdog

Watchdog is a read-only, real-time Grey Hack system monitor. It builds an in-memory baseline of the full filesystem and running processes, then reports detected file additions, deletions, changes, process starts, stops, and PID reuse. It creates no config, log, or report files.


## AutoAcademic

AutoAcademic is a supervised Grey Hack automation script for classic **Academic Changes** mission contracts. It reads compatible contracts from MetaMail, allows the player to select individual jobs or `all`, attacks the target network, searches for a usable computer, escalates access to root, and launches `StudentsViewer.exe` and `Mail.exe`. The script displays the required student, subject, and requested grade change before waiting for the player.

AutoAcademic is **not a truly unattended auto script** because GreyScript cannot perform the required graphical interface actions. The player must complete three actions for every successful job:

1. Change and save the requested grade in `StudentsViewer.exe`.
2. Reply to the original Mission Contract in `Mail.exe`.
3. Return to the terminal, type `done`, and press Enter.

After `done` is entered, AutoAcademic trusts that the player completed those actions, closes the viewer, cleans all retained remote system logs it can access, removes the completed contract from its task queue, and continues to the next selected job. Failed access attempts are recorded and skipped without stopping the remaining batch.

Complex networks may require a configured reverse-shell server or an optional router-jump library. A vulnerable library is not included with the script. AutoAcademic can run without one, but difficult routed networks may have a lower success rate.

Target version: **Grey Hack Public v0.9.6773**.


# Nmap Synthwave Deep Recon

Nmap Synthwave Deep Recon is an extensively expanded, read-only replacement for Grey Hack’s basic `nmap` script. It turns a simple port listing into a complete network reconnaissance report while preserving the shared synthwave appearance used by the Auto script family.

This is not an exploitation tool. It performs no overflows, opens no MetaXploit sessions, writes no files, and changes no network configuration.

 Usage

```text
nmap [--quick] <IP address or domain>
```

Examples:

```text
nmap 77.190.89.172
nmap example.com
nmap --quick 12.32.56.89
```

Full mode performs exhaustive forwarding and eligible subnet sweeps. `--quick` skips those expensive operations while retaining the normal port, router, identity, firewall, and topology information.

 Features

- Traditional open-port and service/version reporting
- IP address and domain-name targets
- Execution-host, public-IP, local-IP, gateway, user, and adapter details
- Public WHOIS identity
- Router and switch discovery
- Router kernel and control-plane information
- Wireless ESSID and BSSID reporting
- Firewall-rule inspection
- Visible public port-forward mapping
- Exhaustive `0–65535` forwarding sweep
- Detection of forwarded ports omitted by `router.used_ports`
- Hidden-open and hidden-closed forward reporting
- Forward destination LAN addresses
- LAN-device inventory
- Internal service and port mapping
- Direct `/24` discovery when running inside the applicable LAN
- Local switch and nested-network discovery
- Bounded recursive topology collection
- Explicit visibility gaps and suggested pivot points
- Detailed scan statistics and elapsed time
- Synthwave terminal colors with readable aligned tables

 Observation Boundaries

Grey Hack exposes different information depending on where the script is executed. An external scan cannot prove that every device behind a firewall or nested router has been discovered. Re-running the script from an internal foothold may reveal additional hosts, services, switches, and network segments.

Public-to-internal port correlations are labeled as likely mappings. Grey Hack exposes the destination LAN address and service information but does not always expose an authoritative internal destination port.

The report clearly distinguishes observed facts, inferred mappings, unavailable information, filtered systems, and areas requiring a closer network vantage.

 Safety Limits

To prevent runaway scans, the script includes limits for:

- Recursive topology depth
- Total observed network devices
- Routers eligible for exhaustive port sweeps
- Table-output size

Despite its size, the script remains completely read-only.

In short: Grey Hack’s original nmap tells you which ports are visible. Nmap Synthwave Deep Recon attempts to explain the entire observable network surrounding them.

## UPDATES
All SRC files will be updated over time.
