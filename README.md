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

## AutoAcademic 2.0.0

AutoAcademic automates classic **Academic Changes** income jobs in Grey Hack while leaving the three unavoidable graphical/operator actions under player control.

It is not a completely unattended automation script. For every successfully accessed job, the operator must:

1. Change the requested grade and click **Save** in `StudentsViewer.exe`.
2. Reply to the original Mission Contract and click **Send** in an already-open Mail.exe.
3. Return to AutoAcademic, type `done`, and press Enter.

When `done` is entered, AutoAcademic trusts that both game actions were completed. It removes the job from its unresolved queue, closes the viewer, waits for the resulting disconnect entry, finalizes logs through retained remote objects, and moves to the next selected contract without polling payment or customer satisfaction.

Target baseline: **Grey Hack Public v0.9.6773**.

 Operator flow

1. Keep Mail.exe open.
2. Run `/bin/autoacademic`.
3. Enter the MetaMail password/PIN at the masked prompt.
4. Select one or more contract indexes, or type `all`.
5. Wait for the `Academic change ready` panel and root-launched `StudentsViewer.exe`.
6. Complete the three operator actions above.
7. Allow AutoAcademic to clean retained logs and continue the batch.

 Selection commands

```text
0                 run one displayed contract
0 2 5             run several displayed contracts
all               run every displayed Academic contract
refresh           merge another game-provided mail snapshot into the queue
r                 same as refresh
fresh             forget the unresolved queue, then collect another snapshot
q                 quit
```

Pressing Enter at the selection prompt is treated as `all` when contracts are available.

 What AutoAcademic automates

- Reads classic Academic Changes contracts and extracts the public network, database LAN reference, student, subject, and requested result.
- Maintains an unresolved-contract queue so independently observed jobs are not lost between runs.
- Accepts any useful foothold on the contract's public network; the database LAN address is reference data, not the only valid compromise target.
- Requires root before launching the viewer, including `/etc/passwd` recovery, password deciphering, and re-login when needed.
- Searches exposed services, forwarded ports, internal services, remote libraries, and bounded route continuations.
- Reuses known exact-version exploits and contributes new useful records to the shared ACVDB3 database.
- Supports optional reverse-shell continuation and an optional vulnerable router library for PoisonLib-assisted jumps.
- Locates or copies `StudentsViewer.exe` into `/root`, launches it as root, and prints the required student, subject, and requested change.
- Closes viewer processes after `done` or `skip`.
- Finalizes `/var/system.log` through retained cleanup-capable objects after the viewer closes.
- Records individual failures and continues an `all` batch instead of stopping the entire run.

 Configuration

The GitHub source contains no personal mail identity, server address, password, or private file path:

```text
MAIL_USER = ""
MAIL_PASSWORD = ""
PIN = ""

RSHELL_SERVER_IP = ""
RSHELL_SERVER_PORT = 0
RSHELL_SERVER_SSH_PORT = 22
RSHELL_SERVER_SSH_USER = ""
RSHELL_SERVER_SSH_PASSWORD = ""

POISON_HTTP_SOURCE = ""
```

For normal MetaMail use, leave `MAIL_USER`, `MAIL_PASSWORD`, and `PIN` blank. AutoAcademic detects the active player's mail address and uses the single masked prompt as the MetaMail password.

Reverse-shell support is optional. To enable it, fill the listener and SSH fields with the player's own server information in a private copy. Leave the address, user, and password blank to disable it.

`POISON_HTTP_SOURCE` is also optional. It must point to a compatible vulnerable router library on the execution server. The GitHub release does not bundle one.

 Organized runtime files

```text
/root/autoscripts/academic/
├── tasks/
│   └── current.txt
└── logs/
    ├── latest.txt
    └── latest-partN.txt

/root/vulndb/
├── index.txt
└── <library>/
    └── V<major>/
        └── shard-NNNN.txt
```

Successfully completed grade/reply checkpoints are removed from `current.txt` immediately. Failed or skipped jobs remain unresolved and can appear again. `fresh` is intentionally destructive to that unresolved queue; use it only when the stored queue should be forgotten.

The ACVDB3 database stores exact library versions inside packed major-version shards. Compatible Auto-family tools can reuse useful exploits learned by AutoAcademic, and AutoAcademic can reuse exploits learned by the other tools.

 MetaMail behavior

Startup, `refresh`, and `fresh` request mail through a short-lived intake-only child process rather than intentionally reusing the main interpreter's MetaMail object. `refresh` merges the returned snapshot into the unresolved queue. `fresh` clears the queue before merging it.

This cannot force Grey Hack's server to expose mail that is absent from the game-provided MetaMail snapshot. If Mail.exe and newly launched workers continue returning an incomplete or unchanged set, repeatedly restarting AutoAcademic cannot repair that server-side account state.

 Field results

The field-proven Academic engine completed **26 of 29 selected contracts** in one large Grey Hack Public run and continued through three access failures. In a separate observed job, AdminMonitor started an active trace and then reported **Active Trace cancelled** after the operator entered `done` and AutoAcademic performed retained log cleanup.

These are observed results, not a guaranteed success percentage. Random networks can still provide no usable access path.

 Important limits

- Only classic Academic Changes contracts are supported.
- AutoAcademic cannot click, edit, or save the graphical grade fields.
- Mail.exe must already be open; AutoAcademic does not launch it or send the mission reply.
- Typing `done` is the final authority. The script does not verify the grade, reply, customer response, or payment.
- Log finalization covers retained objects AutoAcademic can still control. A machine that never returned access cannot be cleaned through that path.
- The database LAN reference does not guarantee that exact machine is reachable or that it is the only valid viewer host.
- PoisonLib replacement is not automatically restored after use.

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

## Auto Tool Family

The Auto Family is a collection of focused Grey Hack tools designed to work independently while sharing a common foundation. AutoRoute provides a trusted connection path, AutoNet recruits reusable network nodes, AutoDeploy distributes tools, and mission workers such as AutoCred, AutoAcademic, and AutoCorrupt automate their specific job types. Compatible tools organize their files beneath `/root/autoscripts/` and share exact-version exploit knowledge through `/root/vulndb`, so vulnerabilities discovered by one tool can improve the speed and success rate of the others over time.

## UPDATES
All SRC files will be updated over time.
