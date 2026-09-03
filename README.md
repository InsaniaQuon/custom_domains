# custom_domains

Personal repository with domain and subnet lists for granular traffic routing.
The lists are used together with sing-box based clients.

---

## sing-box version

`.srs` files are compiled with **sing-box 1.13.18**.

---

## Repository structure

```
custom_domains/
├── txt/                     # Source lists
├── json/                    # Auto-generated: sing-box source rule-set
├── lst/                     # Auto-generated: plain text list
└── srs/                     # Auto-generated: compiled binary rule-set
```

> Files in `json/`, `lst/` and `srs/` are generated automatically from the sources in `txt/`.

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
