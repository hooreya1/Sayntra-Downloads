# Sayntra 베타 지원

Sayntra는 현재 Windows용 공개 베타다. 베타 기간에는 최신 `0.4.x` 버전을 대상으로
최선 노력(best effort) 방식으로 문제를 확인하며, 응답 시간이나 모든 장치의 호환성을
보장하지 않는다.

## 지원 범위

- 목표 운영체제: Windows 10 version 2004/build 19041 이상 또는 Windows 11 x64
- 목표 하드웨어: 호환 NVIDIA GPU와 최신 드라이버
- 입력: 한국어, 영어, 한영 혼합 음성
- 배포: 사용자 계정용 Windows 설치 프로그램

현재 실측 기준선은 Windows 11, RTX 4070 Ti, FIFINE USB 마이크 한 조합이다. Windows
10, 다른 GPU·VRAM, 다른 마이크의 호환성은 아직 정식으로 입증하지 않았다. 최소 VRAM
수치도 확정 전이다. 자세한 제한은 [KNOWN_ISSUES.md](KNOWN_ISSUES.md)를 확인한다.

## 일반 문의와 오류 신고

[GitHub Issues](https://github.com/hooreya1/Sayntra-Downloads/issues)에 새 이슈를
작성한다. 먼저 최신 베타와 [알려진 문제](KNOWN_ISSUES.md)를 확인한다.

가능하면 다음 비식별 정보만 포함한다.

- Sayntra 버전
- Windows 버전과 빌드 번호
- GPU 모델과 드라이버 버전
- 마이크 유형(예: `USB_MIC`)과 녹음 입력 방식(키보드/X1/X2)
- 재현 단계와 재현 횟수
- 앱이 표시한 고정 오류 코드 또는 예외 종류
- `LocalWhisperDoctor.exe`가 보여 준 PASS/WARN/FAIL 요약

다음 내용은 공개 이슈나 첨부 파일에 넣지 않는다.

- 원본 음성
- 실제 전사 문장
- 클립보드 내용
- 창 제목, 문서명, URL, 사용자명
- 개인 용어 파일
- 이메일·전화번호·주소 같은 개인정보
- 전체 로그 파일

필요한 로그 행만 확인하되 내용 필드가 없음을 먼저 검토한다. 민감한 보안 문제는
공개 이슈가 아니라 [비공개 보안 신고](SECURITY.md)를 사용한다.

## 설치·업데이트·제거

- 현재 자동 업데이트는 없다. 새 버전은
  [GitHub Releases](https://github.com/hooreya1/Sayntra-Downloads/releases)에서
  직접 확인하고 설치한다.
- 동일 AppId를 사용하는 새 설치기는 기존 설정을 보존하는 제자리 업그레이드를
  목표로 한다. 업데이트 전 `%LOCALAPPDATA%\LocalWhisper\config`를 백업할 수 있다.
- 앱 제거 후에도 사용자 설정·비식별 로그와 Hugging Face 모델 캐시는 데이터 손실을
  막기 위해 남는다. 완전 삭제 방법은 [PRIVACY.md](PRIVACY.md#앱-제거와-완전-삭제)를
  따른다.

## 별도 지원 대상이 아닌 항목

- macOS, Linux, Android, iOS
- CPU-only 환경과 AMD/Intel GPU
- 모델·VAD·안전 게이트를 임의로 수정한 빌드
- 제3자 재패키징 설치 프로그램
- 클라우드 STT, 계정, 결제, 동기화
