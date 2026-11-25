# Sony-A7R6-research

Public research into Sony A7R VI (ILCE-7RM6) firmware and A7R V (ILCE-7RM5) feature ports, with the FX3 and A1 II as additional reference platforms. This repository records reproducible methods and observed results.

## Current status

As of 2026-11-25, Sony lists **1.02** as the latest A7R VI body firmware. The official Japanese download matches the local research copy byte for byte. [Sony Japan release notes](https://support.sony.jp/electronics/support/e-mount-body-ilce-7-series/ilce-7rm6/software/00413256)

| Target | Result | Evidence |
| --- | --- | --- |
| A7R VI 1.02 | UFU container and CRC verified. FDAT decryption stopped with `No decrypter found`. | [Release and offline analysis](docs/research/2026-11-25-r6-firmware-1.02.md) |
| A7R VI English menu | Public unlock remains unverified. PMCA-RE Reloaded 1.15.1 still reports Senser v2 as unsupported. | [Tool and language evidence](docs/research/2026-11-25-r6-firmware-1.02.md#service-access-and-menu-language) |
| A7R V 4.00 | Decryption with `CXD90057_k8` and file extraction succeeded. Internal model ID `0x11030080` and version `4.00` were verified. | [Offline validation](docs/research/2026-11-05-fwtool-a7iv.md) |
| Sony LUT Camera | Direct installation on A7R V or A7R VI is unverified. The project reports A6300 validation. | [LUT applicability](docs/research/2026-11-05-sony-lut-camera.md) |

## Research records

- [A7R VI 1.02 release and static analysis](docs/research/2026-11-25-r6-firmware-1.02.md)
- [R6 firmware access and English-menu status](docs/research/2026-11-16-r6-access-and-language-status.md)
- [FX3-related components found in R5 firmware](docs/research/2026-11-16-r5-fx3-static-audit.md)
- [A7R V feature-port candidates](docs/research/2026-11-05-a7rv-feature-port-candidates.md)
- [fwtool a7iv validation](docs/research/2026-11-05-fwtool-a7iv.md)
- [Sony LUT Camera applicability](docs/research/2026-11-05-sony-lut-camera.md)
- [External sources](docs/sources.md)
- [Firmware identification metadata](data/firmware-manifest.json)
- [Repository instructions](AGENTS.md)

## Local analysis

Original firmware and extracted files are excluded from this repository. Identify inputs by their recorded filenames, sizes, and SHA-256 hashes. Use the recorded tool commits and generate outputs in a separate directory.

```sh
git clone https://github.com/hletrd/Sony-A7R6-research.git
cd Sony-A7R6-research
```

## Official references

- [Sony A7R V 4.00 release information](https://www.sony.com/electronics/support/e-mount-body-ilce-7-series/ilce-7rm5/software/00292267)
- [Sony A7R VI 1.02 release information](https://www.sony.com/electronics/support/e-mount-body-ilce-7-series/ilce-7rm6/software/00413269)
