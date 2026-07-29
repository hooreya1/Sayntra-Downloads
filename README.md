# Sayntra Downloads

한국어·영어 음성을 사용자 PC 안에서 텍스트로 바꾸고, 안전할 때만 현재 입력창에
붙여넣는 Windows 로컬 받아쓰기 앱 **Sayntra**의 공식 베타 다운로드 저장소다.

- 홈페이지: <https://hooreya1.github.io/Sayntra-Downloads/>
- 최신 베타: <https://github.com/hooreya1/Sayntra-Downloads/releases>
- 오류 신고: <https://github.com/hooreya1/Sayntra-Downloads/issues>
- 비공개 보안 신고:
  <https://github.com/hooreya1/Sayntra-Downloads/security/advisories/new>

## 현재 공개 버전

`0.4.1 Beta`가 현재 공개돼 있다. 정식 출시가 아니라 검증 범위가 제한된 Windows
베타이며, 미검증 항목은 [KNOWN_ISSUES.md](KNOWN_ISSUES.md)에 공개한다.

## 요구 사항과 검증 범위

- 목표 OS: Windows 10 version 2004/build 19041 이상 또는 Windows 11 x64
- x64, 호환 NVIDIA GPU, 최신 NVIDIA 드라이버와 입력 마이크
- 최소 VRAM: 아직 확정되지 않음
- 실제 검증 기준선: Windows 11, RTX 4070 Ti, FIFINE USB 마이크 한 조합

Windows 10과 다른 GPU·마이크 조합은 아직 정식 호환성 검증 전이다.

## 설치 파일 확인

Release에서 설치기와 같은 이름의 `.sha256` 파일을 함께 받은 뒤 PowerShell에서
확인한다.

```powershell
Get-FileHash .\Sayntra-Setup-0.4.1.exe -Algorithm SHA256
Get-Content .\Sayntra-Setup-0.4.1.exe.sha256
```

현재 공개 `0.4.1` 설치기는 코드 서명이 없어 Windows SmartScreen 또는 알 수 없는
발행자 경고가 나타날 수 있다. SHA-256은 전송 오류 확인에는 유용하지만 설치기와
sidecar가 함께 교체되는 저장소 침해의 진위성을 단독으로 보장하지 않는다.

## 첫 실행

설치판에는 Python과 필요한 Windows 런타임이 포함돼 있지만 Whisper 모델 가중치는
포함하지 않는다. 모델이 없으면 첫 실행 때 약 1.51 GiB의 고정 snapshot을 내려받는다.
모델 준비가 끝나기 전에는 받아쓰기를 시작할 수 없다.

## 문서

- [지원](SUPPORT.md)
- [베타 이용 조건](BETA_TERMS.md)
- [개인정보 안내](PRIVACY.md)
- [알려진 문제](KNOWN_ISSUES.md)
- [보안 정책](SECURITY.md)
- [제3자 소프트웨어 고지](THIRD_PARTY_NOTICES.md)
- [자체 코드 권리 고지](LICENSE.md)

이 저장소는 공식 설치 파일과 공개 문서를 위한 저장소다. Sayntra 소스 코드는 별도의
비공개 저장소에서 관리하며 공개 오픈소스 라이선스로 제공되지 않는다.
