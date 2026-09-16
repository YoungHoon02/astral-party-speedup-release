# Astral Party 배속 모드

Astral Party에서 화면에 재생되는 캐릭터와 각종 연출의 애니메이션 속도를
<code>1x / 1.5x / 2x / 3x / 5x</code>로 조절하는 BepInEx 모드입니다.

다른 플레이어의 애니메이션도 빠르게 보이지만 서버에 전달되는 행동과 실제 턴 진행
시점은 바꾸지 않습니다. 화면 하단의 턴 타이머도 배속과 무관하게 실제 시간으로
흘러갑니다.

> 이 저장소는 **배포 전용**입니다. 소스 코드는 포함되어 있지 않습니다.

## 다운로드

[![최신 릴리스 다운로드](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fraw.githubusercontent.com%2FYoungHoon02%2Fastral-party-speedup-release%2Fdistribution%2Frelease-index.json&query=%24.version&prefix=v&label=DOWNLOAD&color=7C3AED&logo=github&logoColor=white&style=for-the-badge&cacheSeconds=300)](../../releases/latest)

버튼의 버전은 `distribution/release-index.json`을 기준으로 자동 갱신됩니다.

v1.0.3 배포 파일 SHA-256:

~~~text
07f810fb25fdde8c4457e2dc3f045f97aeff6f79d0d0f61a469b5df935aa27c4
~~~

## 준비물

- Windows x64 버전 Astral Party
- [BepInEx 6 Unity.IL2CPP-win-x64](https://builds.bepinex.dev)
- [.NET Desktop Runtime 8.0 x64](https://dotnet.microsoft.com/download/dotnet/8.0)

.NET Desktop Runtime은 게임과 별도로 실행되는 배속 설정 창에 필요합니다.

## 설치

### 1. BepInEx 설치

이미 BepInEx 6 IL2CPP가 설치되어 있다면 이 단계는 건너뛰어도 됩니다.

1. BepInEx 빌드 페이지에서 <code>Unity.IL2CPP-win-x64</code>로 시작하는 최신 zip을 받습니다.
2. zip의 내용을 <code>AstralParty_INT.exe</code>가 있는 게임 폴더에 풉니다.
3. 게임을 한 번 실행한 뒤 종료합니다. 첫 실행은 interop 파일 생성 때문에 오래 걸릴 수 있습니다.

Steam 설치 경로는 일반적으로 다음과 같습니다.

~~~text
...\Steam\steamapps\common\Astral Party\8vJXnINT\
~~~

### 2. UnityLogListening 비활성화

> [!CAUTION]
> BepInEx를 새로 설치했다면 반드시 확인해야 합니다. 이 게임에서는
> <code>UnityLogListening = true</code>가 시작 직후 <code>AccessViolationException</code>을 일으킬 수 있습니다.

게임을 한 번 실행해 <code>BepInEx\config\BepInEx.cfg</code>가 생성된 다음 아래 값을
<code>false</code>로 바꿉니다.

~~~ini
[Logging]
UnityLogListening = false
~~~

이 설정은 모드 기능이 아니라 BepInEx의 Unity 로그 수집 기능입니다. 문제가 발생하면
다음과 같은 로그가 남을 수 있습니다.

~~~text
System.AccessViolationException: Attempted to read or write protected memory.
   at Il2CppInterop.Runtime.Injection.Hooks.MetadataCache_GetTypeInfoFromTypeDefinitionIndex_Hook
~~~

### 3. 모드 설치

1. 위의 <code>AstralPartyAnimSpeed-v1.0.3.zip</code>을 받습니다.
2. zip을 <code>AstralParty_INT.exe</code>가 있는 게임 폴더에 그대로 풉니다.
3. 덮어쓰기 여부를 물으면 허용합니다.
4. 게임을 실행합니다.

정상 설치되면 다음 폴더에 플러그인과 설정 앱이 들어갑니다.

~~~text
BepInEx\plugins\AstralPartyAnimSpeed\
~~~

## 사용법

게임을 실행하면 작은 설정 창이 함께 열립니다.

- 원하는 배속을 누르면 **Save 버튼 없이 즉시 저장**됩니다.
- 게임에는 기본적으로 몇 초 안에 새 배속이 적용됩니다.
- <code>Now running at 3x</code>와 같은 상태 문구로 현재 배속을 확인할 수 있습니다.
- <code>Launch this window when the game starts</code>를 해제하면 다음 실행부터 설정 창이 자동으로 열리지 않습니다.
- 다른 위치의 설정 파일을 사용해야 할 때만 <code>Change config file...</code>을 누릅니다.
- 설정 창을 닫거나 게임을 정상 종료하면 배속 값은 자동으로 **1x**로 돌아갑니다.
- 로비와 매칭 등 제외된 화면에서는 1x로 동작합니다.

설정 창은 처음 나타날 때만 게임 위로 올라오며, 이후에는 다른 일반 창처럼 뒤로
보내거나 최소화할 수 있습니다.

## v1.0.3 변경 사항

- 배속 선택과 자동 실행 설정을 클릭 즉시 저장하도록 변경
- Save 및 Reload 버튼을 제거하고 화면을 간소화
- 설정 파일 경로를 <code>Change config file...</code> 링크와 툴팁으로 정리
- 상태 문구를 <code>Now running at {N}x</code> 형식으로 통일
- 설정 창이 계속 최상단에 고정되던 문제 수정
- 100~200% 디스플레이 배율에 맞춘 고DPI 레이아웃 적용
- 긴 업데이트 안내가 잘리지 않도록 창 높이를 내용에 맞게 조정
- 설정 파일 교체 시 일시적인 파일 점유 충돌을 짧게 재시도

## 업데이트 확인

설정 창은 시작할 때 새 버전을 한 번 확인하며 새 버전이 있을 때만 안내와
<code>Download</code> 버튼을 표시합니다. 업데이트 파일을 자동으로 덮어쓰지는 않습니다.

업데이트 정보는 <code>distribution</code> 브랜치의
<a href="../../blob/distribution/release-index.json">release-index.json</a>을
<code>raw.githubusercontent.com</code>에서 읽습니다. <code>api.github.com</code>을 직접 사용하지 않으므로
미인증 GitHub API의 IP당 요청 제한에 영향을 받지 않습니다.

## 문제 해결

### 게임이 시작 직후 종료되는 경우

<code>BepInEx\config\BepInEx.cfg</code>의 <code>UnityLogListening</code>이 <code>false</code>인지 먼저 확인합니다.
그래도 실행되지 않으면 <code>BepInEx\plugins\AstralPartyAnimSpeed</code> 폴더를 잠시 다른 곳으로
옮긴 뒤 게임이 실행되는지 확인합니다.

### 설정 창이 나타나지 않는 경우

.NET Desktop Runtime 8.0 **Windows x64 Desktop Runtime**이 설치되어 있는지 확인합니다.
일반 .NET Runtime이나 ASP.NET Core Runtime과는 다른 항목입니다.

### 로그 확인

문제 제보 시 <code>BepInEx\LogOutput.log</code>를 함께 확인하면 원인을 찾는 데 도움이 됩니다.

## 제거

게임을 종료한 다음 아래 폴더를 삭제하면 됩니다.

~~~text
BepInEx\plugins\AstralPartyAnimSpeed\
~~~

## 라이선스

[MIT License](LICENSE)
