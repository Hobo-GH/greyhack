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

## UPDATES
All SRC files will be updated over time.
