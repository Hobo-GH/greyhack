# AutoCorrupt 1.0.0-rc1-public

AutoCorrupt handles classic **Corrupt Data** Mission Contracts: read the current contract mail, select one or more jobs, attack the public router, reach the requested LAN machine, acquire useful authority, destroy the target filesystem, reboot when available, and perform retained cleanup.

This folder contains a sanitized public release candidate. It deliberately does not contain the private reverse-shell server address, listener port, SSH user, or SSH password used by the field build.

## Configure and install

Copy [`autocorrupt-1.0.0-rc1-public.src`](autocorrupt-1.0.0-rc1-public.src) to a private working file and fill only the infrastructure values you actually use:

```text
RSHELL_SERVER_IP
RSHELL_SERVER_PORT
RSHELL_SERVER_SSH_PORT
RSHELL_SERVER_SSH_USER
RSHELL_SERVER_SSH_PASSWORD
```

Compile the private copy as `/bin/autocorrupt`. Leave `MAIL_USER`, `MAIL_PASSWORD`, and `PIN` blank to use the active mail address and masked prompt. A compatible optional router-jump library may be placed at `/root/PoisonLibs/libhttp.so`.

## Operation

Run `autocorrupt`, enter the MetaMail PIN, and choose indexes or `all`. The worker processes selected classic Corrupt Data contracts, records each route and exploit result, continues after failed jobs, and prints a final result table.

## Runtime data

This repair line writes split diagnostics using the `autocorrupt-debug` prefix and maintains its compatibility vulnerability store at `/root/autocorrupt-vulns.txt`. These are in-game runtime files, not files to upload with the source.

## Release notes

### 1.0.0-rc1-public

- Promoted the simple field worker into its first public release-candidate line.
- Preserved the paid router-to-exact-LAN destruction path, batch continuation, poison-library jump option, reverse-shell continuation, reboot, and retained cleanup.
- Sanitized every private reverse-shell and SSH infrastructure value from the public source.
- Kept the compatibility vulnerability store unchanged pending its next ACVDB3 integration pass.

## Boundaries

- This is a release candidate for real game-world testing, not a stable success-rate guarantee.
- It has completed and paid actual Corrupt Data contracts, but current Grey Hack routers frequently expose only guest authority or no useful shell.
- Reverse-shell continuation and poison-library promotion require player-supplied infrastructure.
- Cleanup can cover only machines and routers for which the script retained a usable object.
