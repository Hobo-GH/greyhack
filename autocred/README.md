# AutoCred 2.2.0

AutoCred automates classic credential Mission Contracts. It reads the current mail snapshot, lets the operator choose indexes or `all`, attacks the exact requested LAN machine, recovers the requested user's password, and prints the result for a manual Mission Contract reply.

It supports named-user `/etc/passwd` recovery, root decipher and re-login, bounded route continuation, remote library scanning, optional PoisonLib router jumps, retained-object log cleanup, and ACVDB3 reuse.

## Install and run

Compile [`autocred-2.2.0.src`](autocred-2.2.0.src) as:

```text
/bin/autocred
```

Run `autocred`, enter the MetaMail PIN, and select one or more jobs. At the selection prompt:

- `fresh` or `refresh` discards the displayed snapshot and fetches current MetaMail data in a short-lived intake process.
- `q` quits.

Recovered passwords are not submitted automatically. Reply to each matching Mission Contract in `Mail.exe` with the printed password.

## Optional configuration

The public source leaves `MAIL_USER`, `MAIL_PASSWORD`, `PIN`, and `POISON_HTTP_SOURCE` blank. Blank mail fields use the active player's address and the masked PIN/password prompt, so most players do not need to edit them. Set `POISON_HTTP_SOURCE` only when a compatible personal router-jump library is available; do not publish private credentials or infrastructure paths.

## Runtime data

```text
/root/autoscripts/credential/tasks/current.txt
/root/autoscripts/credential/logs/latest.txt
/root/vulndb/index.txt
/root/vulndb/<library>/V<major>/shard-NNNN.txt
```

The task file contains only the current run's remaining queue and is cleared after processing. The source in this folder is the canonical 2.2.0 release with isolated fresh-process mail intake; it replaces the older public copy previously stored at the repository root.

## Release notes

### 2.2.0

- Replaced stale task-memory behavior with a current-run queue beneath `/root/autoscripts/credential/`.
- Added isolated mail intake plus explicit `fresh` and `refresh` reloads.
- Adopted the shared ACVDB3 database, Rowan synthwave readouts, and retained-object log cleanup.
- Improved named-user recovery through `/etc/passwd` decipher, root re-login, and exact-target escalation.

## Boundaries

- Procedural Fraud, Sabotage, and Corporate Espionage missions are not classic credential contracts and are ignored.
- Exact-target success depends on reachable services, current library versions, and useful exploit returns.
- One field batch completed 12 of 15 selected harder level-one jobs. That is an observed result, not a guaranteed rate.
