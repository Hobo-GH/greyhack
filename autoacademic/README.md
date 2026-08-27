# AutoAcademic

`/bin/autoacademic` automates classic Academic Changes missions around the graphical steps GreyScript cannot perform.

Run the command, enter the MetaMail PIN, and choose one or more contracts. AutoAcademic merges the current game-provided mail snapshot with its unresolved contract queue, attacks each contract's public network, and accepts any useful machine on that network. A named-user foothold is escalated to root before the viewer is launched. The database LAN IP is displayed as a reference; it is not treated as the required compromise target.

When the viewer opens, the operator performs three actions: change and save the displayed grade, reply to the original Mission Contract in an already-open `Mail.exe`, then return to the terminal and enter `done`. AutoAcademic removes that completed task from its queue, closes the viewer, waits for its disconnect log, overwrites remote logs through retained file objects, and continues. Access or cleanup failures are recorded and the batch moves to the next selected contract.

Field-proven engine: `0.1.0-live5`. A 29-contract Public field run completed 26 jobs, continued through three access failures, and demonstrated active-trace cancellation after retained log cleanup. This is one observed run, not a guaranteed success rate.

Current owner-accepted line: `2.0.4`. Version `2.0.2` established the exact Auto Family operational-output standard; `2.0.3` added labeled PIN/help/selection refinements, and `2.0.4` carries the owner's final centered circuit without changing the accepted mission stream. Purple identifies actions and exploit surfaces; cyan identifies hosts, ports, libraries, and destinations; green identifies retained or completed work; red identifies refusal and failure; orange identifies payload techniques, cleanup, paths, and operator attention; pink identifies people, authority, indexes, and selections.

The preserved engine removes automatic `Mail.exe` launching, uses the command-safe Auto Family data hub, participates in ACVDB3, and prints batch progress. Its mail loader launches a short-lived copy of `/bin/autoacademic` in intake-only mode so startup, `refresh`, and `fresh` receive a newly created MetaMail object instead of intentionally reusing Public's immutable in-process snapshot. Version 2.0.0, Live5, and all development predecessors remain preserved in Git history.

## Install

Set a private `PIN` in `autoacademic-2.0.4.src`, then compile it as `/bin/autoacademic`. `MAIL_USER`, `MAIL_PASSWORD`, and every optional reverse-shell server field are intentionally blank in this public source. If the MetaMail password matches the PIN, `MAIL_PASSWORD` may remain blank and the entered PIN is reused.

## Runtime files

- `/root/autoscripts/academic/tasks/current.txt` - unresolved Academic Changes queue.
- `/root/autoscripts/academic/logs/latest.txt` - newest diagnostic log.
- `/root/autoscripts/academic/logs/latest-partN.txt` - rotated parts of the same run.
- `/root/vulndb/index.txt` - shared family database index.
- `/root/vulndb/<library>/V<major>/shard-NNNN.txt` - packed exact-version vulnerability records.

Version 2.0.4 preserves 2.0.0's storage behavior: it creates missing folders in place and does not move, rename, or delete old app data. Short-lived mail-intake request and snapshot files are created under the Academic task folder and removed after each handoff. If a legacy ACVDB1 or ACVDB2 database is present before ACVDB3 exists, its vulnerability records can be imported while the original files remain untouched. Existing unresolved task data is moved only when the operator chooses to copy it manually.

The Auto Family is a collection of focused Grey Hack tools designed to work independently while sharing a common foundation. AutoRoute provides a trusted connection path, AutoNet recruits reusable network nodes, AutoDeploy distributes tools, and mission workers such as AutoCredential, AutoAcademic, and AutoCorrupt automate their specific job types. Compatible tools organize their files beneath `/root/autoscripts/` and share exact-version exploit knowledge through `/root/vulndb`, so vulnerabilities discovered by one tool can improve the speed and success rate of the others over time.
