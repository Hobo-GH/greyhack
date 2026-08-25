# FullTree 1.0.0

FullTree is a read-only Grey Hack terminal utility that prints a detailed, sorted filesystem tree. It scans from `/` by default, accepts another starting path, supports paged output, and displays symlinks without following them when the runtime exposes symlink metadata.

It creates no report, configuration, cache, or log file.

## Install and commands

Compile [`fulltree-1.0.0.src`](fulltree-1.0.0.src) as `/bin/tree`.

```text
tree
tree <path>
tree <path> --page <lines>
tree help
tree -h
tree --help
```

Examples:

```text
tree
tree /bin
tree /bin --page 30
```

The final summary reports directories, files, symlinks, binaries, unknown items, and enumeration/metadata issues. Red issue lines identify incomplete observations.

## Release notes

### 1.0.0

- Promotes the terminal-native recursive inventory utility as the first stable release.
- Adds sorted iterative traversal, optional starting paths, paged output, hidden-path visibility, and explicit observation summaries.
- Remains completely read-only and does not create report or configuration files.

## Observation boundary

Run as root for the broadest filesystem view. An unprivileged account may not see inaccessible items. Some Grey Hack runtimes do not expose `is_symlink`; when unavailable, FullTree reports that symlink classification cannot be guaranteed.
