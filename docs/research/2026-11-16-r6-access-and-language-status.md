# A7R VI access and English-menu status

## Scope

Initially checked on 2026-11-16 after a request to enable English on an A7R VI. On 2026-11-19, the user confirmed firmware 1.02 and that English is unavailable because of locale restrictions. The exact market/region code remains unconfirmed. No camera language change has been performed.

## Normal language selection

Sony documents the path as `MENU > Setup > Area/Date > Language > desired language`. If English is offered, select it there. This documents the normal setting; it does not establish that English can be selected on a region-restricted body. Source: [A7R VI Language](https://helpguide.sony.net/ilc/2620/v1/en/contents/0601_language.html).

## Public unlock evidence

| Source checked | Observation | Interpretation |
| --- | --- | --- |
| [Sony-PMCA-RE issue #722](https://github.com/ma1co/Sony-PMCA-RE/issues/722) | The Japan-version language request was closed on 2026-10-22. The public discussion contains a service-provider claim, with no published procedure or technical validation. | Closure does not establish a reproducible public R6 unlock. |
| [Sony-PMCA-RE issue #716](https://github.com/ma1co/Sony-PMCA-RE/issues/716) | The title includes A7R VI, but the concrete public PAL/NTSC instructions concern an A7 IV. | Do not transfer another model's settings recipe to the R6 without validation. |
| [fwtool PR #52](https://github.com/ma1co/fwtool.py/pull/52) | The head remains `3955d7890fc38daf942bb52827599bfe35de4a14`. The latest key-matrix comment, dated 2026-10-22, still lists the R6 key as unknown. | No new R6 decryptor was established in this change or its discussion. |
| [q19032/Sony-firmware-unpacker](https://github.com/q19032/Sony-firmware-unpacker) | Latest commit remains `e118ab0145275382d6114e047b8ce4df98020374`, dated 2026-09-12. | No new implementation change since the earlier local collection. |

The local input classified as R6 1.02 failed extraction with the checked fwtool implementation, as documented in the [extraction record](2026-11-05-fwtool-a7iv.md). Firmware decryption and service-mode authentication are separate questions; a failure in one does not prove that every route through the other is unavailable.

GitHub repository and issue searches for `ILCE-7RM6`, `A7RVI`, and `a7r6`, together with the sources above, did not establish a new reproducible R6 English unlock. This is a result of the sources checked, not proof that no private method exists.

Sony's [current firmware listing](https://support.sony.jp/electronics/support/e-mount-body-ilce-7-series/ilce-7rm6/downloads) still lists 1.02, released on 2026-10-21.

## Service authentication finding, 2026-11-19

The current PMCA RE Reloaded source was inspected at commit `3121bb856151ce33cb5ea266a5f503d478a86678`, dated 2026-11-18. Its authentication implementation explicitly returns `SenserV2Unsupported` when the first authentication reply has return value `9` and a payload beginning with `0x02`. The implemented legacy paths accept SHA-1 or SHA-256 challenge selections instead. This is a direct source-code observation, not a captured response from the user's camera. Source: [SenserAuthDevice::authenticate](https://github.com/masterflai/pmca-re-reloaded/blob/3121bb856151ce33cb5ea266a5f503d478a86678/crates/pmca-usb/src/senser.rs#L398-L420).

The maintainer's device documentation identifies the R6 among bodies with an RSA-signed Senser v2 handshake and marks its community support as disputed. That protocol attribution is an external maintainer report; it was not independently established through a device trace or R6 firmware analysis here. Source: [device documentation](https://github.com/masterflai/pmca-re-reloaded/blob/3121bb856151ce33cb5ea266a5f503d478a86678/crates/pmca-app/src/devices.rs#L271-L279).

The legacy language-mask implementation does not bypass this authentication requirement. An English-language flag in older models is therefore insufficient evidence of an applicable R6 unlock. The current public tool does not provide the required v2 authentication path. This does not prove that every alternative access method is unavailable.

## New color-processing work

[cyZhu98/a7r6-looks](https://github.com/cyZhu98/a7r6-looks) has changes dated 2026-11-12: Classic Chrome profile work and Classic Negative calibration previews. The reviewed head is `d3bbe69a1093707b2fb66e1b397ec23f905a47e0`.

The project reconstructs Sony Creative Looks for Lightroom/Camera Raw from ARW metadata and constants obtained from a local Imaging Edge Edit installation. It does not establish camera firmware decryption, a service-mode entry, or a language unlock. This distinction matters when interpreting claims that R6 data has been decoded. Sources: [README at the reviewed commit](https://github.com/cyZhu98/a7r6-looks/blob/d3bbe69a1093707b2fb66e1b397ec23f905a47e0/README.md) and [technical record](https://github.com/cyZhu98/a7r6-looks/blob/d3bbe69a1093707b2fb66e1b397ec23f905a47e0/TECHNICAL.md).

The color pipeline may help comparative look research without extracting R6 firmware. Compatibility with the R5 requires separate parameter and calibration work.

## Next check

The target firmware and missing English option are now confirmed. The next device check is identification and service-access behavior on the actual body, using a computer to which the user can connect it. The local USB inventory on 2026-11-19 did not show a Sony device, and the target computer is pending. A diagnostic connection would establish compatibility evidence; it is not an established English-unlock procedure. A camera-specific access method and verified property mapping remain necessary before changing the language configuration.
