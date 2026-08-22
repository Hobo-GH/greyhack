## AutoCred 2.2.0

AutoCred is a Grey Hack automation tool for classic **Credentials needed** Mission Contracts. It turns the normal credential-recovery workflow into one command, one masked MetaMail password/PIN prompt, and one job selection.

Choose an index, several indexes, or `all`. AutoCred reads the contracts, maps each target, attacks available services, recovers the requested credentials, finalizes logs on retained remote objects, and continues to the next selected job when one target fails.

Target baseline: **Grey Hack Public v0.9.6773**.

 Operator flow

1. Run `autocred`.
2. Enter the MetaMail password/PIN at the masked prompt.
3. Select one or more contract indexes, or type `all`.
4. Allow AutoCred to recover and print the credentials.
5. Reply to each matching Mission Contract manually in Mail.exe using the printed password.

AutoCred does **not** send Mission Contract replies automatically.

 Selection commands

```text
0                 run one displayed contract
0 2 5             run several displayed contracts
all               run every displayed credential contract
fresh             reload the MetaMail API snapshot
refresh           same as fresh
q                 quit
```

Pressing Enter at the selection prompt is also treated as `all`.

 What AutoCred automates

- Reads current classic credential Mission Contracts from MetaMail.
- Separates **ANY user** jobs from contracts requesting a specific username.
- Maps public ports, forwarded services, internal ports, and the requested LAN address.
- Reuses known exact-version exploits from the shared ACVDB3 vulnerability database.
- Scans unknown library versions and adds useful results back to that database.
- Prefers exact-target computer, shell, and file objects over unrelated footholds.
- Reads accessible `/etc/passwd` files, deciphers root credentials, and retries the exact target with elevated access.
- Uses bounded router and LAN continuation when the requested machine is behind the public router.
- Supports an optional vulnerable router library for PoisonLib-assisted LAN jumps.
- Finalizes `/var/system.log` on retained cleanup-capable objects after every attempted contract.
- Continues an `all` run after individual failures instead of stopping the entire batch.
- Prints a final per-contract result list and a separate list of recovered credentials.

 Configuration

The GitHub release intentionally contains no player identity, password, IP address, or private file path:

```text
MAIL_USER = ""
MAIL_PASSWORD = ""
PIN = ""
POISON_HTTP_SOURCE = ""
```

For normal use, leave the first three fields blank. AutoCred detects the active player's mail address and uses the single masked prompt as the MetaMail password.

`POISON_HTTP_SOURCE` is optional. To enable the router-library fallback, place a compatible vulnerable library on the execution server and enter its absolute path. Leave it blank to disable that fallback.

Compile the source as `/bin/autocred` on the machine that will perform the attacks.

 Organized runtime files

AutoCred creates missing folders automatically and keeps its files out of `/root`:

```text
/root/autoscripts/credential/
├── tasks/
│   └── current.txt
└── logs/
    └── latest.txt

/root/vulndb/
├── index.txt
└── <library>/
    └── V<major>/
        └── shard-NNNN.txt
```

`current.txt` contains only the active run's remaining queue. It is rebuilt at startup and cleared after processing, so an old completed job list is not intentionally reused as task memory.

The ACVDB3 database is shared with compatible Auto-family tools. Records retain the exact library version inside packed major-version shards, allowing later attacks to try known useful exploits before rescanning the library.

 Fresh and refresh behavior

`fresh` and `refresh` discard the displayed list and launch a short-lived, intake-only AutoCred worker. That worker logs into MetaMail, fetches a new API snapshot, returns it to the parent process, and exits.

This worker has been confirmed to launch and return records in Grey Hack. However, it cannot force Grey Hack's game server to generate or expose newer mail. If Mail.exe and newly launched workers continue showing the same contracts, repeatedly restarting AutoCred will not repair that server-side mail state.

 Important limits

- Only classic credential Mission Contracts are supported. Procedural Fraud, Sabotage, and Corporate Espionage jobs are intentionally excluded.
- Mission replies remain manual because the recovered password must be sent through Mail.exe.
- Log finalization covers retained objects that AutoCred can still control. It cannot clean a machine when every exploit failed and no cleanup-capable object was obtained.
- A vulnerable PoisonLib can improve router-jump coverage, but the GitHub release does not bundle one.
- MetaMail API output is controlled by Grey Hack. `fresh` cannot repair stale server/account mail data.


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
