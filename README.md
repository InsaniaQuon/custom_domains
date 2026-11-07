# custom_domains

Personal repository with domain and subnet lists for granular traffic routing.
The lists are used together with sing-box based clients.

---

## sing-box version

`.srs` files are compiled with **sing-box 1.14.4**.

---

## Repository structure

```
custom_domains/
├── txt/                     # Source lists
├── json/                    # Auto-generated: sing-box source rule-set
├── lst/                     # Auto-generated: plain text list
├── srs/                     # Auto-generated: compiled binary rule-set
├── dat/                     # Auto-generated: Xray geo file
└── hagezi/                  # Auto-generated: HaGeZi blocklists
```

> Files in `json/`, `lst/`, `srs/` and `dat/` are generated automatically from the sources in `txt/`.

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

### `dat/` — Xray geo file

Binary protobuf geo file: `GeoSiteList` for domains or `GeoIPList` for subnets.
One category per source file, tag = file name stem.
Domain type: `RootDomain = 2`.

---

## HaGeZi blocklists

Generated directly from the original [HaGeZi DNS Blocklists](https://github.com/hagezi/dns-blocklists)
Adblock sources as `.list` and `.dat` files.

| Rule set | Original HaGeZi source | LIST download | DAT download |
| --- | --- | --- | --- |
| `hagezi-light` | [adblock/light.txt](https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/light.txt) | [hagezi-light.list](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-light.list) | [hagezi-light.dat](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-light.dat) |
| `hagezi-normal` | [adblock/multi.txt](https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/multi.txt) | [hagezi-normal.list](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-normal.list) | [hagezi-normal.dat](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-normal.dat) |
| `hagezi-pro` | [adblock/pro.txt](https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.txt) | [hagezi-pro.list](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-pro.list) | [hagezi-pro.dat](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-pro.dat) |
| `hagezi-pro-plus` | [adblock/pro.plus.txt](https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.plus.txt) | [hagezi-pro-plus.list](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-pro-plus.list) | [hagezi-pro-plus.dat](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-pro-plus.dat) |
| `hagezi-ultimate` | [adblock/ultimate.txt](https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/ultimate.txt) | [hagezi-ultimate.list](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/list/hagezi-ultimate.list) | [hagezi-ultimate.dat](https://raw.githubusercontent.com/InsaniaQuon/custom_domains/main/hagezi/dat/hagezi-ultimate.dat) |
