# Sayntra 제3자 소프트웨어 및 모델 고지

최종 갱신: 2026-07-29

Sayntra Windows 배포본은 여러 제3자 Python 패키지와 네이티브 라이브러리를 포함하고,
Whisper 변환 모델을 첫 실행 때 별도로 내려받는다. 각 구성요소는 해당 권리자의
라이선스를 따른다. Sayntra 자체 코드의 비공개·독점적 권리 표시는 제3자 라이선스를
대체하거나 제한하지 않는다.

## 0.4.1 배포본에서 확인한 주요 런타임 구성요소

| 구성요소 | 확인 버전 | 패키지 metadata의 라이선스 표기 |
|---|---:|---|
| PySide6 | 6.11.1 | `LGPL-3.0-only OR GPL-2.0-only OR GPL-3.0-only` |
| faster-whisper | 1.2.1 | MIT |
| CTranslate2 | 4.8.1 | MIT |
| huggingface-hub | 1.24.0 | Apache-2.0 |
| NumPy | 2.4.6 | BSD-3-Clause 및 번들 구성요소의 복합 라이선스 |
| PyAV | 18.0.0 | BSD-3-Clause |
| ONNX Runtime | 1.28.0 | MIT |
| Pydantic | 2.13.4 | MIT |
| PyYAML | 6.0.3 | MIT |
| sounddevice | 0.5.5 | MIT |
| Click | 8.4.2 | BSD-3-Clause |
| tqdm | 4.69.1 | MPL-2.0 AND MIT |
| NVIDIA cuBLAS wheel | 12.9.2.10 | `LicenseRef-NVIDIA-Proprietary` |
| NVIDIA cuDNN wheel | 9.24.0.43 | `LicenseRef-NVIDIA-Proprietary` |
| tokenizers | 0.23.1 | 배포 metadata에서 미선언; 별도 확인 필요 |

이 표는 사람이 읽기 쉬운 주요 목록이며 완전한 바이너리·전이 의존성 감사 결과가
아니다. `0.4.1` 실제 portable의 `*.dist-info/METADATA`와 고정 모델 정보를 읽은
CycloneDX 1.6 SBOM은 Release의 `Sayntra-0.4.1.cdx.json`으로 함께 배포한다.

## 포함된 라이선스 원문

PyInstaller 빌드는 `copy_metadata()`로 주요 패키지의 `.dist-info` metadata와 그
패키지가 wheel에 제공한 `LICENSE`, `COPYING`, `NOTICE` 파일을 portable의
`_internal` 아래에 함께 둔다. 예:

```text
_internal\<package>-<version>.dist-info\METADATA
_internal\<package>-<version>.dist-info\licenses\...
```

일부 프로젝트는 별도 라이선스 파일을 wheel에 넣지 않거나 metadata 표현이
불완전하다. 파일이 존재한다는 사실만으로 Sayntra의 재배포 의무가 모두 충족됐다고
판정하지 않는다.

## Qt/PySide6와 NVIDIA의 별도 검토

- PySide6/Qt는 선택한 오픈소스 또는 상용 라이선스 경로에 따라 재링크·고지·소스 제공
  등 의무가 달라질 수 있다. 실제 배포 방식이 해당 조건을 충족하는지 Qt 공식 문서와
  전문가 검토로 확정해야 한다.
- NVIDIA CUDA/cuDNN wheel과 DLL은 NVIDIA의 별도 독점 라이선스 조건을 따른다.
  재배포 가능 범위와 필요한 고지를 NVIDIA 공식 조건으로 다시 확인해야 한다.
- `tokenizers`처럼 현재 wheel metadata에 라이선스 표현이 없는 항목은 upstream
  LICENSE와 실제 번들 버전을 수동 대조해야 한다.

## 외부 모델

Sayntra는 설치기에 Whisper 모델 가중치를 넣지 않는다. 첫 실행 때 다음 고정 snapshot을
사용자 캐시에 다운로드한다.

```text
repository: mobiuslabsgmbh/faster-whisper-large-v3-turbo
revision: 0a363e9161cbc7ed1431c9597a8ceaf0c4f78fcf
```

모델 repository의 모델 카드와 라이선스, 원본 모델 및 변환물의 조건은 앱 라이선스와
별도로 적용될 수 있다. 상용·대규모 공개 배포 전에 해당 revision의 파일과 라이선스를
별도로 보존·검토해야 한다.

## 감사 상태

이 문서는 2026-07-29의 패키지 metadata와 실제 `0.4.1` portable에서 확인한
인벤토리다. 법률 자문, 전체 라이선스 감사 또는 준수 완료 인증이 아니다. 최종 배포
전에는 다음이 필요하다.

1. 새 빌드의 CycloneDX SBOM 생성
2. SBOM과 portable payload·릴리스 manifest 버전 일치 확인
3. 각 wheel 및 네이티브 DLL의 라이선스 원문 보존 확인
4. Qt/PySide6, NVIDIA, tokenizers와 모델 revision의 전문 검토
5. 최종 이용조건과 제3자 고지의 설치기 포함 여부 확인
