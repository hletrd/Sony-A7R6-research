# Sony LUT Camera 적용 범위

2026-11-05에 [EnglandLobster/sony-lut-camera](https://github.com/EnglandLobster/sony-lut-camera)의 README, [빌드 문서](https://github.com/EnglandLobster/sony-lut-camera/blob/main/docs/BUILD.md)와 [검증 기록](https://github.com/EnglandLobster/sony-lut-camera/blob/main/docs/STATUS.md)을 검토했다. 코드를 빌드하지 않았고 실기기에 설치하지 않았다.

## 확인한 범위

이 프로젝트는 Sony의 구형 Android/PMCA 환경에 APK를 설치해 사진에 3D LUT를 적용한다. 유지관리자는 A6300으로 촬영하고 원본 JPEG와 LUT 적용 JPEG를 저장한 결과를 보고한다. 빌드 문서는 구형 Sony Android와 ARMv5를 대상 환경으로 명시한다.

검토한 자료에서 A7R V와 A7R VI의 설치나 촬영 성공 기록은 확인하지 못했다. 다른 기종을 실험적으로 지원한다는 문구를 두 기종의 호환성 근거로 사용하지 않는다.

## 연구 활용

LUT 보간과 JPEG 처리 코드는 색 처리 구현의 참고 자료이다. Sony 촬영 인터페이스와 Android 런타임에 의존하는 부분은 A7R V와 A7R VI의 펌웨어 수정 방법으로 바로 적용할 수 있다고 판단하지 않는다. 실제 적용 가능성은 대상 기종의 실행 환경과 API를 조사한 뒤 검증한다.

프로젝트의 원본 코드는 GPL-3.0-only이며 LUT와 폰트 등의 자산에는 별도 라이선스가 있다. 코드를 재사용할 때 [라이선스](https://github.com/EnglandLobster/sony-lut-camera/blob/main/LICENSE), [자산 출처](https://github.com/EnglandLobster/sony-lut-camera/blob/main/ASSET_LICENSES.md)와 [제삼자 자료](https://github.com/EnglandLobster/sony-lut-camera/blob/main/THIRD_PARTY_NOTICES.md)를 확인한다.
