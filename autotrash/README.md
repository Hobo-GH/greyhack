# AutoTrash

AutoTrash is the Auto-family “I am not deleting all of that by hand” utility for Grey Hack. One command empties the conventional trash folders available to the active account while preserving every `.Trash` folder itself.

This is the GitHub-ready `1.1.1` source. Set a private value for `PIN`, then compile `autotrash-1.1.1.src` as `/bin/autotrash`.

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

## AutoSentry interaction

AutoSentry will correctly report the removed trash contents as persistent deletions. Review those alerts and use `autosentry accept` only when the cleanup is known to be intentional and safe.

AutoTrash is destructive by design. Use `preview` when there is anything in the trash you may want to recover.

## Stable release

AutoTrash `1.0.0` is the field-verified stable release. In its root-mode Grey Hack Public run it discovered two conventional trash roots, removed 70 top-level entries consisting of 67 files and 3 folders, preserved both `.Trash` roots, and finished with zero deletion failures, zero remaining entries, and zero verification issues. AutoSentry independently observed the expected trash-content deletions.

The stable source differs from the field-tested `1.0.0-dev1` engine only in its displayed version label. The non-root-only scope, preview mode, and a cleanup containing an exposed symlink were not exercised during this promotion.

## Family-interface version 1.1.1

`1.1.1` leaves the owner-accepted cleanup engine intact. It carries forward the unique AutoTrash Rowan circuit, mandatory masked PIN activation, clear front-page guide, origin and account-scope identity, exact Auto Family semantic palette, structured cleanup and verification records, and concise diagnostic log at `/root/autoscripts/autotrash/logs/latest.txt`. Its only change from the accepted `1.1.0` run is the owner's corrected circuit geometry and the required version promotion.

AutoTrash remains a one-shot bounded utility rather than a persistent console. Its cleanup-specific event records are a narrow tool exception because account-trash discovery, direct-child validation, and preserved `.Trash` roots have no equivalent AutoAcademic hacking event. The GitHub-ready `1.1.1` source is static-parse accepted and contains no preinstalled PIN.
