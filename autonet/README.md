# AutoNet 1.0.0

AutoNet is the Auto Family's SSH recruiter. Run it from the final owned server opened by AutoRoute. It searches random public routers for SSH services, reuses exact-version ACVDB3 knowledge, recovers root credentials, proves those credentials with a fresh SSH login, performs required cleanup, and stores verified machines as reusable proxy nodes.

AutoNet never edits AutoRoute's trusted owned-route file. Its node database is separate.

## Install

Compile [`autonet-1.0.0.src`](autonet-1.0.0.src) as `/bin/autonet` on the final owned server. That server must provide `/lib/metaxploit.so` and `/lib/crypto.so`.

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

`nodes` masks passwords. `remove` requires exact confirmation, rebuilds every matching shard out of the database, and denies the removed public IP so it cannot be rediscovered.

## Runtime data

```text
/root/autoscripts/autonet/nodes/
/root/autoscripts/autonet/logs/latest.txt
/root/vulndb/
```

Node credentials are stored in plaintext inside root-owned in-game files because unattended SSH reuse requires them. Never publish runtime shards.

## Release notes

### 1.0.0

- Introduced bounded random SSH hunting with exact-version ACVDB3 reuse.
- Requires a fresh root SSH proof before admitting a machine as a proxy node.
- Added organized node shards, masked listings, exact-confirmation removal, and a deny list that prevents rediscovery.
- Separated AutoNet's untrusted proxy inventory from AutoRoute's owned-route store.

## Admission and cleanup rules

- A returned root shell is insufficient; AutoNet requires a fresh root SSH reconnect.
- Target-computer cleanup and execution computer/router cleanup are mandatory.
- Target-router cleanup is attempted and recorded but remains best effort. A node may be admitted when the execution-route chain break is clean even if its physical router could not be cleaned.
- Failed candidates can retain evidence on machines AutoNet never controlled. The diagnostic records that residual risk.
