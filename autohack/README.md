# AutoHack

AutoHack is the Auto Family's targeted access tool for Grey Hack Public v0.9.6773. Give it a public IP and, optionally, an exact port and expected LAN IP. It maps visible services, consults the shared ACVDB3 vulnerability database before scanning, ranks known exploits, recovers and reuses root credentials without printing them, and retains the strongest usable target shell in an indexed session list.

Current packaged version: `3.0.0`. It is the clean-rebuild successor to the older public `2.5.0` line, preserves the complete `0.1.0-dev15` engine and personality, and applies the locked Auto Family presentation standard. No attack method, cleanup path, retained-session feature, inventory behavior, PoisonLib promotion, Blackout gate, fortification gate, or embedded Nmap capability was removed or reduced.

## Install

Set a private `PIN` in `autohack-3.0.0.src`, then compile that compact source as `/bin/autohack`. The separate `autohack-3.0.0-readable.src` is provided for source review but exceeds CodeEditor's character limit and is not the compile target.

Successful access does not unexpectedly replace the AutoHack console. Use `shell` to open the newest result or `shell <index>` to choose another retained target. When the target terminal is closed, AutoHack resumes and replaces the retained target-computer, target-router when available, execution-server, and execution-router logs. Target-computer and owned execution-route cleanup are mandatory; unavailable target-router cleanup is reported honestly as best effort.

Use `interesting` to inventory non-stock files on the newest retained target, or `interesting <index>` for a selected session. It is designed for finding player tools, GreyScript source, chat/mail artifacts, pictures, PDFs, logs, documents, and unusual data without dumping the whole operating-system tree. The command prints paths and metadata only; it does not read contents or download anything.

## Commands

- `autohack <ip> [port] [lan-ip]` — attack one target, then remain at the AutoHack console.
- `<ip> [port] [lan-ip]` — attack another target from the persistent `autohack>` console.
- `target <ip> [port] [lan-ip]` — explicit console form of the same command.
- `nmap <ip|host> [--quick]` — run the embedded read-only Synthwave Deep Recon engine.
- `sessions` — list up to 12 retained verified access sessions.
- `where` / `whoami` — show execution origin and selected target.
- `shell [index]` — open the newest or selected retained session; terminal `exit` returns to AutoHack and runs finalization.
- `interesting [index]` — list visible non-stock files on the newest or selected session, then finalize logs and return to AutoHack.
- `autoshell [on|off]` — inspect or change automatic terminal entry; the default is off.
- `poison [status|list|on|off]` — inspect or control exact-name weak-library promotion.
- `nuke [index]` — run the separately confirmed Blackout payload against one retained root target.
- `harden home|server` — run separately confirmed local fortification.
- `forget [index|all]` — release retained shell objects from the current AutoHack run.
- `status` — show storage and shared VDB readiness.
- `help` — show the concise command guide.
- `quit` — leave AutoHack and return to the original terminal.

## Auto Family role

AutoRoute supplies the trusted owned chain and temporary proxy path. AutoRecon fills missing exact-version exploit knowledge. AutoNet recruits reusable SSH nodes. AutoDeploy will stage and remove temporary payloads. AutoHack consumes those shared capabilities to obtain one usable target session, then returns control to the route and cleanup lifecycle.

## Auto Family interface

`3.0.0` keeps AutoHack's accepted circuit, full help, left-to-right origin/target prompt, and detailed console. The user-facing console now requires a masked activation PIN. Attack attempts and results use the exact AutoAcademic grammar, while AHLOG records are split into semantic two-field branches: hosts, ports, libraries, and technical objects are cyan; identities and authority are pink; successful state is green; failures are red; cleanup and operator attention are orange; vulnerability actions remain purple; AHLOG badges are dim violet.

Both public sources intentionally ship with `PIN = ""`; configure the compact compile target before use or AutoHack remains locked. AutoHack's internally copied `--router-clean-helper` is the one deliberate PIN exception because an interactive prompt inside that unattended helper would break target-router cleanup.

## Runtime contract

- App state: `/root/autoscripts/autohack`
- Diagnostics: `/root/autoscripts/autohack/logs/latest.txt`
- Shared vulnerability database: `/root/vulndb`
- Optional matching weak libraries: `/root/PoisonLibs`
- Required local libraries: `/lib/metaxploit.so` and `/lib/crypto.so`

Target-computer and owned execution-route cleanup remain mandatory. Target-router cleanup remains honestly best effort when the target library yields no cleanup-capable object. Successful access is retained without unexpectedly replacing the AutoHack console unless AutoShell is enabled.

## Package status

The personal compact build is 154,266 characters, leaving 5,734 beneath CodeEditor's 160,000-character limit. The public compact build is 154,251 characters. All readable and compact `3.0.0` artifacts pass the local direct-source parser and compatibility audit with zero findings. Ordinary in-game use is the acceptance authority; there is no staged testing sequence.

The complete `3.0.0` presentation and ordinary attack lifecycle are field-observed and owner-accepted. The accepted run retained guest and root shells plus file and computer objects, handled numeric returns and rejected endpoints, recovered root access, preserved the native lavender attack narration, emitted the canonical semantic attack and AHLOG branches, completed target and execution cleanup, reported unavailable target-router cleanup honestly, and returned to the ready AutoHack console. Under `Trust Me`, this release is frozen until an encountered issue or an explicitly approved future capability requires another version.

Transfer `get/put`, shared-PC/router password escalation, Nmap reduction, and other serious capability work are intentionally deferred to a future update. AutoHack will not sacrifice its existing personality, skill, or usefulness to force in a conditional method.
