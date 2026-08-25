# AutoTrash 1.0.0

AutoTrash is the Auto Family's “I am not deleting all of that by hand” utility. One command empties conventional account trash folders while preserving every `.Trash` root.

## Install and commands

Compile [`autotrash-1.0.0.src`](autotrash-1.0.0.src) as `/bin/autotrash`.

```text
autotrash
autotrash preview
autotrash --dry-run
autotrash help
```

- Running as `root` cleans `/root/.Trash` and direct `/home/<account>/.Trash` folders.
- Running as another account cleans only `/home/<active-user>/.Trash`.
- `preview` and `--dry-run` list top-level deletion targets without changing anything.

AutoTrash does not accept an arbitrary path and does not search the whole filesystem for folders named `.Trash`. It validates the entire account scope before deletion, operates only on direct children of approved roots, uses Grey Hack's recursive deletion for nested trash folders, verifies every root afterward, and reports anything left behind.

## Release notes

### 1.0.0

- Replaced the early single-path cleaner with account-aware root and non-root scope.
- Added dry-run preview, direct-child validation, recursive folder cleanup, progress reporting, and post-clean verification.
- Preserves every conventional `.Trash` root while emptying its contents.

## Safety

AutoTrash is destructive by design. Use `preview` whenever the trash contains anything you may want to recover. AutoSentry will correctly report the cleanup as persistent deletions; accept those baseline changes only after reviewing them.

The stable field run removed 70 top-level entries from two conventional trash roots with no deletion or verification failures while preserving both roots. Non-root scope and exposed-symlink cleanup were not exercised in that promotion.
