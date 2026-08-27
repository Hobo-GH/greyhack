# AutoSentry

AutoSentry is a persistent full-system integrity monitor for Grey Hack. It saves a trusted filesystem baseline beneath `/root/autoscripts/sentry`, compares the machine against that baseline whenever it starts, reports only what was added, deleted, or modified, and then continues watching filesystem and process activity live.

Current release version: `1.1.2`. It keeps the owner-accepted baseline, monitoring, and startup Y/N flow from `1.1.1` and promotes the owner's final circuit geometry without changing operational behavior.

## Install

Set a private `PIN` in `autosentry-1.1.2.src`, then compile it as `/bin/autosentry`. The public source intentionally contains no preinstalled PIN.

Unlike the earlier Watchdog builds, AutoSentry can detect changes made while it was not running. It does not print a full filesystem tree. Dot-prefixed files and folders are included: a new or altered path such as `/root/.Trash/payload` is explicitly reported as `HIDDEN`.

## Commands

```text
autosentry
autosentry <refresh_seconds>
autosentry check
autosentry accept
autosentry help
autosentry -h
autosentry --help
```

- `autosentry` compares the saved baseline, offers `Y/N` when changes exist, then begins live monitoring with a one-second delay.
- `autosentry <refresh_seconds>` uses the same startup decision with a custom live delay of at least 0.1 seconds.
- `autosentry check` performs one persistent comparison and exits.
- `autosentry accept` reviews current differences and requires the exact word `ACCEPT` before replacing the trusted state. If the saved baseline is damaged, the same command requires `REBUILD` instead.

The first run creates the initial trusted baseline automatically. On later normal runs, `Y` writes and verifies the reviewed current state in the inactive bank before committing it as trusted; `N` preserves the existing baseline. The explicit `autosentry accept` and invalid-baseline `REBUILD` paths remain available and unchanged.

The public source intentionally ships with `PIN = ""`; configure it before compiling or AutoSentry remains locked.

## What it detects

- Files and folders added or removed anywhere exposed by the File API
- Readable text-content changes using MD5
- Type, permissions, owner, group, size, binary-state, and symlink-target changes
- Hidden dot-path changes
- Live process starts, stops, and PID reuse
- Filesystem and process enumeration problems

Grey Hack does not expose binary contents through the current File API, so a same-path binary replacement is detectable only when exposed metadata also changes. Live polling can also miss an action that is created and fully reversed between two completed scans.

## Baseline storage

AutoSentry uses verified, sharded, double-bank storage:

```text
/root/autoscripts/sentry/
├── index.txt
├── baseline-a/
│   └── shard-0001.txt
└── baseline-b/
    └── shard-0001.txt
```

It writes a complete new snapshot to the inactive bank, verifies every shard, and updates the index last. AutoSentry's own managed index, shards, and exact diagnostic log are excluded from alerts so the monitor cannot report itself. Unexpected files placed beside the managed state remain visible.

If the earlier Sentry candidate created `/root/sentry`, run `/bin/autosentry` once. AutoSentry copies both banks and the index, verifies the migrated baseline, and only then removes the exact legacy managed structure. It refuses cleanup if unexpected data is present.

## Releases

`1.0.0` remains the field-verified engine reference. It corrects both halves of the pipe-delimited state format: readers use the regex-safe `[|]` pattern, and the encoder escapes literal pipes without treating `|` as an empty regular-expression alternative. When it encounters the uniform character-by-character pipe corruption created by an earlier development build, it repairs only the trusted saved representation, verifies the rewritten bank, and then performs the real comparison. It never substitutes the current filesystem for the trusted baseline, and it refuses mixed or ambiguous corruption.

The stable engine repaired and reloaded an existing 397-entry baseline in Grey Hack Public, reported a clean persistent comparison, entered live watch with zero scan issues, and then correctly reported hidden-file deletion and ordinary-file additions.

`1.1.0` preserves that engine and changes the controlled presentation and diagnostics layer. Real owner runs showed that the large report correctly separated additions, modifications, and the `.Trash` content removed by AutoTrash; after explicit acceptance, bank B loaded 352 trusted items, the persistent comparison returned zero changes, and live watch began normally. A file moved to trash while AutoSentry was stopped was then correctly reported at the next startup as deletion of `/NewFile` plus addition of `/root/.Trash/NewFile`, confirming persistent comparison rather than only live polling.

`1.1.1` changes only the normal startup decision described above. Its real run reported three additions and one deletion, presented `Accept these changes? [Y/N]`, promoted the current state after `Y`, and returned clean on the next startup. It does not alter scanning, comparison, A/B bank selection, explicit `ACCEPT`, invalid-baseline `REBUILD`, process watching, or alert classification.

`1.1.2` is the owner-accepted release. It promotes the corrected circuit with a joined upper feed and closed Bank B return; the field-used `1.1.1` build and `1.1.2` differ only in the displayed version. The GitHub-ready source passes the local parser and compatibility audit with zero findings and contains no preinstalled PIN. All supplied Watchdog, FullTree, legacy Watchdog, and earlier AutoSentry sources remain preserved.
