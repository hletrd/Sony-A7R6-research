# 외부 소스

2026-11-05에 수집한 분석 후보이다. 각 저장소의 대상 기종과 기능은 A7R VI 호환성을 보장하지 않는다. 로컬 소스 수집 작업 공간에서는 각 저장소를 Git 서브모듈로 관리한다. 공개 연구 기록에는 검토한 커밋과 적용 범위를 기록한다.

| 저장소 | 조사 용도 |
| --- | --- |
| [ma1co/Sony-PMCA-RE](https://github.com/ma1co/Sony-PMCA-RE) | Sony 카메라 통신과 PMCA 관련 구현 |
| [masterflai/pmca-re-reloaded](https://github.com/masterflai/pmca-re-reloaded) | PMCA 도구 재구현 |
| [voxivoid/recipe-lab-sony-pmca](https://github.com/voxivoid/recipe-lab-sony-pmca) | PMCA 관련 응용 소스 |
| [Hearts-Ace/sony-a7r5-custom-firmware](https://github.com/Hearts-Ace/sony-a7r5-custom-firmware) | A7R V 관련 수정 연구 |
| [Erlla/sony-a7m4-custom-firmware](https://github.com/Erlla/sony-a7m4-custom-firmware) | A7 IV 관련 수정 연구 |
| [YuuLuo/a7c2-camera-tools](https://github.com/YuuLuo/a7c2-camera-tools) | A7C II 관련 도구 |
| [DavidBuchanan314/ILCE-7M4-RE](https://github.com/DavidBuchanan314/ILCE-7M4-RE) | A7 IV 하드웨어와 펌웨어 분석 |
| [QAQLeonard/a7c2-fl23-research](https://github.com/QAQLeonard/a7c2-fl23-research) | A7C II FL2/FL3 연구 |
| [q19032/Sony-firmware-unpacker](https://github.com/q19032/Sony-firmware-unpacker) | Sony 펌웨어 추출 구현 |
| [DavidBuchanan314/Sony-ILCE-7M4-Linux](https://github.com/DavidBuchanan314/Sony-ILCE-7M4-Linux) | A7 IV 관련 Linux 소스 |
| [DavidBuchanan314/fwtool.py, a7iv](https://github.com/DavidBuchanan314/fwtool.py/tree/a7iv) | 검증에 사용한 펌웨어 추출 도구 |
| [EnglandLobster/sony-lut-camera](https://github.com/EnglandLobster/sony-lut-camera) | 구형 Android/PMCA의 LUT 처리 구현 |

fwtool 검증 결과는 [실험 기록](research/2026-11-05-fwtool-a7iv.md)에, LUT 프로젝트의 적용 범위는 [검토 기록](research/2026-11-05-sony-lut-camera.md)에 정리한다. 나머지 소스는 수집 단계이며 개별 기능을 검증하지 않았다.
