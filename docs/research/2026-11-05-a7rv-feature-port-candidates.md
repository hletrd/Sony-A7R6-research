# A7R V feature-port candidates

Reviewed on 2026-11-05. The implementation target is A7R V firmware 4.00. Donor feature availability comes from Sony's current Help Guides; portability assessments below are engineering inferences. No feature port, device installation, or runtime validation was performed in this comparison.

## Existing A7R V capabilities

The stock A7R V already provides S-Log2, S-Log3, and S-Cinetone through Picture Profiles. These should not be counted as missing FX3 features. The meaningful differences include custom LUT workflows and Cine EI exposure operation. See Sony's [A7R V Picture Profile documentation](https://helpguide.sony.net/ilc/2230/v1/en/contents/TP0002920003.html).

The A7R V's documented Creative Looks include FL, but not FL2 or FL3. Its movie stabilization provides Active, Standard, and Off, without Dynamic active. Its subject-recognition menu offers specific target categories without the newer general Auto selection. These observations describe the documented controls, not a complete inventory of dormant firmware code. Sources: [Creative Look](https://helpguide.sony.net/ilc/2230/v1/en/contents/TP0002911200.html), [SteadyShot](https://helpguide.sony.net/ilc/2230/v1/en/contents/TP0002897739.html), and [Recognition Target](https://helpguide.sony.net/ilc/2230/v1/en/contents/TP1000669441.html).

## Candidate comparison

| Feature | Documented reference | A7R V research assessment |
| --- | --- | --- |
| Shutter-angle control | [FX3, firmware 6.00 or later](https://helpguide.sony.net/ilc/2210/v1/en/contents/TP1001690662.html) | A bounded first video prototype: map angle and frame rate to the existing exposure controls, then investigate UI state and persistence. Exact timing and frame-rate transitions still require validation. |
| Anamorphic de-squeeze preview | [FX3](https://helpguide.sony.net/ilc/2210/v1/en/contents/TP1001106329.html) | Investigate the display-scaling path separately from recording. Sony's implementation has mode, AF, and stabilization restrictions; a menu entry alone would not reproduce it. |
| Importable user LUTs and LUT preview | [A7R VI](https://helpguide.sony.net/ilc/2620/v1/en/contents/211h_manage_lut.html), [A1 II](https://helpguide.sony.net/ilc/2440/v1/en/contents/211h_manage_lut.html), and [FX3](https://helpguide.sony.net/ilc/2210/v1/en/contents/TP1000888940.html) | A valuable but substantial imaging-path investigation. Separate importing a CUBE file, monitor preview, recorded-video processing, and embedded LUT metadata. No R5 path has been validated here. |
| FL2 and FL3 Creative Looks | [A7R VI](https://helpguide.sony.net/ilc/2620/v1/en/contents/0411B_creative_look.html); [A1 II firmware 4.00 or later](https://helpguide.sony.net/ilc/2440/v1/en/contents/0411B_creative_look.html) | A useful still-photo starting point because the collected R5 modification source already contains related work. Look tables, processing, menu selection, and persistent slots need separate validation. |
| Cine EI and Cine EI Quick | [FX3](https://helpguide.sony.net/ilc/2210/v1/en/contents/TP1000888942.html) | A larger exposure-and-monitoring project. Use R5-specific gain behavior and calibration; copying an EI label cannot reproduce another sensor's noise or dynamic range. |
| Automatic recognition-target selection | [A7R VI](https://helpguide.sony.net/ilc/2620/v1/en/contents/211h_recognition_target.html) and [A1 II](https://helpguide.sony.net/ilc/2440/v1/en/contents/211h_recognition_target.html) | Advanced research. Compare recognition-controller interfaces, models, and execution requirements before assuming this is a hidden setting. |
| Auto Framing | [A7R VI](https://helpguide.sony.net/ilc/2620/v1/en/contents/221h_auto_framing.html) and [A1 II](https://helpguide.sony.net/ilc/2440/v1/en/contents/221h_auto_framing.html) | Requires coordinated recognition, crop control, and output routing. Investigate supported resolutions and processing budgets before attempting a port. |
| Dynamic Active stabilization | [A7R VI](https://helpguide.sony.net/ilc/2620/v1/en/contents/0412B_movie_steadyshot.html) and [A1 II](https://helpguide.sony.net/ilc/2440/v1/en/contents/0412B_movie_steadyshot.html) | Advanced research into crop, scaling, stabilization, and calibration paths. Existing R5 Active mode does not establish compatibility with the newer implementation. |
| Pre-Capture and Continuous Shooting Speed Boost | [A7R VI](https://helpguide.sony.net/ilc/2620/v1/en/contents/231h_pre_capture.html) and [A1 II](https://helpguide.sony.net/ilc/2440/v1/en/contents/231h_pre_capture.html) | Pre-capture is a buffering/control candidate at R5-supported rates. Matching a donor's full-resolution burst rate is a separate sensor-throughput problem. Buffer ownership, AF/AE timing, and thermal behavior need validation. |

The LUT references document 16 user slots and 17-point or 33-point CUBE files. LUT preview is a separate function, as described in [A7R VI Display LUT](https://helpguide.sony.net/ilc/2620/v1/en/contents/211h_display_lut.html). These movie workflows do not establish arbitrary LUT processing for still-image JPEGs.

FX3 de-squeeze supports 1.3x and 2.0x from firmware 3.00, with 1.5x and 1.6x menu options added in firmware 7.00. Shutter angle and de-squeeze are useful FX3-specific reference features even though they are not A7R VI additions.

## Further candidates

FX3 supports DCI 4K recording and true 24.00p in its recording settings. This is a separate, harder candidate involving encoder dimensions, sensor modes, timing, muxing, and audio synchronization. The R5's documented 24p mode is 23.98 fps. Sources: [FX3 Movie Settings](https://helpguide.sony.net/ilc/2210/v1/en/contents/TP1000868278.html) and [A7R V Movie Settings](https://helpguide.sony.net/ilc/2230/v1/en/contents/TP0002911203.html).

The A1 II also documents [NR Shooting](https://helpguide.sony.net/ilc/2440/v1/en/contents/231h_nr_shoot_setting.html): a sequence of 4 to 32 RAW files combined on a computer. An R5 capture-sequence experiment may be useful, but writing suitable metadata and reproducing Sony's desktop integration require separate work. This is not in-camera RAW merging.

## Hardware-dependent differences

The A7R VI uses a fully stacked sensor and a BIONZ XR2 processor. Its higher readout and recording capabilities must not be treated as menu-only differences. Full-resolution burst performance, full-frame high-frame-rate video, and readout-related rolling-shutter improvements need sensor and processing support. This is an engineering assessment based on Sony's [A7R VI hardware description](https://www.sony.co.uk/electronics/interchangeable-lens-cameras/ilce-7rm6/specifications).

A7R VI [Dual Gain Shooting](https://helpguide.sony.net/ilc/2620/v1/en/contents/252h_dual_gain_shooting.html) is another distinct research area. It is not the same operation as selecting the FX3's low or high Base ISO. Neither the R6's dynamic-range behavior nor the FX3's low-light performance can be established by copying exposure-menu options to the R5.

## Existing source and evidence gaps

The collected [Hearts-Ace R5 source at be3dc9a](https://github.com/Hearts-Ace/sony-a7r5-custom-firmware/tree/be3dc9a622a797ce72270ff39a5d44ccaa33edc8) includes FL2/FL3 slot work and custom color-processing code. Its README distinguishes the main branch from a separate, unmerged photo/PPLUT branch. Those maintainer claims are external evidence; this workspace has not built or installed the modified firmware. Custom Look processing does not by itself establish a generic native user-LUT implementation.

Locally, R5 4.00 extraction has succeeded; the input classified as R6 1.02 has not been decrypted. The [fwtool author reports successful extraction for FX3 and A1 II](https://github.com/ma1co/fwtool.py/pull/52#issuecomment-5625960817), but those donor images have not been tested in this workspace. See the [local extraction record](2026-11-05-fwtool-a7iv.md).

## Initial investigation order

1. Inspect the existing R5 FL2/FL3 and color-processing work, preserving the distinction between source evidence and device validation.
2. Prototype shutter-angle control through the R5's existing exposure path. Use `exposure_time = shutter_angle / (360 * frame_rate)` as the desired mapping, then measure actual timing and supported quantization.
3. Investigate preview-only anamorphic de-squeeze and user-LUT display paths independently of recorded output.
4. Extend to Cine EI, recorded LUT processing, or DCI/24.00p only after the necessary R5 interfaces and calibration requirements are understood.
5. Treat AF automation, stabilization, auto framing, and pre-capture as separate investigations rather than bundling them into the first patch.
