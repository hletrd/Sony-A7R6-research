# Sony-A7R6-research

Public research into Sony A7R VI (ILCE-7RM6) firmware and A7R V (ILCE-7RM5) feature ports, with the FX3 and A1 II as additional reference platforms. This repository records reproducible methods and observed results.

## Current status

On 2026-11-05, the `a7iv` branch of `DavidBuchanan314/fwtool.py` was tested against two firmware files.

| Target | Result | Evidence |
| --- | --- | --- |
| A7R V 4.00 | Decryption with `CXD90057_k8` and file extraction succeeded | Internal model ID `0x11030080` and version `4.00` verified |
| File inferred to be A7R VI 1.02 | Extraction failed with `No decrypter found` | Matches the official release size; internal model and version remain unverified |
| Sony LUT Camera | Direct installation on A7R V or A7R VI is unverified | An older Android/PMCA application with reported A6300 validation |

The two firmware filenames were initially swapped and have been corrected. The A7R V identity was verified from internal metadata; the A7R VI classification relies on the official file size. No comparison against an official firmware hash was performed. Extraction does not establish that modified firmware can be installed.

## Research records

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
