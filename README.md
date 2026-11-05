# Sony-A7R6-research

Sony A7R VI(ILCE-7RM6)의 펌웨어 구조와 수정 가능성을 조사하는 공개 연구 저장소이다. A7R V(ILCE-7RM5) 펌웨어를 비교 대상으로 사용한다. 재현 방법과 확인된 결과를 기록한다.

## 현재 상태

2026-11-05에 `DavidBuchanan314/fwtool.py`의 `a7iv` 브랜치를 두 펌웨어 파일에 적용했다.

| 대상 | 결과 | 근거 |
| --- | --- | --- |
| A7R V 4.00 | `CXD90057_k8` 복호화 및 파일 추출 성공 | 내부 모델 ID `0x11030080`, 버전 `4.00` 확인 |
| A7R VI 1.02로 추정되는 파일 | `No decrypter found`로 추출 실패 | 공식 배포 크기 일치, 내부 모델과 버전은 미확인 |
| Sony LUT Camera | A7R V와 A7R VI 직접 설치 가능 여부 미확인 | 구형 Android/PMCA 앱이며 A6300 검증 기록 제공 |

펌웨어 두 파일의 최초 이름이 서로 바뀌어 있어 이름을 수정했다. A7R V는 내부 정보로 확인했고 A7R VI는 공식 파일 크기에 근거해 분류했다. 공식 배포 파일과 해시를 대조하지 않았다. 추출 성공은 수정 펌웨어의 설치 가능성을 뜻하지 않는다.

## 조사 기록

- [fwtool a7iv 검증](docs/research/2026-11-05-fwtool-a7iv.md)
- [Sony LUT Camera 적용 범위](docs/research/2026-11-05-sony-lut-camera.md)
- [외부 소스 목록](docs/sources.md)
- [펌웨어 식별 정보](data/firmware-manifest.json)
- [작업 규칙](AGENTS.md)

## 로컬 분석

펌웨어 원본과 추출 결과는 이 저장소에 포함하지 않는다. 조사 기록의 파일명, 크기와 SHA-256으로 입력을 식별한다. 외부 도구는 기록된 커밋을 사용하고 별도 경로에 결과를 생성한다.

```sh
git clone https://github.com/hletrd/Sony-A7R6-research.git
cd Sony-A7R6-research
```

## 공식 자료

- [Sony A7R V 4.00 배포 정보](https://www.sony.com/electronics/support/e-mount-body-ilce-7-series/ilce-7rm5/software/00292267)
- [Sony A7R VI 1.02 배포 정보](https://www.sony.com/electronics/support/e-mount-body-ilce-7-series/ilce-7rm6/software/00413269)
