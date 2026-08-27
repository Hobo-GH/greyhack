# AutoNet

AutoNet is the SSH recruiter for the Auto script family. Run it from the final owned server opened by AutoRoute. It searches random public routers for SSH services, uses the shared vulnerability database, proves that the recovered root password works through a fresh SSH login, requires target-computer and owned execution-route cleanup, and then saves the machine as a reusable proxy node. Target-router cleanup is attempted and recorded but is no longer allowed to discard an otherwise verified node when the owned execution-route chain break is clean.

AutoNet does not touch AutoRoute's trusted `owned-route.txt`. Its node database is kept separately at:

`/root/autoscripts/autonet/nodes`

## Commands

```text
autonet
autonet hunt [verified-node goal] [random-candidate budget]
autonet nodes
autonet remove [index]
autonet deny <public IP>
autonet help
```

Examples:

```text
autonet hunt 1 250
autonet hunt 5 1000
autonet nodes
autonet remove 3
```

`autonet nodes` never displays passwords. `autonet remove` requires an exact confirmation, removes every matching saved record during the shard rebuild, and adds the public IP to the denylist so it cannot be rediscovered.

## Installation and first run

1. Configure `PIN`, then compile `autonet-1.1.1.src` as `/bin/autonet` on AutoRoute's final owned server.
2. Confirm that `/lib/metaxploit.so` and `/lib/crypto.so` exist on that server.
3. Keep AutoRoute resident on home so the trusted owned route remains available for emergency cleanup.
4. Start with `autonet hunt 1 250`.
5. Inspect `autonet nodes` and `/root/autoscripts/autonet/logs/latest.txt` after the run.

The development build scans unknown SSH libraries and adds what it learns to the shared ACVDB3 database under `/root/vulndb`. Known exact library versions are reused on later runs by AutoNet, AutoCredential, AutoAcademic, and other compatible Auto-family tools.

## Important limits

- A root shell is not enough. AutoNet reconnects with a recovered root password before considering the node reusable.
- Target-computer cleanup and execution computer/router cleanup are mandatory. Target-router cleanup is best-effort; its actual `yes` or `no` result is stored with the admitted node.
- Failed exploitation can leave evidence on a candidate that AutoNet never controlled. The script reports that risk and cleans the execution server and its router before continuing.
- Node credentials are stored in plaintext inside the game because AutoRoute Stage 2 needs unattended SSH reuse. Keep the AutoNet folder root-owned and do not publish its runtime shards.

## Current family interface

AutoNet `1.1.1` preserves the field-proven 1.0.0 direct in-game engine and gives it the complete Auto Family operating language. Its owner-refined network-mesh Rowan circuit is unique to AutoNet and owner-accepted. The startup surface includes a labeled masked PIN gate and a front-page guide. Hunt limits, node selection, and destructive removal confirmation use contextual origin-and-destination signatures. Every overflow uses the exact AutoAcademic attack/result grammar, native Grey Hack narration remains untouched, and ACLOG records split network, authority, cleanup, vulnerability, warning, and result values by semantic color rather than painting entire records one color.

Node listings remain password-free and now expose authority, verification, and actual computer/router cleanup state as separate readable values. Recruitment results are grouped into verified nodes, candidate count, SSH services, exploit surfaces, skips, stored total, and latest diagnostic path.

The 1.1.1 source and compact build are 65,457 characters, leaving 94,543 beneath CodeEditor's 160,000-character limit. Personal and GitHub-ready lanes are packaged with blank PIN configuration and share SHA-256 `198013EF5A7D3B20D6191B3CF505F71757CCA9976953DE1F1B3DEB95D46E6E1D`. Static parsing accepts both; the 19 direct-layout warnings are inherited unchanged from the field-proven Greybel-generated 1.0.0 build.

The ordinary 2026-08-26 run displayed 23 candidates, verified 5 of 5 requested nodes, retained 30 stored nodes in total, and added `libssh.so` knowledge to the shared ACVDB shards. The owner accepted the rendered circuit, operating output, and workflow. Version 1.1.1 packages that exact accepted circuit as a plain visual patch successor without changing the recruitment engine.

## Preserved stable engine

AutoNet `1.0.0` is the field-verified stable release. Public runs proved SSH discovery, exact-version ACVDB3 reuse, reusable root reconnection, target-computer cleanup, execution computer/router cleanup, best-effort target-router reporting, node admission, shard/index persistence, cold reload, masked node listing, confirmed removal, complete shard rebuild, automatic denylisting of a removed node, and manual denylist insertion.

The stable source differs from the field-proven `0.1.1-dev` engine only in its displayed version label. The admitted field node correctly recorded unresolved target-router cleanup while the mandatory execution-route chain break remained clean.

The previously discussed 100-node ceiling is deliberately not bundled into 1.1.1. Stable `1.0.0` and current `1.1.1` both accept `hunt 10`, `hunt 25`, and `hunt 50`; `hunt 100` remains a separate future capability with its own semantic version.
