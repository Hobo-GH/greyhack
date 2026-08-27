# AutoRoute

AutoRoute is the Auto Family's persistent Grey Hack route controller. It builds a trusted SSH chain through the player's owned servers, optionally extends that chain through verified root-SSH nodes collected by AutoNet, and collapses the temporary proxy layer in reverse order while replacing every retained computer log and every available router log.

AutoRoute 2.1.1 is a two-source tool:

- `autoroute-2.1.1.src` is the controller. It owns PIN entry, setup, connections, cleanup, terminal access, the AutoDeploy handoff, and commands.
- `autoroute-proxy-helper-2.1.1.src` is the small companion staged beyond the owned route only when router cleanup is attempted. It contains no PIN, owned-route setup, saved SSH state, AutoNet records, interactive controller, or private escalation override.

## Install

Compile both release sources on the computer where AutoRoute starts:

```text
/bin/autoroute
/bin/autoroute-proxy-helper
```

Set `PIN` in the personal controller, run `autoroute`, enter the labeled masked PIN, and enter each owned SSH hop in order on first use. Passwords are masked during entry and never printed. The saved owned route and AutoNet node records necessarily contain reusable plaintext credentials inside root-owned in-game files so unattended SSH connections can work.

The GitHub-ready controller leaves both `PIN = ""` and `HOME_ROUTER_PASSWORD = ""`. A personal copy may fill those values; the router password is used only to escalate a guest-only shell on the execution computer's physical router. Never publish a filled private copy. The controller remains confined to home and the trusted owned route; only the separate companion helper is copied to proxy nodes.

## Separate route stores

```text
/root/autoscripts/network/
|-- index.txt
|-- owned-route.txt
`-- active-proxy-route.txt

/root/autoscripts/autonet/nodes/
|-- index.txt
`-- ssh-0001.txt ...
```

`owned-route.txt` contains operator-entered trusted infrastructure. AutoNet owns the isolated proxy-node database on the final owned server. AutoRoute reads verified nodes from that database but never adds, edits, removes, or denies them.

## Commands

- `nodes` lists verified AutoNet proxy nodes without printing passwords.
- `extend [count]` adds 1-50 randomly selected proxy hops; the default is 3.
- `collapse` releases proxy hops deepest-first, performs final cleanup, and returns to the final owned server.
- `clean`, `clog`, or `logs` replaces logs across every currently retained proxy and owned layer.
- `open` opens another terminal at the current route endpoint.
- `status` shows route state and computer/router cleaner readiness.
- `rebuild` collapses, cleans, and reconnects the saved owned route.
- `setup` collapses, cleans, and replaces the saved owned route.
- `help` shows the front-page guide again.
- `quit` performs final collapse and cleanup before closing AutoRoute.

The persistent terminal signature reads from origin through the final owned endpoint to the current proxy endpoint and shows whether the AutoDeploy handoff is empty or ready. Network values remain cyan, authority pink, success green, cleanup and warnings orange, and genuine failures or residual risk red.

## Cleanup boundary

Every proxy computer must provide a usable cleanup object or AutoRoute refuses to retain it. Physical-router cleanup remains best effort and is reported separately. Later activity can create fresh evidence, so `collapse` releases each retained proxy shell before applying its final retained cleanup object.

AutoRoute protects its route; it does not replace mission-target cleanup performed by AutoCredential, AutoAcademic, AutoCorrupt, or another tool.

## Verification

The Stage 2 engine completed a live five-node AutoNet extension, opened the fifth-node terminal, wiped the inspected fifth proxy's `/var/system.log`, collapsed nodes 5 through 1 with successful post-disconnect computer cleanup returns, cleaned home and both owned servers and routers, and restored the Server B terminal. All five physical proxy routers were explicitly reported as best effort.

The 2.0.0 release preserved that route and cleanup flow while splitting proxy-router work into the credential-free companion. The later 2.1.0-dev1 real run established three AutoNet proxies, published the ordered `ASPROXY1` handoff with the final proxy last, cleaned the required owned and proxy computers, and collapsed back to the owned route. Physical proxy-router cleanup remained explicitly best effort.

Plain 2.1.0 preserves that field-proven engine and the corrected dev2 Rowan circuit. It adds the labeled masked PIN gate, front-page guide, exact AutoAcademic attack/result branches, and semantically structured route, cleanup, status, and handoff readouts. Both sources passed the local compatibility audit and static GreyScript parser before the first ordinary in-game route use exposed the runtime fault recorded below.

That ordinary run exposed one presentation-only crash: early router-clean helper execution reached an attack before the normal controller startup created `visual_attack_index`. Version 2.1.1 checks whether the map key exists before reading it. No routing, cleanup, handoff, credential, circuit, help, color, or event-layout behavior was redesigned. Both 2.1.1 sources pass the same cheap compatibility and parser checks.

The next real route run passed that failure point, loaded the two-hop owned route, extended and collapsed five proxy hops, restored the ready handoff and terminal state, and completed owned-route cleanup. Physical proxy routers remained explicitly labeled best effort, as designed. The owner accepted AutoRoute 2.1.1 on 2026-08-26; under `Trust Me`, this version is complete unless a new field need or defect is reported.

## Included files

- `autoroute-2.1.1.src` — public controller with private configuration blank.
- `autoroute-proxy-helper-2.1.1.src` — credential-free matched helper. Always compile and deploy the controller and helper from the same version.
