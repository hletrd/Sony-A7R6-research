# FX3-related components in A7R V firmware

## Scope and inputs

On 2026-11-16, five components from the existing A7R V 4.00 extraction were inspected for shutter angle, Cine EI, user LUTs, anamorphic de-squeeze, and DCI 4K. This follows the [feature comparison](2026-11-05-a7rv-feature-port-candidates.md).

The original firmware SHA-256 is `51e1176a255a9a4b4782dfbcfa6c5f332b71173bdfe9ed2bcf4fca6bcbc6c2e2`. The extraction provenance is documented in the [fwtool record](2026-11-05-fwtool-a7iv.md). This audit inspected the existing extracted files rather than repeating extraction.

| Component | Size in bytes | Role in this inspection |
| --- | --- | --- |
| `im.elf` | 40,920 | Application launcher |
| `appFw.so` | 97,368,304 | Main application framework and feature-related code references |
| `libSysDef.so` | 6,041,280 | Additional application-side comparison |
| `cpapp-b.bin` | 17,617,008 | Control-processor diagnostic strings |
| `av-cam.bin` | 12,956,536 | Imaging-side diagnostic strings |

The application files are stripped AArch64 ELF binaries. No matching feature names were found in the limited ASCII scan of `im.elf` or `libSysDef.so`; this is not proof that they have no relevant behavior. Component hashes and reviewed references are in the [audit metadata](../../data/2026-11-16-r5-fx3-static-audit.json).

## Method

ASCII strings were searched for feature-specific identifiers and diagnostic names. Selected string addresses in `appFw.so` were then traced from its executable `.text` section using AArch64 ADRP/ADD address construction. Candidate decoding was checked with Capstone, and representative surrounding instructions were inspected. ELF relocation entries were also checked for selected parameter and backup-catalog labels.

The environment was CPython 3.14.2, pyelftools 0.33, and Capstone 5.0.9. The two analysis dependencies were checked against PyPI before installation. The trace found 15 code references to the selected strings and three selected catalog relocation references. These counts describe the selected targets and conservative search, not all feature-related code.

## Findings

| Feature | Direct static observation | Representative code-reference VA |
| --- | --- | --- |
| Shutter angle | Executable code references the diagnostic name for `extern_BKID_APP_EXTERN_SHUTTER_ANGLE_STEP`; the parameter catalog includes `PRM_setting_shutter_angle`, angle values, and a shutter-angle backup label. | `0x2e1c9f4` |
| Cine EI | Executable code references an exposure-index enable handler and an external Base ISO handler. `cpapp-b.bin` contains EI gain and Base ISO processing diagnostics. | `0x2429d78` |
| User LUTs | Executable code references 3D-LUT reading, LUT-folder mounting, and a LUT-send routine. `cpapp-b.bin` contains a `SET_USER_LUT_BINARY_DATA` diagnostic. | `0x30a244c` |
| Anamorphic de-squeeze | Executable code references the diagnostic name for `sequence_set_anamo_desqueeze_scale::run()`. The application catalog includes 1.3x and 2.0x settings. | `0x3475ec4` |
| DCI 4K / true 24.00p | Executable code references the diagnostic name for a DCI/24.00p reboot handler. Imaging-side strings include DCI recording-mode identifiers. | `0x2759a24` |

The shutter-angle parameter and backup labels also have ELF relocation references. These are catalog entries; the recorded ELF addresses are not the numeric property IDs accepted by a service-shell command.

The surrounding code confirms that the selected names are referenced by instructions rather than merely existing as isolated strings. Several references are diagnostic or assertion paths. That distinction matters: a reference establishes compiled feature-related code, not that the corresponding feature is reachable or supported on the R5.

## Interpretation and limits

The R5 firmware contains shared framework components related to all five investigated FX3 feature groups. Availability checks, model configuration, parameter routing, and lower-level compatibility are therefore useful next targets before assuming the feature must be transplanted from another camera.

This is an inference about the next research direction. The audit did not establish a working unlock, identify a validated setting to enable, execute the routines, or test a modified camera. It did not compare an extracted FX3 firmware image. Generic control-firmware messages also mention hardware capabilities that the R5 does not provide, so message presence alone is not a capability test.

For user LUTs, the file-loading and lower-level transfer diagnostics are stronger leads than a menu label alone. Whether the R5 can use them for preview, recorded video, or still-image JPEG processing remains unverified. Cine EI also requires R5-specific exposure and gain validation; its presence does not establish FX3 sensor performance.

## Reproducing representative references

Use the exact `appFw.so` identified in the metadata. This example checks the component hash and disassembles the five representative reference locations. It reads a local file only.

```sh
uv venv --python 3.14 .venv
uv pip install --python .venv/bin/python pyelftools==0.33 capstone==5.0.9
R5_APPFW="/path/to/appFw.so" .venv/bin/python - <<'PY'
import hashlib
import io
import os
from pathlib import Path
from capstone import Cs, CS_ARCH_ARM64, CS_MODE_LITTLE_ENDIAN
from elftools.elf.elffile import ELFFile

data = Path(os.environ["R5_APPFW"]).read_bytes()
assert hashlib.sha256(data).hexdigest() == "41bd8f4cda1f44c7038912837737e1ce6a650065f2108061ada30e5c7f9ce7c7"
elf = ELFFile(io.BytesIO(data))
text = elf.get_section_by_name(".text")
code = text.data()
decoder = Cs(CS_ARCH_ARM64, CS_MODE_LITTLE_ENDIAN)
for address in [0x2e1c9f4, 0x2429d78, 0x30a244c, 0x3475ec4, 0x2759a24]:
    offset = address - text["sh_addr"]
    print(hex(address))
    for insn in decoder.disasm(code[offset:offset + 32], address):
        print(hex(insn.address), insn.mnemonic, insn.op_str)
PY
```

## Next checks

1. Trace feature availability and model-selection conditions for shutter angle and de-squeeze.
2. Identify the actual R5 backup-property mappings independently of catalog names.
3. Follow the LUT reader and transfer paths to their format checks and imaging interfaces.
4. Compare known FX3 firmware components before proposing a port or activation patch.
