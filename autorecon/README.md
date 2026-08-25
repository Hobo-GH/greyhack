# AutoRecon 2.0.0

AutoRecon grows the shared ACVDB3 vulnerability database. It scans random or exact public targets, reuses complete exact-version coverage, fills missing coverage, harvests new exploit entries, and records what remains unknown. Its exact-library locator performs a focused metadata sweep and ignores unrelated services; a field search located `kernel_router.so 4.0.6` after 43 attempts in 3.926728 seconds.

## Install

Compile [`autorecon-2.0.0.src`](autorecon-2.0.0.src) as `/bin/autorecon`. The execution machine requires `/lib/metaxploit.so` and `/lib/crypto.so`.

## Commands

```text
hunt [count]                         scan random public targets
hunt focus <lib> [version] [count]   scan only one library family
hunt focus missing [count]           discover uncatalogued exact versions
target <ip> [port]                   scan one exact target
focus missing <lib> [version]        skip complete exact versions
focus <lib> [version]                fill one library and its gaps
focus all                            clear the library filter
rescan <lib> [version]               force fresh scans
huntlib <lib> [version] [count]      temporary missing-version hunt
coverage <lib> [version]             report complete and partial versions
find <lib> <version> [max-attempts]  locate that exact library in the wild
export                               write a compact coverage seed
import                               merge synchronized shards into ACVDB3
outbox                               show unsynchronized research
fresh                                reset focus and runtime counters only
status                               show database and focus state
quit                                 save, clean, and exit
```

## Runtime data

```text
/root/autoscripts/autorecon/logs/latest.txt
/root/autoscripts/autorecon/tasks/focus.txt
/root/autoscripts/autorecon/findings/locations.txt
/root/autoscripts/autorecon/outbox/
/root/autoscripts/autorecon/inbox/
/root/vulndb/index.txt
/root/vulndb/<library>/V<major>/shard-NNNN.txt
```

An endpoint copy can write research into its outbox; an authoritative copy imports synchronized shards into the shared database. Runtime databases and route credentials should never be published.

## Release notes

### 2.0.0

- Promoted AutoRecon after field confirmation of focused family hunting and the exact-library locator.
- Added broad missing-version discovery, family/version focus, complete-version skipping, forced rescans, coverage reports, and synchronized inbox/outbox research.
- Organized ACVDB3 by library, major version, and bounded shards for reuse across the Auto Family.
- Added the Rowan Circuit interface and exact metadata-only locator that ignores unrelated services.

## Runtime boundary

The library-family focus and exact-library locator are field-confirmed. Random-world availability, cleanup authority, and exposed library coverage vary by target; AutoRecon reports residual risk when it cannot retain the objects needed to clean a service.
