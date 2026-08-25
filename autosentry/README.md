# AutoSentry 1.0.0

AutoSentry is a persistent full-system integrity monitor. It saves a trusted filesystem baseline, compares the current machine with that baseline whenever it starts, reports only additions, deletions, and modifications, then continues watching filesystem and process activity live.

Unlike a simple live watcher, AutoSentry can detect changes made while it was not running. It includes dot-prefixed hidden paths and does not print a full filesystem tree.

## Install and commands

Compile [`autosentry-1.0.0.src`](autosentry-1.0.0.src) as `/bin/autosentry`.

```text
autosentry
autosentry <refresh_seconds>
autosentry check
autosentry accept
autosentry help
autosentry -h
autosentry --help
```

- `autosentry` compares the saved baseline and starts live monitoring.
- `autosentry <refresh_seconds>` uses a custom delay of at least 0.1 seconds.
- `autosentry check` performs one persistent comparison and exits.
- `autosentry accept` requires `ACCEPT` before trusting reviewed changes, or `REBUILD` when the saved baseline is invalid.

The first run creates the initial baseline automatically. Later changes are never trusted merely because AutoSentry observed them.

## Release notes

### 1.0.0

- Rebuilt legacy Watchdog as a persistent two-bank integrity monitor.
- Added trusted-state validation, hidden-path coverage, offline-change detection, and explicit `accept`/`REBUILD` gates.
- Added live filesystem and process monitoring without printing a full tree.
- Corrected baseline encoding so unchanged systems no longer appear simultaneously added and deleted.

## Detection

AutoSentry reports files and folders added or removed, readable text-content changes, exposed metadata changes, hidden dot paths, process starts/stops/PID reuse, and enumeration problems. Grey Hack does not expose binary contents through the File API, so a same-path binary replacement requires an exposed metadata change to be visible. Activity created and fully reversed between two scans can also be missed.

## Baseline storage

```text
/root/autoscripts/sentry/index.txt
/root/autoscripts/sentry/baseline-a/shard-0001.txt
/root/autoscripts/sentry/baseline-b/shard-0001.txt
```

AutoSentry writes and verifies the inactive bank before switching the index. Its exact managed state files are excluded from alerts; unexpected files beside them remain monitored.

AutoTrash cleanup will correctly appear as deletions. Use `autosentry accept` only after reviewing intentional changes.
