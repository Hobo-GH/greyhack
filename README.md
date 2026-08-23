## AutoNet

AutoNet is the SSH recruiter for the Auto script family. Run it from the final owned server opened by AutoRoute. It searches random public routers for SSH services, uses the shared vulnerability database, proves that the recovered root password works through a fresh SSH login, requires target-computer and owned execution-route cleanup, and then saves the machine as a reusable proxy node. Target-router cleanup is attempted and recorded but is no longer allowed to discard an otherwise verified node when the owned execution-route chain break is clean.

AutoNet does not touch AutoRoute's trusted `owned-route.txt`. Its node database is kept separately at:

`/root/autoscripts/autonet/nodes`

 Commands

```text
autonet
autonet hunt [verified-node goal] [random-candidate budget]
autonet nodes
autonet remove [index]
autonet deny <public IP>
autonet help
```

Examples:

```text
autonet hunt 1 250
autonet hunt 5 1000
autonet nodes
autonet remove 3
```

`autonet nodes` never displays passwords. `autonet remove` requires an exact confirmation, removes every matching saved record during the shard rebuild, and adds the public IP to the denylist so it cannot be rediscovered.

 Installation and first run

1. Compile `autonet-0.1.1-dev.src` as `/bin/autonet` on AutoRoute's final owned server.
2. Confirm that `/lib/metaxploit.so` and `/lib/crypto.so` exist on that server.
3. Keep AutoRoute resident on home so the trusted owned route remains available for emergency cleanup.
4. Start with `autonet hunt 1 250`.
5. Inspect `autonet nodes` and `/root/autoscripts/autonet/logs/latest.txt` after the run.

The development build scans unknown SSH libraries and adds what it learns to the shared ACVDB3 database under `/root/vulndb`. Known exact library versions are reused on later runs by AutoNet, AutoCred, AutoAcademic, and other compatible Auto-family tools.

 Important limits

- A root shell is not enough. AutoNet reconnects with a recovered root password before considering the node reusable.
- Target-computer cleanup and execution computer/router cleanup are mandatory. Target-router cleanup is best-effort; its actual `yes` or `no` result is stored with the admitted node.
- Failed exploitation can leave evidence on a candidate that AutoNet never controlled. The script reports that risk and cleans the execution server and its router before continuing.
- Node credentials are stored in plaintext inside the game because AutoRoute Stage 2 needs unattended SSH reuse. Keep the AutoNet folder root-owned and do not publish its runtime shards.

## AutoRoute

AutoRoute is the Auto Family's persistent Grey Hack route controller. It builds a trusted SSH chain through the player's owned servers, optionally extends that chain through verified root-SSH nodes collected by AutoNet, and collapses the temporary proxy layer in reverse order while replacing every retained computer log and every available router log.

AutoRoute 2.0.0 is a two-source release:

- `autoroute-2.0.0.src` is the controller. It owns setup, connections, cleanup, terminal access, and commands.
- `autoroute-proxy-helper-2.0.0.src` is the small companion staged beyond the owned route only when router cleanup is attempted. It contains no owned-route setup, saved SSH state, AutoNet records, interactive controller, or private escalation override.

 Install

Compile both release sources on the computer where AutoRoute starts:

```text
/bin/autoroute
/bin/autoroute-proxy-helper
```

Run `autoroute` and enter each owned SSH hop in order. Passwords are masked during entry and never printed. The saved owned route and AutoNet node records necessarily contain reusable plaintext credentials inside root-owned in-game files so unattended SSH connections can work.

The public controller leaves `HOME_ROUTER_PASSWORD = ""`. A private copy may fill that value to escalate a guest-only shell on the execution computer's physical router. Never publish a filled private copy. The controller remains confined to home and the trusted owned route; only the separate companion helper is copied to proxy nodes.

 Separate route stores

```text
/root/autoscripts/network/
|-- index.txt
`-- owned-route.txt

/root/autoscripts/autonet/nodes/
|-- index.txt
`-- ssh-0001.txt ...
```

`owned-route.txt` contains operator-entered trusted infrastructure. AutoNet owns the isolated proxy-node database on the final owned server. AutoRoute reads verified nodes from that database but never adds, edits, removes, or denies them.

 Commands

- `nodes` lists verified AutoNet proxy nodes without printing passwords.
- `extend [count]` adds 1-12 randomly selected proxy hops; the default is 3.
- `collapse` releases proxy hops deepest-first, performs final cleanup, and returns to the final owned server.
- `clean`, `clog`, or `logs` replaces logs across every currently retained proxy and owned layer.
- `open` opens another terminal at the current route endpoint.
- `status` shows route state and computer/router cleaner readiness.
- `rebuild` collapses, cleans, and reconnects the saved owned route.
- `setup` collapses, cleans, and replaces the saved owned route.
- `quit` performs final collapse and cleanup before closing AutoRoute.

 Cleanup boundary

Every proxy computer must provide a usable cleanup object or AutoRoute refuses to retain it. Physical-router cleanup remains best effort and is reported separately. Later activity can create fresh evidence, so `collapse` releases each retained proxy shell before applying its final retained cleanup object.

AutoRoute protects its route; it does not replace mission-target cleanup performed by AutoCred, AutoAcademic, AutoCorrupt, or another tool.

 Verification

The Stage 2 engine completed a live five-node AutoNet extension, opened the fifth-node terminal, wiped the inspected fifth proxy's `/var/system.log`, collapsed nodes 5 through 1 with successful post-disconnect computer cleanup returns, cleaned home and both owned servers and routers, and restored the Server B terminal. All five physical proxy routers were explicitly reported as best effort.

The 2.0.0 release preserves that route and cleanup flow while splitting proxy-router work into the credential-free companion. Both stable sources pass Greybel build. The split-helper transport itself still needs one short in-game `extend 1` then `collapse` smoke run.

 Release files

- Public controller: `release/2.0.0/autoroute-2.0.0.src`
- Public helper: `release/2.0.0/autoroute-proxy-helper-2.0.0.src`
- Personal template: `personal/2.0.0/autoroute-2.0.0-personal.src`
- Greybel builds: `build/2.0.0/`
- Preserved field evidence: `tests/field/FIELD-RUN-2.0.0-dev1.md`


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

# AutoTrash

AutoTrash is the Auto-family “I am not deleting all of that by hand” utility for Grey Hack. One command empties the conventional trash folders available to the active account while preserving every `.Trash` folder itself.

```text
autotrash
autotrash preview
autotrash --dry-run
autotrash help
```

- Running as `root` cleans `/root/.Trash` and direct `/home/<account>/.Trash` folders.
- Running as another account cleans only `/home/<active-user>/.Trash`.
- `preview` and `--dry-run` list the top-level deletion targets without changing anything.

AutoTrash does not accept a path argument and does not search `/` for every folder named `.Trash`. It validates the complete account scope before deleting, operates only on direct children of an approved trash root, uses Grey Hack's recursive folder deletion for nested trash folders, verifies the roots afterward, and reports anything left behind.

The supplied `trashclean-0.1.0.src` prototype is preserved unchanged under `reference/original`. AutoTrash replaces its whole-filesystem scan, unconditional `is_symlink` dependency, versioned command name, and file-only deletion behavior with the bounded Auto-family implementation.

 AutoSentry interaction

AutoSentry will correctly report the removed trash contents as persistent deletions. Review those alerts and use `autosentry accept` only when the cleanup is known to be intentional and safe.

AutoTrash is destructive by design. Use `preview` when there is anything in the trash you may want to recover.

# AutoSentry

AutoSentry is a persistent full-system integrity monitor for Grey Hack. It saves a trusted filesystem baseline beneath `/root/autoscripts/sentry`, compares the machine against that baseline whenever it starts, reports only what was added, deleted, or modified, and then continues watching filesystem and process activity live.

Unlike the earlier Watchdog builds, AutoSentry can detect changes made while it was not running. It does not print a full filesystem tree. Dot-prefixed files and folders are included: a new or altered path such as `/root/.Trash/payload` is explicitly reported as `HIDDEN`.

 Commands

```text
autosentry
autosentry <refresh_seconds>
autosentry check
autosentry accept
autosentry help
autosentry -h
autosentry --help
```

- `autosentry` compares the saved baseline, then begins live monitoring with a one-second delay.
- `autosentry <refresh_seconds>` uses a custom live delay of at least 0.1 seconds.
- `autosentry check` performs one persistent comparison and exits.
- `autosentry accept` reviews current differences and requires the exact word `ACCEPT` before replacing the trusted state. If the saved baseline is damaged, the same command requires `REBUILD` instead.

The first run creates the initial trusted baseline automatically. Later additions, deletions, and modifications are never trusted merely because AutoSentry observed them.

 What it detects

- Files and folders added or removed anywhere exposed by the File API
- Readable text-content changes using MD5
- Type, permissions, owner, group, size, binary-state, and symlink-target changes
- Hidden dot-path changes
- Live process starts, stops, and PID reuse
- Filesystem and process enumeration problems

Grey Hack does not expose binary contents through the current File API, so a same-path binary replacement is detectable only when exposed metadata also changes. Live polling can also miss an action that is created and fully reversed between two completed scans.

 Baseline storage

AutoSentry uses verified, sharded, double-bank storage:

```text
/root/autoscripts/sentry/
├── index.txt
├── baseline-a/
│   └── shard-0001.txt
└── baseline-b/
    └── shard-0001.txt
```

It writes a complete new snapshot to the inactive bank, verifies every shard, and updates the index last. AutoSentry's own managed index and shard files are excluded from alerts; the state folders and unexpected files placed beside those shards are still monitored.

If the earlier Sentry candidate created `/root/sentry`, run `/bin/autosentry` once. AutoSentry copies both banks and the index, verifies the migrated baseline, and only then removes the exact legacy managed structure. It refuses cleanup if unexpected data is present.

 Stable release

`1.0.0` is the field-verified stable release. It corrects both halves of the pipe-delimited state format: readers use the regex-safe `[|]` pattern, and the encoder escapes literal pipes without treating `|` as an empty regular-expression alternative. When it encounters the uniform character-by-character pipe corruption created by an earlier development build, it repairs only the trusted saved representation, verifies the rewritten bank, and then performs the real comparison. It never substitutes the current filesystem for the trusted baseline, and it refuses mixed or ambiguous corruption.

The stable engine repaired and reloaded an existing 397-entry baseline in Grey Hack Public, reported a clean persistent comparison, entered live watch with zero scan issues, and then correctly reported hidden-file deletion and ordinary-file additions. The release source differs from the field-proven `1.0.0-dev5` source only in its displayed version label.

AutoSentry `1.0.0` passes the Greybel build and the release pipe-safety checks. The supplied Watchdog, FullTree, and legacy Watchdog references remain preserved and unchanged.


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

## FullTree

FullTree is a read-only Grey Hack terminal utility that prints a detailed, sorted filesystem tree. It can scan from / or a chosen path, supports paged output for large directories, and displays symlinks without following them when supported by the runtime.

## Auto Tool Family

The Auto Family is a collection of focused Grey Hack tools designed to work independently while sharing a common foundation. AutoRoute provides a trusted connection path, AutoNet recruits reusable network nodes, AutoDeploy distributes tools, and mission workers such as AutoCred, AutoAcademic, and AutoCorrupt automate their specific job types. Compatible tools organize their files beneath `/root/autoscripts/` and share exact-version exploit knowledge through `/root/vulndb`, so vulnerabilities discovered by one tool can improve the speed and success rate of the others over time.

## UPDATES
All SRC files will be updated over time.
