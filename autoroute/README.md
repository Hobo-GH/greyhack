# AutoRoute 2.1.0-rc1

AutoRoute is the Auto Family's persistent route controller. It builds a trusted SSH chain through owned servers, optionally extends that chain through verified root-SSH nodes collected by AutoNet, and collapses the temporary proxy layer in reverse order while replacing retained computer logs and every available router log.

This release candidate contains two required, version-matched sources:

- [`autoroute-2.1.0-rc1.src`](autoroute-2.1.0-rc1.src) — the controller, saved-route manager, terminal, and cleanup engine.
- [`autoroute-proxy-helper-2.1.0-rc1.src`](autoroute-proxy-helper-2.1.0-rc1.src) — a small temporary companion staged only when proxy-router cleanup is attempted.

## Install

Compile both sources on the computer where AutoRoute starts:

```text
/bin/autoroute
/bin/autoroute-proxy-helper
```

Run `autoroute` and enter each owned SSH hop in order. Passwords are masked during entry but must be stored as reusable plaintext inside root-owned in-game route files.

## Commands

```text
nodes              list verified AutoNet nodes without passwords
extend [count]     add 1-50 random proxy hops; default 3
collapse           clean and release proxy hops, then return to the owned route
clean | clog | logs
                   replace logs across every active route layer
open               open another terminal at the current endpoint
status             show route and cleaner readiness
rebuild            collapse, clean, and reconnect the saved route
setup              replace the saved owned route
quit               final cleanup and exit
```

## Route stores

```text
/root/autoscripts/network/owned-route.txt
/root/autoscripts/autonet/nodes/
```

AutoRoute owns the first store and reads—but never edits—the second.

## Release notes

### 2.1.0-rc1

- Raises the temporary proxy ceiling from 12 to 50 nodes.
- Repairs cleanup ordering so the proxy helper's self-removal cannot become the final surviving log entry.
- Preserves owned-route and AutoNet-node separation, reverse-order proxy collapse, route rebuild, and interactive cleanup controls.
- Publishes only the matched 2.1.0 controller/helper pair; never mix helper versions.

## Cleanup boundary

Every retained proxy must provide a usable computer cleanup object. Physical-router cleanup is best effort and reported separately. `collapse` releases each proxy shell before applying its final retained cleanup object, because later disconnect or file activity can recreate evidence.

The public controller leaves `HOME_ROUTER_PASSWORD = ""`. A private copy may fill it to escalate cleanup on a guest-only home-router shell. Never publish a filled private copy. AutoRoute protects the route; mission workers remain responsible for their own targets.
