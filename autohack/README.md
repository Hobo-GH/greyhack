# AutoHack 2.5.0

AutoHack is the Auto Family's persistent general-purpose access console. It attacks public services or an exact LAN target, retains useful access instead of immediately opening a terminal, returns to its own console after a target shell closes, and keeps the execution origin and selected target visible in its Rowan circuit prompt.

This release combines shared ACVDB3 reuse, exact-LAN scans without a required port, router control-plane targeting on port `0`, retained sessions, deliberate shell entry, non-stock file discovery, embedded deep Nmap reconnaissance, poison-library promotion, target cleanup, destructive blackout, and local hardening.

## Source files

- [`autohack-2.5.0.src`](autohack-2.5.0.src) — compact source intended for Grey Hack's 160,000-character CodeEditor limit.
- [`autohack-2.5.0-readable.src`](autohack-2.5.0-readable.src) — canonical formatted source for review and maintenance; it is too large to save directly in the current CodeEditor.

Both files print and report version `2.5.0`.

## Install

Compile the compact source as `/bin/autohack`. The execution machine requires:

```text
/lib/metaxploit.so
/lib/crypto.so
```

Optional weak libraries are discovered beneath `/root/PoisonLibs/`.

## Console commands

```text
<ip> [port] [lan-ip]          attack all services or one exact port
target <ip> [port] [lan-ip]   explicit form of the same command
nmap <ip|host> [--quick]      embedded deep topology reconnaissance
sessions                      list retained verified access
where | whoami                show execution origin and selected target
shell [index]                 open retained access and return here on exit
interesting [index]           list non-stock files without reading contents
autoshell [on|off]            control automatic shell entry
poison [status|list|on|off]   inspect or control weak-library promotion
nuke [index]                  destroy one retained root target after confirmation
harden [home|server]          root-lock the execution host with home safeguards
forget [index|all]            release retained access objects
status                        show storage and ACVDB readiness
help                          show the command guide
quit                          clean the execution route and leave AutoHack
```

`<public-ip> <lan-ip>` scans every visible service mapped to that exact LAN machine. `<public-ip> 0 <router-lan-ip>` explicitly targets the router control plane.

## Runtime data

```text
/root/autoscripts/autohack/logs/
/root/vulndb/
/root/PoisonLibs/
```

The public source contains no personal route credentials. `af2026` is an in-game password replacement convention, not an account secret.

## Release notes

### 2.5.0

- Promoted AutoHack from an access experiment into the Auto Family's mature persistent hacking console.
- Added all-service exact-LAN targeting, router port `0`, retained sessions, deliberate shell entry, return-to-console handoff, and visible origin/target state.
- Integrated deep Nmap reconnaissance, ACVDB3 reuse, focused poison-library promotion, non-stock `interesting` inventory, Blackout target destruction, and home/server fortification.
- Added color-coded attack instrumentation and the Rowan Circuit interface while retaining a CodeEditor-safe compact build and a matched readable source.

## Runtime boundary

Exact-target attacks, retained-session return, embedded Nmap, blackout, hardening, and cleanup all have field evidence. Success still depends on the current service map and exploit objects exposed by each library; target-router cleanup remains best effort when no usable router object is returned.
