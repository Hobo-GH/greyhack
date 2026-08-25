# Nmap Synthwave Deep Recon 1.0.1

Nmap Synthwave is a thorough, read-only network reconnaissance tool. It combines visible-port scanning with public identity, routers and switches, wireless identity, router control planes, firewall rules, visible and hidden forwarding, LAN nodes, likely internal service mappings, switch edges, coverage gaps, pivot guidance, and a final scan summary.

It does not exploit targets, open sessions, write files, call `net_use`, or modify network configuration.

## Install and commands

Compile [`nmap-synthwave-1.0.1.src`](nmap-synthwave-1.0.1.src) as `/bin/nmap`.

```text
nmap <ip_address|domain>
nmap --quick <ip_address|domain>
nmap help
nmap -h
nmap -help
nmap --help
```

Full mode is the default. It includes bounded 0-65535 router-forward sweeps and direct-subnet discovery when the current vantage permits them. Quick mode omits those exhaustive passes while retaining exposed port, identity, and topology views.

The help system expands with each dash: `help` is compact, `-h` adds syntax and examples, `-help` explains modes and report sections, and `--help` provides the full observation-boundary and interpretation reference.

## Release notes

### 1.0.1

- Added the graduated `help`, `-h`, `-help`, and `--help` reference system.
- Preserved the full synthwave topology engine, quick mode, exhaustive forwarding discovery, gap reporting, and read-only boundary.
- Standardized the public version label and source filename for release.

## Observation boundary

Results are complete only for data visible from the execution vantage. An external scan cannot prove what exists behind a nested firewall or a game-hidden LAN identity. Nmap reports those gaps explicitly and recommends scanning again from an internal foothold rather than presenting absence as certainty.
