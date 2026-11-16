# custom_domains

Personal repository with domain and subnet lists for granular traffic routing.
The lists are provided in multiple text and binary formats.

---

## Core versions

- `.srs` files are compiled with **sing-box 1.14.4**.
- `.mrs` files are compiled with **mihomo 1.19.33**.

---

## Repository structure

```
custom_domains/
├── txt/                     # Source lists
├── json/                    # Auto-generated: sing-box source rule-set
├── lst/                     # Auto-generated: plain text list
├── list/                    # Auto-generated: text rule-set
├── srs/                     # Auto-generated: compiled binary rule-set
├── mrs/                     # Auto-generated: mihomo binary rule-set
├── dat/                     # Auto-generated: Xray geo file
├── hagezi/                  # Auto-generated: HaGeZi blocklists
└── runetfreedom_export/      # Auto-generated: selected RunetFreedom lists
    └── category-ai-!cn/
        ├── mrs/             # Domain rules
        └── list/            # Additional classical rules
```

> Files in `json/`, `lst/`, `list/`, `srs/`, `mrs/` and `dat/` are generated automatically from the sources in `txt/`.

---

## File formats

### `txt/` — sources

Plain text file, one domain per line (domains only, or subnets only).
Lines starting with `#` and empty lines are ignored during the build.

```
# Comment
youtube.com
googlevideo.com
```

---

### `lst/` — text list

Same as `txt/`, but without comments — only domains or subnets.

```
youtube.com
googlevideo.com
```

---

### `list/` — text rule-set

One rule per line, without an embedded policy. Domains use `DOMAIN-SUFFIX`, IPv4 networks use `IP-CIDR`.

```
DOMAIN-SUFFIX,youtube.com
IP-CIDR,74.125.250.0/24
```

---

### `json/` — sing-box source rule-set

JSON file in the sing-box Rule Set Source Format.
Format version: **3** (supported by sing-box 1.11.0+).

For domains
```json
{
  "version": 3,
  "rules": [
    {
      "domain_suffix": [
        "youtube.com",
        "googlevideo.com"
      ]
    }
  ]
}
```

For subnets
```json
{
  "version": 3,
  "rules": [
    {
      "ip_cidr": [
        "11.222.0.0/11"
      ]
    }
  ]
}
```

---

### `srs/` — sing-box binary rule-set

Compiled binary file.
Binary format version: **2** (supported by sing-box 1.10.0+).

---

### `mrs/` — mihomo binary rule-set

Compiled binary file. Supports `domain` and `ipcidr` behaviors.

Domain lists (`custom_domains`, `ip-checker`) use `domain` behavior with `+.domain` inputs to match the apex domain and subdomains. `custom_subnets` uses `ipcidr` behavior.

---

### `dat/` — Xray geo file

Binary protobuf geo file: `GeoSiteList` for domains or `GeoIPList` for subnets.
One category per source file, tag = uppercase source filename stem.
Domain type: `RootDomain = 2`.

| File | Type | Category tag |
| --- | --- | --- |
| `custom_domains.dat` | GeoSite | `CUSTOM_DOMAINS` |
| `custom_subnets.dat` | GeoIP | `CUSTOM_SUBNETS` |
| `ip-checker.dat` | GeoSite | `IP-CHECKER` |

Use `ext:custom_domains.dat:custom_domains` in a routing rule's `domain` array (`routing.rules[].domain`).
Xray uppercases the category name when loading it, so lowercase references work. Filename case is handled separately by the filesystem; use the exact filename shown above.

---

## HaGeZi blocklists

Generated directly from the original [HaGeZi DNS Blocklists](https://github.com/hagezi/dns-blocklists)
Adblock sources as `.list`, `.dat` and `.mrs` files.

| Rule set | Original HaGeZi source | LIST download | DAT download | MRS download |
| --- | --- | --- | --- | --- |
| `hagezi-light` | [adblock/light.txt](https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/light.txt) | [hagezi-light.list](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-light.list) | [hagezi-light.dat](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-light.dat) | [hagezi-light.mrs](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/mrs/hagezi-light.mrs) |
| `hagezi-normal` | [adblock/multi.txt](https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/multi.txt) | [hagezi-normal.list](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-normal.list) | [hagezi-normal.dat](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-normal.dat) | [hagezi-normal.mrs](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/mrs/hagezi-normal.mrs) |
| `hagezi-pro` | [adblock/pro.txt](https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.txt) | [hagezi-pro.list](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-pro.list) | [hagezi-pro.dat](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-pro.dat) | [hagezi-pro.mrs](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/mrs/hagezi-pro.mrs) |
| `hagezi-pro-plus` | [adblock/pro.plus.txt](https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.plus.txt) | [hagezi-pro-plus.list](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-pro-plus.list) | [hagezi-pro-plus.dat](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-pro-plus.dat) | [hagezi-pro-plus.mrs](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/mrs/hagezi-pro-plus.mrs) |
| `hagezi-ultimate` | [adblock/ultimate.txt](https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/ultimate.txt) | [hagezi-ultimate.list](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-ultimate.list) | [hagezi-ultimate.dat](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-ultimate.dat) | [hagezi-ultimate.mrs](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/mrs/hagezi-ultimate.mrs) |

---

## RunetFreedom exports

`runetfreedom_export/` contains selected lists from [RunetFreedom](https://github.com/runetfreedom/russia-v2ray-rules-dat), converted into the required formats.

| Rule set | MRS download | Additional rules |
| --- | --- | --- |
| AI services (`category-ai-!cn`) | [category-ai-!cn.mrs](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/runetfreedom_export/category-ai-!cn/mrs/category-ai-!cn.mrs) | [category-ai-!cn-extra.list](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/runetfreedom_export/category-ai-!cn/list/category-ai-!cn-extra.list) |

Use both files together: MRS with `behavior: domain`, and the additional text list with `behavior: classical` for rules that MRS cannot represent.
