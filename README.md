# custom_domains

Personal repository with domain and subnet lists for granular traffic routing.
The lists are provided in multiple text and binary formats.

## Core versions

- `.srs` files are compiled with **sing-box 1.14.4**.
- `.mrs` files are compiled with **mihomo 1.19.33**.

## Repository structure

`{…}` expands to separate files or directories. All paths are relative to the
repository root. Descriptions are outside the path column.

```text
Repository tree                                         │ Purpose
────────────────────────────────────────────────────────┼───────────────────────────────
├── custom/                                             │ Personal lists
│   ├── custom_domains.{txt,lst,list,json,srs,mrs,dat}  │ Domains; editable TXT source
│   └── custom_subnets.{txt,lst,list,json,srs,mrs,dat}  │ Subnets; editable TXT source
│                                                       │
├── ip-checker/                                         │ Merged max-list domains
│   └── ip-checker.{txt,lst,list,json,srs,mrs,dat}      │ Generated TXT + six formats
│                                                       │
├── category-ai-!cn/                                    │ RunetFreedom AI category
│   ├── category-ai-!cn.mrs                             │ Exact and suffix rules
│   └── category-ai-!cn-extra.list                      │ Keyword/regex companion
│                                                       │
├── exclusion/                                          │ RU-direct domain union
│   ├── exclusion.{txt,json,srs,mrs,dat}                │ Typed TXT + client formats
│   ├── exclusion-extra.list                            │ Keyword/regex companion
│   └── sources.json                                    │ Revisions, hashes and counts
│                                                       │
├── telegram/                                           │ Telegram domain and IP unions
│   ├── telegram_domains.{json,srs,mrs,dat}             │ Domain rules
│   ├── telegram_domains-extra.list                     │ Keyword/regex companion
│   ├── telegram_ips.{json,srs,mrs,dat}                 │ IPv4 + IPv6 in every format
│   └── sources.json                                    │ Revisions, hashes and counts
│                                                       │
├── hagezi/                                             │ HaGeZi blocklists
│   └── {list,dat,mrs}/                                 │ Five lists per format
│                                                       │
├── {txt,lst,list,json,srs,mrs,dat}/                    │ DEPRECATED — 21 copies
├── runetfreedom_export/                                │ DEPRECATED — 2 AI copies
│   └── category-ai-!cn/{mrs,list}/                     │ Original AI paths
└── README.md                                           │ Build and consumer guide
```

## Personal lists: `custom/`

- `custom_domains.*` — personal domain lists; entries match the apex and subdomains.
- `custom_subnets.*` — personal IP and subnet lists.

Both lists are available in TXT, LST, LIST, JSON, SRS, MRS and DAT formats.

## IP Checker: `ip-checker/`

The daily build downloads `ip-check-formatted.txt` and `vpndetect.txt` from
the same latest release of [fatyzzz/max-list](https://github.com/fatyzzz/max-list).
It removes comments/empty lines, unions and sorts the entries, writes
`ip-checker.txt`, and generates the six companion formats.
The TXT file is generated, not a manually maintained source.

## AI: `category-ai-!cn/`

The complete `category-ai-!cn` category is selected from
[RunetFreedom GeoSite](https://raw.githubusercontent.com/runetfreedom/russia-v2ray-rules-dat/release/geosite.dat).
Exact domains stay exact; suffix rules include the apex and subdomains.
Keyword and regex rules are written to `category-ai-!cn-extra.list`.
Use the MRS and companion LIST together for complete category coverage.
GeoSite attributes are treated as metadata; no attribute filter is applied.

## RU-direct: `exclusion/`

The builder unions:

- itdog [`Russia/outside-raw.lst`](https://raw.githubusercontent.com/itdoginfo/allow-domains/main/Russia/outside-raw.lst);
- the complete `ru-available-only-inside` category from RunetFreedom GeoSite.

Deduplication uses the match type and normalized value. Exact domains, suffixes,
keywords and regex retain their meaning. DNS names are lowercased, trailing dots
removed and Unicode names IDNA-encoded; regex and keywords are not lowercased.
The broad suffix rules `ru`, `su`, `xn--p1ai` are **not added** by this builder:
configure them separately in the consumer if desired.

`exclusion.txt` is a **typed inspection export**, not a bare domain list:

```text
full:exact.example
domain:example.org
keyword:example
regexp:^service[0-9]+\.example$
```

`full:` means exact match; `domain:` means apex and subdomains. The prefix ends
at the first colon; everything after it is the value.

## Telegram: `telegram/`

Domains and IPs are independent products, both derived from itdog and
RunetFreedom:

| Data | itdog source | RunetFreedom source |
|---|---|---|
| Domains | [`Services/telegram.lst`](https://raw.githubusercontent.com/itdoginfo/allow-domains/main/Services/telegram.lst) | Complete `telegram` GeoSite category |
| IPv4 | [`Subnets/IPv4/telegram.lst`](https://raw.githubusercontent.com/itdoginfo/allow-domains/main/Subnets/IPv4/telegram.lst) | [`text/telegram.txt`](https://raw.githubusercontent.com/runetfreedom/russia-blocked-geoip/release/text/telegram.txt) |
| IPv6 | [`Subnets/IPv6/telegram.lst`](https://raw.githubusercontent.com/itdoginfo/allow-domains/main/Subnets/IPv6/telegram.lst) | The same dual-stack Telegram IP text |

IP inputs are normalized, deduplicated and collapsed separately per address
family without widening coverage. **All `telegram_ips.*` files contain both
IPv4 and IPv6.** There is no separately maintained IPv4 export.

## Downloads and consumer formats

| Dataset | SRS | MRS | DAT |
|---|---|---|---|
| Personal domains | [SRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/custom/custom_domains.srs) | [MRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/custom/custom_domains.mrs) | [DAT](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/custom/custom_domains.dat) |
| Personal subnets | [SRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/custom/custom_subnets.srs) | [MRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/custom/custom_subnets.mrs) | [DAT](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/custom/custom_subnets.dat) |
| IP Checker | [SRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/ip-checker/ip-checker.srs) | [MRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/ip-checker/ip-checker.mrs) | [DAT](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/ip-checker/ip-checker.dat) |
| AI services | — | [MRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/category-ai-!cn/category-ai-!cn.mrs) | — |
| Exclusion | [SRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/exclusion/exclusion.srs) | [MRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/exclusion/exclusion.mrs) | [DAT](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/exclusion/exclusion.dat) |
| Telegram domains | [SRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/telegram/telegram_domains.srs) | [MRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/telegram/telegram_domains.mrs) | [DAT](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/telegram/telegram_domains.dat) |
| Telegram IPs | [SRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/telegram/telegram_ips.srs) | [MRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/telegram/telegram_ips.mrs) | [DAT](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/telegram/telegram_ips.dat) |

## File formats

### `.txt` — sources

Plain text file, one domain or subnet per line (domains only, or subnets only).
Lines starting with `#` and empty lines are ignored during the build.

### `.lst` — text list

Same as `.txt`, but without comments — only domains or subnets.

### `.list` — text rule-set

One rule per line, without an embedded policy. Suffix domain rules use
`DOMAIN-SUFFIX`, IPv4 networks use `IP-CIDR`, IPv6 networks use `IP-CIDR6`.

### `.json` — sing-box source rule-set

JSON file in the sing-box Rule Set Source Format.
Format version: **3**.

### `.srs` — sing-box binary rule-set

Compiled binary file.
Binary format version: **2**.

### `.mrs` — mihomo binary rule-set

Compiled binary file. Supports `domain` and `ipcidr` behaviors.

### `.dat` — Xray geo file

Binary protobuf geo file: `GeoSiteList` for domains or `GeoIPList` for subnets.
One category per file; tag = uppercase filename stem.

Install DAT files in the Xray asset directory before referencing them:

| File | Category | Routing field |
|---|---|---|
| `custom_domains.dat` | `CUSTOM_DOMAINS` | `domain` |
| `custom_subnets.dat` | `CUSTOM_SUBNETS` | `ip` |
| `ip-checker.dat` | `IP-CHECKER` | `domain` |
| `exclusion.dat` | `EXCLUSION` | `domain` |
| `telegram_domains.dat` | `TELEGRAM_DOMAINS` | `domain` |
| `telegram_ips.dat` | `TELEGRAM_IPS` | `ip` |

Example references: `ext:exclusion.dat:EXCLUSION` in `domain` and
`ext:telegram_ips.dat:TELEGRAM_IPS` in `ip`. Keep domain and IP criteria in
separate rules; combining them would require both to match. Policies, routing
priority and outbound selection belong to the consumer configuration.

## HaGeZi blocklists

Generated directly from the original [HaGeZi DNS Blocklists](https://github.com/hagezi/dns-blocklists)
Adblock sources.

| Stem | Upstream source | LIST | DAT | MRS |
|---|---|---|---|---|
| `hagezi-light` | `adblock/light.txt` | [LIST](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-light.list) | [DAT](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-light.dat) | [MRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/mrs/hagezi-light.mrs) |
| `hagezi-normal` | `adblock/multi.txt` | [LIST](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-normal.list) | [DAT](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-normal.dat) | [MRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/mrs/hagezi-normal.mrs) |
| `hagezi-pro` | `adblock/pro.txt` | [LIST](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-pro.list) | [DAT](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-pro.dat) | [MRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/mrs/hagezi-pro.mrs) |
| `hagezi-pro-plus` | `adblock/pro.plus.txt` | [LIST](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-pro-plus.list) | [DAT](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-pro-plus.dat) | [MRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/mrs/hagezi-pro-plus.mrs) |
| `hagezi-ultimate` | `adblock/ultimate.txt` | [LIST](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-ultimate.list) | [DAT](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-ultimate.dat) | [MRS](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/mrs/hagezi-ultimate.mrs) |

HaGeZi MRS uses `behavior: domain`; DAT tags are uppercase stems.
