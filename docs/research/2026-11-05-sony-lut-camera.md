# Sony LUT Camera applicability

On 2026-11-05, the README, [build documentation](https://github.com/EnglandLobster/sony-lut-camera/blob/main/docs/BUILD.md), and [validation records](https://github.com/EnglandLobster/sony-lut-camera/blob/main/docs/STATUS.md) of [EnglandLobster/sony-lut-camera](https://github.com/EnglandLobster/sony-lut-camera) were reviewed. The code was not built or installed on a camera.

## Documented scope

The project installs an APK in Sony's older Android/PMCA environment to apply 3D LUTs to photographs. The maintainer reports A6300 captures that saved both the original JPEG and a LUT-processed JPEG. The build documentation identifies older Sony Android and ARMv5 as its target environment.

The reviewed material did not establish successful installation or capture on the A7R V or A7R VI. Experimental support for other models is not evidence of compatibility with these two cameras.

## Research use

The LUT interpolation and JPEG processing code can inform color-processing research. Components that depend on Sony's capture interfaces and Android runtime have not been established as directly applicable to A7R V or A7R VI firmware modification. Applicability requires separate investigation of the target cameras' execution environments and APIs.

The project's original code is GPL-3.0-only. Assets such as LUTs and fonts have separate licenses. Before reusing code or assets, check the [license](https://github.com/EnglandLobster/sony-lut-camera/blob/main/LICENSE), [asset provenance](https://github.com/EnglandLobster/sony-lut-camera/blob/main/ASSET_LICENSES.md), and [third-party notices](https://github.com/EnglandLobster/sony-lut-camera/blob/main/THIRD_PARTY_NOTICES.md).
