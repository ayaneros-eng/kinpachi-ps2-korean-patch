# 킨파치 선생님 PS2 한국어 패치 v267

『3年B組金八先生 伝説の教壇に立て！ 完全版』 일본판의 한국어 패치입니다. 한국어 대사·기록문·메뉴·그래픽과 학생 문자 영상을 적용하고, 두 줄 자막의 분할·읽기 호흡·가독성을 다듬었습니다.

**[간편 설치 ZIP 받기](https://github.com/ayaneros-eng/kinpachi-ps2-korean-patch/releases/download/v267/Kinpachi_KR_v267_Windows.zip)** · [릴리스 설명](https://github.com/ayaneros-eng/kinpachi-ps2-korean-patch/releases/tag/v267) · [배포 범위](LEGAL_SCOPE_KO.txt)

직접 준비한 **일본판 완전판 원본 ISO**를 읽어 별도의 한국어 ISO를 만듭니다. 게임과 BIOS는 제공하지 않으며, 원본 ISO는 변경하지 않습니다.

## 필요한 원본 ROM

아래 원본만 지원합니다. 파일 이름보다 **크기와 SHA-256**이 중요합니다.

| 항목 | 필요한 값 |
| --- | --- |
| 게임 | 3年B組金八先生 伝説の教壇に立て！ 完全版 |
| 기종·지역 | PlayStation 2 / 일본판 |
| 제품 번호 | **SLPM-66089** |
| 디스크 안 실행 파일 | `SLPM_660.89` |
| 원본 ISO 크기 | **4,680,515,584바이트** |
| 원본 SHA-256 | `4eb6db476d86bf1ea22f0e75d1412150fd8af716302c86d180b9a9fe5c209fb4` |

일반판, 다른 지역판, 이미 한국어 패치를 적용한 ISO는 입력으로 사용할 수 없습니다. 원본 검사가 실패하면 강제로 적용하지 말고 판본과 파일을 확인하세요. ROM 다운로드 링크는 제공하지 않습니다.

## 설치 준비

- Windows x64 PC(Intel/AMD 64비트)가 필요합니다. 간편 실행기가 기존 **Python 3.12 64비트**를 먼저 확인하고, 없으면 공식 런타임 준비를 안내합니다.
- 처음에는 전용 실행 환경과 의존성을 설치할 인터넷 연결이 필요합니다.
- **결과를 저장할 드라이브에 10 GiB 이상의 여유 공간**이 필요합니다. 원본 ISO 외에 새 ISO와 임시 작업 파일이 별도로 생깁니다.
- ZIP을 먼저 압축 해제하세요. 압축 파일 안에서 직접 실행하지 마세요.

## 간편하게 적용하기

패치 파일은 [Releases의 **Kinpachi_KR_v267_Windows.zip**](https://github.com/ayaneros-eng/kinpachi-ps2-korean-patch/releases/download/v267/Kinpachi_KR_v267_Windows.zip)입니다. 저장소의 소스 다운로드(`Code → Download ZIP`)에는 실행 패치가 포함되지 않습니다.

1. **Kinpachi_KR_v267_Windows.zip**을 받아 새 폴더에 압축 해제합니다.
2. **`한글패치_만들기.cmd`를 더블클릭**합니다.
3. 원본 ISO를 선택하고, 완성 파일을 저장할 폴더를 선택합니다.
4. 요약을 확인하면 환경 준비와 패치 생성을 진행합니다. Python이 없으면 **공식 Python 3.12.10 런타임 다운로드·준비 동의 창**이 먼저 나타납니다.
5. 저장 위치 안에 새로 만들어진 `Kinpachi-v267-날짜-식별자` 폴더에서 완성 ISO와 결과 보고서를 확인합니다.

필요한 런타임은 CPython 공식 NuGet 배포본(약 14.5MB)을 받아 `%LOCALAPPDATA%\KinpachiPatch\python-3.12.10-nuget\`에 압축을 풉니다. SHA-256·공식 SHA-512와 Python Software Foundation 서명을 검사합니다. Windows 설치·등록 없이 사용하며 PATH·기본 앱·시스템 실행 정책을 변경하지 않습니다. [Python 공식 NuGet 배포 안내](https://docs.python.org/3.12/using/windows.html#the-nuget-org-packages)

실행기는 원본 ISO를 덮어쓰지 않습니다. 전용 실행 환경·작업 파일·로그는 별도 경로에 만듭니다. 하위 `patch` 폴더는 검증 대상이므로 파일을 넣거나 편집하지 마세요.

영상·그래픽을 원본에서 생성하므로 시간이 걸릴 수 있습니다. 진행 메시지가 잠시 없어도 영상 처리 중일 수 있습니다. 실패했다면 결과 폴더의 로그를 확인하고, `.partial` 파일은 게임 실행에 사용하지 마세요.

## 소스 패키지로 적용하기

명령행을 직접 사용하려는 경우의 방법입니다. 간편 실행기를 쓰면 아래 명령을 입력할 필요가 없습니다. Python 3.12 64비트가 설치되어 있어야 합니다.

1. Releases의 **Kinpachi_KR_v267_Windows.zip**을 새 폴더에 압축 해제합니다. 패치 폴더 안의 파일을 수정하거나 다른 파일을 추가하지 마세요.
2. 하위 `patch` 폴더(`build_patch.py`와 `README_KO.txt`가 있는 곳)에서 PowerShell을 열고 전용 환경을 설치합니다.

   ```powershell
   powershell -NoProfile -ExecutionPolicy Bypass -File .\setup_build_env.ps1
   ```

   `Bypass`는 이 실행에만 적용되며 시스템 설정을 바꾸지 않습니다. 기본 환경은 패치 폴더의 상위 `kinpachi-build-runtimes`에 만들어집니다. 성공한 환경 설치는 반복하지 않아도 됩니다.

3. 다음 명령의 경로를 자신의 원본과 저장 위치에 맞게 바꿔 실행합니다. 출력 ISO와 작업 폴더에는 **아직 없는 이름**을 지정하세요.

   ```powershell
   py -3.12 -X utf8 -B .\build_patch.py --source-iso "D:\Games\Original.iso" --output "D:\Games\Kinpachi_KR_v267.iso" --work-dir "D:\Games\kinpachi-v267-build"
   ```

4. 완료 후 작업 폴더의 `BUILD_REPORT.json`이 `PASS_COMPLETE_ORIGINAL_SOURCE_BUILD`인지 확인합니다. 검증을 통과해야 `.partial` 파일이 완성 ISO 이름으로 바뀝니다. `.partial`만 남았다면 실행용으로 사용하지 마세요.

작업 폴더의 `graphics.log`, `messages.log`, `prologue.log`에서 구성 요소별 진행을 확인할 수 있습니다. Python 경로 직접 지정 등 자세한 옵션은 `patch/README_KO.txt`를 참고하세요.

## 완성 파일 확인

| 항목 | 정상 결과 |
| --- | --- |
| 패치 ISO 크기 | **4,683,096,064바이트** |
| 패치 ISO SHA-256 | `10006d0f5a7ff55152822b8dc459e319f60d1912865f9ab8597d11b2802324b7` |

PowerShell에서 파일 해시를 확인할 수 있습니다.

```powershell
Get-FileHash -Algorithm SHA256 -LiteralPath "D:\Games\Kinpachi_KR_v267.iso"
```

이전 버전의 강제저장에는 예전 코드나 미리 읽은 영상이 남아 있을 수 있습니다. 패치 후에는 **새 부팅 뒤 일반 게임 저장**을 불러오세요. 메모리카드나 일반 저장 파일을 삭제할 필요는 없습니다.

## v267 변경 사항

- 초반 학생 문자 영상에서 검은 화면으로 멈추던 원인을 수정하고, 같은 방식의 문자 영상 23편에 예방 검사를 적용했습니다.
- 프롤로그 환영 문구의 검은 사각형을 없애고, 원본 하늘 배경과 등장 속도를 따른 한글 제목으로 바꿨습니다.
- 옵션의 스테레오·모노와 화질 관련 글자가 겹치던 표시를 수정했습니다.
- 이전 음성 배치 수정과 본문·자막 타이밍은 유지했습니다.

자세한 변경 내용은 [v267 릴리스 노트](RELEASE_NOTES_KO.md)를 참고하세요.

## 실제 게임 화면

아래 두 장은 **v267을 PCSX2 2.8.2에서 실행한 화면**입니다. 이미지 합성이나 자막 미리보기가 아닌 실제 캡처를 편집 없이 사용했습니다.

![하늘 배경에 표시되는 한국어 프롤로그 환영 문구](prologue-title.png)

프롤로그: 검은 제목판을 제거하고 원래 하늘 배경 위에 한글을 표시합니다.

![스테레오가 선택된 한국어 사운드·화질 옵션 화면](options-stereo.png)

옵션: 선택 글자와 배경 글자의 겹침을 정리했습니다. 화면 가장자리의 가는 선은 별도 관찰 사항으로 남아 있습니다.

## 확인한 범위와 남은 점

본문 15,414개 ID를 원문 기록문과 표시 경로에 대조했고, 문맥·발음·특수 장면 시각을 확정할 수 없는 항목은 별도로 남겼습니다. 이것이 모든 음성을 직접 듣거나 전 구간을 플레이했다는 뜻은 아닙니다.

v267은 PCSX2 2.8.2에서 새 부팅해 **첫 학생 문자 종료 후 지도 복귀**, **프롤로그 제목과 다음 교무실 진입**, **스테레오·모노·화질 옵션 조작**을 확인했습니다. 문자 23편의 정적 검사는 통과했지만, 다른 22편과 게임 전 구간을 실제로 플레이한 것은 아닙니다. **Retroid와 PS2 실기에서 v267은 아직 검증하지 않았습니다.**

남은 항목과 구체적인 한계는 배포 ZIP의 `patch/KNOWN_LIMITS_KO.txt`에서 확인할 수 있습니다. 문제를 제보할 때는 버전, 기기·에뮬레이터, 장면, 새 부팅 여부와 화면을 함께 알려 주세요. 원본 ISO·BIOS·게임 데이터는 올리지 마세요.

## 배포 구성

패치 ZIP에는 원본에서 한국어 ISO를 생성하는 코드·번역·제작 정보와 OFL 글꼴이 들어 있습니다. 원본 또는 수정된 ISO, 게임 영상·원음·배경, BIOS, 저장 데이터는 포함하지 않습니다. 이 저장소의 실제 게임 화면 두 장은 패치 결과를 설명하기 위한 자료이며 설치 입력이 아닙니다.

포함된 글꼴의 저작권 고지와 OFL 라이선스는 그대로 유지해 주세요. 원본 게임의 권리와 상표는 각 권리자에게 있습니다. 구성 범위는 [배포 범위 고지](LEGAL_SCOPE_KO.txt)를 참고하세요.
