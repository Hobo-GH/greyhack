# AutoDeploy

AutoDeploy is the Auto Family payload controller for Grey Hack Public v0.9.6773. It reads the final proxy written by AutoRoute, copies an editable set of tools and libraries to that proxy, and records every new remote path in a local deployment ledger.

The default payload is intentionally useful out of the box but not mandatory. Edit `/root/autoscripts/autodeploy/tasks/payload.txt` to add, remove, or redirect files. Missing local files are reported and skipped. Existing remote files are preserved so retract never deletes something AutoDeploy did not create.

The current default manifest carries the active Auto Family field kit: AutoHack, AutoRecon, AutoTrash, AutoSentry, AutoAcademic, AutoCredential, AutoCorrupt, MetaXploit, and Crypto. Fresh manifests use the official `/bin/autocredential` name. On activation, `1.1.2` surgically replaces the exact historical `F|/bin/autocred|/bin` entry in an existing manifest. Every other custom payload line, comment, and ordering choice is preserved.

## Install and activation

Set a private `PIN` in `autodeploy-1.1.2.src`, then compile it as `/bin/autodeploy`. AutoDeploy identifies the masked startup request as `ENTER PIN` before opening its console. The public source intentionally has `PIN = ""`; never publish a configured personal copy.

## Workflow

1. Build the owned route and run `autoroute extend`.
2. Start AutoDeploy on the final owned server.
3. Run `payload` to review the manifest.
4. Run `deploy` to populate the final proxy.
5. Use `status` whenever you want to verify the tracked payload.
6. Run `retract` before collapsing the proxy route.
7. Run `autoroute collapse` for route-wide cleanup and return.

`retract` removes the exact files in AutoDeploy's ledger, removes the remote `/root/autoscripts` tree created by Auto Family tools, empties every discovered account Trash, and replaces the target computer log as its final remote filesystem action. It removes the local ledger only after all required surfaces succeed, so a partial recall remains visible and retryable. AutoRoute remains responsible for cleanup across the entire owned and proxy chain.

## Commands

- `deploy` - deploy configured files to the active target.
- `status` - inspect the target, ledger, and remote file presence.
- `retract` - remove the tracked payload and perform final target cleanup.
- `clean` / `clog` / `logs` - replace the target computer log.
- `payload` - show manifest entries and local readiness.
- `setup` - save a manual SSH fallback when no AutoRoute handoff exists.
- `help` - show command help.
- `quit` - leave AutoDeploy.

## Runtime files

- AutoRoute handoff: `/root/autoscripts/network/active-proxy-route.txt`
- Editable payload: `/root/autoscripts/autodeploy/tasks/payload.txt`
- Deployment ledger: `/root/autoscripts/autodeploy/tasks/active-deployment.txt`
- Diagnostics: `/root/autoscripts/autodeploy/logs/latest.txt`

## Version 1.1.2

`1.1.0` is the preserved plain-version family-interface successor to `1.0.0-dev5`. It keeps the field-observed handoff parser, final-proxy selection, manual fallback, payload parser, missing-file tolerance, existing-file preservation, exact deployment ledger, cleanup source, Trash purge, retraction engine, commands, and unique Rowan circuit.

The new interface adds the labeled masked PIN gate, a front-page explanation and help panel, a contextual `PACKAGE`/`HANDOFF` input signature, the exact Auto Family palette, dim `ADLOG` sequence badges, and short event-plus-branch records for connection, package, cleanup, ledger, status, and recall state. Deployment-specific records are a narrow AutoDeploy exception because package ownership and exact retraction do not have an AutoAcademic hacking-event equivalent.

The source also refuses to claim full success when the deployment ledger cannot be saved. Retraction retains that ledger unless tracked-file deletion, family-data removal, Trash cleanup, final target-log cleanup, and ledger removal all succeed. Missing local payload entries remain an expected orange skip rather than a failed deployment.

A real `1.1.0` AutoRoute-handoff deployment connected successfully, deployed eight of nine manifest entries, skipped the missing older `/bin/autocred` entry as designed, saved the ledger, completed endpoint cleanup, and returned to the tracked prompt. That run exposed one presentation-only fault: indexed package headings that relied on global constants as optional-parameter defaults printed literal `<color=_17>` and `<color=_18>` tags.

`1.1.1` changes only `show_event`, `show_indexed_event`, and `show_branch`. Their optional color defaults are now empty literals, and the functions resolve the intended family colors internally. All operational functions are unchanged from `1.1.0`; the repair prevents the literal color placeholders observed in the earlier terminal output.

`1.1.2` keeps that repair and adds only the requested saved-manifest rename migration. After the correct PIN is entered, AutoDeploy replaces an exact legacy `/bin/autocred` package line with `/bin/autocredential`; if both names already exist, it removes only the obsolete duplicate. It records and displays the upgrade once, then proceeds normally. The release source is static-parse accepted with zero compatibility errors; the preserved deployment engine has already completed a real handoff deployment while tolerating a missing package entry.
