# Sayntra 개인정보 및 로컬 데이터 안내

최종 갱신: 2026-07-29
적용 대상: Sayntra Windows 공개 베타

## 요약

Sayntra는 마이크 음성을 사용자 PC에서 로컬 Whisper 모델로 전사한다. 계정, 광고,
분석 SDK, 사용량 텔레메트리와 클라우드 STT를 사용하지 않는다. 앱은 원본 음성 파일과
전사 이력을 의도적으로 디스크에 쓰지 않는다.

다만 “앱이 저장하지 않는다”는 설명이 Windows의 클립보드 기록, 클라우드 클립보드,
원격 데스크톱 동기화, 페이지 파일, 최대 절전 파일, crash dump와 다른 프로그램의
동작까지 통제하거나 완전 무잔존을 보장한다는 뜻은 아니다.

## 앱이 처리하는 정보

| 정보 | 처리 목적 | 기본 보관 |
|---|---|---|
| 마이크 샘플과 500ms 프리롤 | 녹음과 로컬 전사 | 작업 중 RAM, 작업 종료 시 참조 폐기 |
| 전사 결과 | 개인 용어 교정과 붙여넣기 | RAM 및 Windows 클립보드, 전사 이력 파일 없음 |
| foreground HWND/process/focus epoch | 잘못된 창 붙여넣기 차단 | 작업 중 비식별 상태 |
| 사용자 설정과 개인 용어 | 마이크·입력·표기 설정 | `%LOCALAPPDATA%\LocalWhisper\config` |
| 운영 로그 | 오류 진단 | `%LOCALAPPDATA%\LocalWhisper\logs`의 회전 로그 |
| Whisper 모델 | 로컬 추론 | Hugging Face 사용자 캐시 |

운영 로그는 상태 전이, 시간, 오디오·VAD 길이, 세그먼트 수, 고정 오류 코드와
붙여넣기 전송/보류 여부만 허용한다. 원본 음성, 전체 전사문, 클립보드 내용, 개인
용어가 포함된 실제 발화와 창 제목은 로그에 남기지 않는 것이 제품 규칙이다.

## 네트워크 사용

Whisper 모델이 로컬 캐시에 없으면 첫 실행 때 다음 고정 source에서 모델 snapshot을
다운로드한다.

```text
repository: mobiuslabsgmbh/faster-whisper-large-v3-turbo
revision: 0a363e9161cbc7ed1431c9597a8ceaf0c4f78fcf
```

이 다운로드 과정에서는 Hugging Face 서비스와 네트워크 통신이 발생한다. 서비스
운영자는 네트워크 요청에 수반되는 IP 주소 등의 메타데이터를 자체 정책에 따라 처리할
수 있으므로 [Hugging Face 개인정보 안내](https://huggingface.co/privacy)를 별도로
확인한다.

현재 Sayntra 자체 서버로 음성, 전사문, 클립보드, 창 제목, 개인 용어 또는 사용 통계를
전송하는 기능은 없다. 홈페이지·GitHub 방문과 설치기 다운로드는 사용자가 브라우저에서
이용하는 별도 서비스다.

## Windows 클립보드 주의

전사 결과는 Unicode 클립보드에 기록된 뒤 안전 게이트가 허용하는 경우에만 `Ctrl+V`
명령을 보낸다. 다음 Windows 또는 제3자 기능을 켠 경우 클립보드 내용이 앱 외부에
보관되거나 동기화될 수 있다.

- Windows 클립보드 기록
- 장치 간 클라우드 클립보드
- 원격 데스크톱 클립보드 리디렉션
- 클립보드 관리자와 보안·모니터링 프로그램

민감한 받아쓰기를 사용할 때는 해당 기능과 조직 정책을 사용자가 확인해야 한다.

## 앱 제거와 완전 삭제

제거 프로그램은 설정 손실을 막기 위해 다음 경로를 자동 삭제하지 않는다.

```text
%LOCALAPPDATA%\LocalWhisper
HF_HOME
%USERPROFILE%\.cache\huggingface
```

완전히 삭제하려면:

1. Sayntra를 종료하고 Windows 설정에서 앱을 제거한다.
2. 필요한 개인 용어를 백업한 뒤 `%LOCALAPPDATA%\LocalWhisper`를 확인해 삭제한다.
3. 다른 Hugging Face 프로그램이 같은 캐시를 사용하는지 확인한 뒤, 더 이상 필요하지
   않은 경우에만 `HF_HOME` 또는 기본 Hugging Face 캐시에서 해당 모델 snapshot을
   삭제한다.
4. 민감한 클립보드가 남아 있으면 새 비민감 내용을 복사하고 Windows 클립보드 기록을
   별도로 지운다.

## 문의

일반 개인정보 문의는 [GitHub Issues](https://github.com/hooreya1/Sayntra-Downloads/issues)에
개인정보 없이 작성한다. 비공개 처리가 필요한 개인정보·보안 결함은
[GitHub 비공개 보안 신고](https://github.com/hooreya1/Sayntra-Downloads/security/advisories/new)를
사용한다.

이 문서는 현재 베타의 실제 데이터 흐름 설명이며 법률 자문이나 모든 국가의 법적
준수 완료 선언이 아니다. 계정·결제·텔레메트리·클라우드 기능이 추가되기 전 데이터
흐름과 이 문서를 다시 검토해야 한다.
