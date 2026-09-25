# Astral Party 배속 모드

Astral Party에서 캐릭터와 각종 연출의 재생 속도를
<code>1x / 1.5x / 2x / 3x / 5x</code>로 조절하는 BepInEx 모드입니다.

배속은 사용자의 게임 화면 안에서만 적용됩니다. 연출뿐 아니라 이동과 화면 전환도
함께 빨라지고, 화면 하단의 턴 타이머는 배속과 무관하게 실제 시간으로 흘러갑니다.
서버에 전달되는 행동과 실제 턴 진행 시점은 바꾸지 않습니다.

> 이 저장소는 **배포 전용**입니다. 소스 코드는 포함되어 있지 않습니다.

## 하지 않는 것

- 게임과 서버 사이의 통신에 관여하지 않습니다. 플러그인에는 네트워크 코드가 없습니다.
- 게임 패킷을 읽거나 쓰지 않습니다.
- 키 입력을 자동화하거나 대신 눌러 주지 않습니다.
- 턴 타이머를 배속에 맞춰 바꾸지 않습니다. 타이머는 항상 실제 시간으로 흐릅니다.

## 사용 전 안내

설치 전에 [USER_AGREEMENT.txt](USER_AGREEMENT.txt)(사용 전 안내)를 확인해 주세요.
설치 절차는 [HOW_TO_INSTALL.txt](HOW_TO_INSTALL.txt)에 정리되어 있으며, 두 파일은
배포 zip의 `BepInEx\plugins\AstralPartyAnimSpeed\` 폴더에도 같은 내용으로 들어 있습니다.

## 다운로드

[![최신 릴리스 다운로드](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fraw.githubusercontent.com%2FYoungHoon02%2Fastral-party-speedup-release%2Fdistribution%2Frelease-index.json&query=%24.version&prefix=v&label=DOWNLOAD&color=7C3AED&logo=github&logoColor=white&style=for-the-badge&cacheSeconds=300)](../../releases/latest)

버튼의 버전은 `distribution/release-index.json`을 기준으로 자동 갱신됩니다.

최신 배포 파일의 SHA-256은 [업데이트 인덱스](../../blob/distribution/release-index.json)에서 확인할 수 있습니다.

## 준비물

- Windows x64 버전 Astral Party
- [BepInEx 6 Unity.IL2CPP-win-x64](https://builds.bepinex.dev)
- [.NET Desktop Runtime 8.0 x64](https://dotnet.microsoft.com/download/dotnet/8.0)

.NET Desktop Runtime은 게임과 별도로 실행되는 배속 설정 창에 필요합니다.

## 설치

### 1. BepInEx 설치

이미 BepInEx 6 IL2CPP가 설치되어 있다면 이 단계는 건너뛰어도 됩니다.

BepInEx는 모드마다 따로 설치하는 프로그램이 아닙니다. 다른 모드 때문에 이미 설치되어
있다면 다시 덮어쓰지 말고 아래의 `BepInEx\config\BepInEx.cfg` 설정과 모드 설치 단계만
확인해 주세요. 새로 설치할 때는 `Unity.IL2CPP-win-x64` 빌드를 선택하고, ZIP 안의
`BepInEx` 폴더가 게임 폴더 바로 아래에 오도록 압축을 풀어야 합니다. `BepInEx\BepInEx`
처럼 폴더가 중첩되면 모드가 인식되지 않습니다.

1. BepInEx 빌드 페이지에서 <code>Unity.IL2CPP-win-x64</code>로 시작하는 최신 zip을 받습니다.
2. zip의 내용을 <code>AstralParty_INT.exe</code>가 있는 게임 폴더에 풉니다. 게임 폴더 바로
   아래에 <code>BepInEx</code> 폴더가 생겨야 합니다.
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

1. 위의 다운로드 버튼에서 최신 버전의 <code>AstralPartyAnimSpeed-v*.zip</code>을 받습니다.
2. zip을 <code>AstralParty_INT.exe</code>가 있는 게임 폴더에 그대로 풉니다.
3. 덮어쓰기 여부를 물으면 허용합니다.
4. 게임을 실행합니다.

정상 설치되면 다음 폴더에 플러그인, 설정 앱, <code>USER_AGREEMENT.txt</code>,
<code>HOW_TO_INSTALL.txt</code>, <code>LICENSE</code>가 들어갑니다.

~~~text
BepInEx\plugins\AstralPartyAnimSpeed\
~~~

설정 파일 <code>config.json</code>은 게임을 처음 실행할 때 이 폴더에 자동으로 만들어집니다.
zip에는 설정 파일이 없으므로 업데이트해도 기존 설정이 그대로 유지됩니다.

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

## 최근 변경 사항 (v1.0.6)

- 선택한 배속이 표시된 값 그대로 적용되도록 바로잡았습니다. 이전 버전에서는 같은
  배속이 표시보다 더 빠르게 느껴질 수 있었습니다. 이전과 같은 체감을 원하면 한 단계
  높은 배속을 선택해 주세요.
- 설정 파일의 타이머 관련 고급 옵션을 정리했습니다. 턴 타이머는 항상 실제 시간으로
  흐르며, 기존 설정 파일은 그대로 사용할 수 있습니다.
- 게임 업데이트 후 모드가 정상인지 알 수 있도록, 시작할 때 상태를 로그에 한 줄 남깁니다.
- 라이선스 파일(<code>LICENSE</code>)을 설치 폴더에 함께 넣었습니다.

이전 버전의 변경 내용은 [Releases](../../releases)에서 확인할 수 있습니다.

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

### 게임 업데이트 후 배속이 적용되지 않는 경우

게임 업데이트로 내부 구조가 바뀌면 배속이 적용되지 않을 수 있습니다. 이때는
<code>BepInEx\LogOutput.log</code>에서 <code>[status]</code>로 시작하는 줄을 확인합니다.
<code>frame tick patch NOT installed</code>가 보이면 이 모드가 현재 게임 버전과 맞지
않는 것이므로 새 버전을 기다려 주세요. <code>timer patch NOT installed</code>가 보이면
배속은 적용되지만 턴 타이머가 배속대로 빨라질 수 있습니다.

### 로그 확인

문제 제보 시 <code>BepInEx\LogOutput.log</code>를 함께 확인하면 원인을 찾는 데 도움이 됩니다.

## 제거

게임을 종료한 다음 아래 폴더를 삭제하면 됩니다.

~~~text
BepInEx\plugins\AstralPartyAnimSpeed\
~~~

## 라이선스

[MIT License](LICENSE) — 이 저장소의 코드와 배포 파일에만 적용됩니다. 게임과 게임
자산에는 각 권리자의 조건이 적용됩니다.
