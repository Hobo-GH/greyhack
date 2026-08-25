# AutoAcademic 2.0.0

AutoAcademic automates classic **Academic Changes** Mission Contracts around the graphical steps GreyScript cannot perform. It gathers current contracts, attacks the public network, escalates a useful named-user foothold to root when possible, launches `StudentsViewer.exe`, selects the requested student, and cleans retained remote logs after the operator finishes.

This is intentionally not a completely hands-free script. For each accessible job, the operator must:

1. Change and save the requested grade in `StudentsViewer.exe`.
2. Reply to the original Mission Contract in an already-open `Mail.exe`.
3. Return to AutoAcademic and type `done`.

AutoAcademic trusts those three actions when `done` is entered, finalizes cleanup, removes the completed task from the unresolved queue, and continues through the selected batch. Access failures are recorded without stopping later jobs.

## Install and run

Compile [`autoacademic-2.0.0.src`](autoacademic-2.0.0.src) as:

```text
/bin/autoacademic
```

Run `autoacademic`, enter the MetaMail PIN, then choose one or more indexes or `all`. At the selection prompt:

- `refresh` merges a newly fetched snapshot with unresolved queued jobs.
- `fresh` forgets the unresolved queue and uses only the newly fetched snapshot.
- `q` quits.

Keep `Mail.exe` open yourself; this release does not launch another Mail window.

## Runtime data

```text
/root/autoscripts/academic/tasks/current.txt
/root/autoscripts/academic/logs/latest.txt
/root/autoscripts/academic/logs/latest-partN.txt
/root/vulndb/index.txt
/root/vulndb/<library>/V<major>/shard-NNNN.txt
```

The script creates missing folders in place. It uses the shared ACVDB3 vulnerability database and can import older family records without deleting the originals.

## Release notes

### 2.0.0

- Moved tasks and diagnostics beneath organized `/root/autoscripts/academic/` folders.
- Adopted the shared, version-sharded ACVDB3 database used by the Auto Family.
- Added resilient mail intake, `fresh`/`refresh` queue control, batch continuation after failures, and supervised `done` handoff.
- Removed automatic Mail launching; the operator keeps one Mail window open for the required reply.

## Boundaries

- The database LAN IP is a reference, not necessarily the machine that must be compromised; any suitable system on the school network may provide the shared viewer.
- GUI grade editing and the Mission Contract reply remain manual.
- Success depends on current network topology, available services, and useful exploit returns.
- The release preserves the field-proven batch engine that completed 26 of 29 jobs in one observed run; that run is evidence, not a guaranteed rate.
