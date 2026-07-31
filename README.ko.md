<div align="center">

# Prettifer

**골라낸 커밋만 반영된 결과를 하나의 diff로 검토합니다.**

[![Latest release](https://img.shields.io/github/v/release/jjj5306/prettifer-release?label=release&color=8f80fa)](https://github.com/jjj5306/prettifer-release/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/jjj5306/prettifer-release/total?color=5bb98c)](https://github.com/jjj5306/prettifer-release/releases)
[![Platform](https://img.shields.io/badge/platform-Windows%20x64-0078d4)](https://github.com/jjj5306/prettifer-release/releases/latest)
[![Issues](https://img.shields.io/github/issues/jjj5306/prettifer-release?color=f9bc45)](https://github.com/jjj5306/prettifer-release/issues)

[English](README.md) · [한국어](README.ko.md)

[다운로드](#설치) · [사용법](#사용법) · [동작 원리](#동작-원리) · [문제 해결](#문제-해결) · [버그 신고](https://github.com/jjj5306/prettifer-release/issues/new/choose)

</div>

---

## 무엇을 하는 도구인가

브랜치에 커밋이 20개 쌓였는데 그중 3개만 검토해야 할 때, Prettifer는 그 3개의
변경만 반영된 최종 파일 상태와 통합 diff를 만들어 보여줍니다. 원본 저장소는
건드리지 않습니다.

|  | 방법 | 문제 |
|---|---|---|
| ❌ | 커밋을 하나씩 본다 | 같은 파일을 여러 번 고친 경우 최종 모습을 알 수 없다 |
| ❌ | 브랜치 전체 diff를 본다 | 검토 대상이 아닌 커밋의 변경까지 섞인다 |
| ✅ | **Prettifer** | 원하는 커밋만 골라 그 결과만 본다 |

![통합 diff를 검토하는 Prettifer](docs/screenshot-tree-view.png)

## 설치

**요구 사항**

- Windows x64
- `PATH`에서 실행 가능한 Git `2.30+`

```powershell
git --version
```

**설치 순서**

1. [Releases](https://github.com/jjj5306/prettifer-release/releases/latest)에서 최신 Windows ZIP을 내려받습니다.
2. 원하는 위치에 압축을 풉니다.
3. `prettifer.exe`를 실행합니다.

설치 프로그램과 코드 서명은 아직 제공하지 않아 첫 실행 시 Windows SmartScreen
안내가 나타날 수 있습니다. ZIP과 함께 게시된 `SHA256SUMS.txt`로 내려받은 파일을
검증할 수 있습니다.

```powershell
Get-FileHash .\prettifer-win32-x64-<version>.zip -Algorithm SHA256
```

## 사용법

1. **Open Repository** — 검토할 로컬 Git 저장소를 엽니다. 저장소를 열어둔 상태로
   시작할 수도 있습니다: `prettifer.exe C:\work\repo`.
2. **비교 범위 정하기** — `Base branch`와 `Working branch`를 고르고
   `Load Commit Range`를 실행합니다.
3. **커밋 고르기** — 합성할 커밋의 체크 상자를 선택합니다. 카드 본문을 누르면
   선택을 유지한 채 해당 커밋을 살펴볼 수 있습니다.
4. **Build Selected Result** — 계산을 실행합니다. `Cancel`로 중단할 수 있습니다.
5. **검토** — `Changed Files`에서 파일을 고르고 기준 내용과 선택 결과를
   비교합니다.

Commit History는 왼쪽이 가장 오래된 커밋, 오른쪽이 가장 최신 커밋입니다.

> [!IMPORTANT]
> **Base에는 작업 브랜치가 실제로 갈라져 나온 브랜치를 고르세요.** 작업
> 브랜치가 `release/2026.6`에서 갈라졌는데 Base를 `master`로 두면, 두 브랜치가
> 갈라진 뒤 `release/2026.6`에 쌓인 커밋까지 모두 표시됩니다. Git 기준으로는
> 정상 동작이지만 의도한 범위가 아닐 수 있습니다.

## 주요 기능

| 기능 | 설명 |
|---|---|
| 비연속 커밋 선택 | 서로 떨어진 커밋을 여러 개 선택합니다 |
| 통합 결과 | 선택 커밋만 오래된 순서부터 적용한 최종 상태를 만듭니다 |
| merge commit | merge commit을 선택하고 어느 부모를 기준으로 비교할지 고릅니다 |
| 부분 결과 | 적용할 수 없는 파일만 문제로 표시하고, 나머지 파일은 그대로 검토합니다 |
| Tree / List 보기 | 변경 파일을 폴더 계층 또는 전체 경로 목록으로 봅니다 |
| 폴더 접기 | 폴더를 접고 펼치며, 하위 폴더가 하나뿐인 경로는 한 행으로 합칩니다 |
| Side-by-side Diff | 왼쪽이 기준, 오른쪽이 선택 결과입니다 |
| 추가된 파일 | 새 파일은 빈 기준 화면 없이 전체 내용을 추가 상태로 표시합니다 |
| 폭 조절 | 패널과 diff 내부 구분자를 마우스 또는 방향키·Home·End로 조절합니다 |
| 바이너리 파일 | 텍스트로 해석하지 않고 변경 상태만 안내합니다 |
| 명령행으로 열기 | `prettifer.exe <저장소 경로>`로 그 저장소를 열고 시작합니다 |
| 접근성 | 키보드 조작, 포커스 표시, 200% 확대와 고대비 모드를 지원합니다 |

<details>
<summary>List 보기 스크린샷</summary>

![Prettifer List 보기](docs/screenshot-list-view.png)

</details>

## 동작 원리

모든 요청은 원본 저장소와 분리된 임시 로컬 clone에서 실행됩니다.

```text
1. Base와 Working의 공통 조상을 비교 기준으로 결정
2. checkout하지 않은 격리된 임시 로컬 clone 생성
3. 파일 내용에 영향을 주는 안전한 Git 설정과 attributes 적용
4. 선택 커밋이 건드리는 경로만 준비
5. 저장소 전용 merge/filter 드라이버가 필요하면 전체 checkout으로 대체
6. 선택 커밋을 오래된 순서부터 적용
7. 기준 Git 객체와 최종 Git index에서 내용과 diff 수집
8. 성공·실패·취소 어느 경우든 해당 요청의 임시 디렉터리 정리
```

계산 중에는 임시 파일이 디스크에 만들어집니다. 정리에 실패하면 앱이 남은 임시
경로를 안내하므로, 해당 경로를 쓰는 프로그램을 종료한 뒤 직접 정리할 수 있습니다.

**원본 저장소에서 유지되는 것**: 현재 branch와 HEAD, staged·unstaged·untracked
파일, 로컬 Git config, 다른 Git worktree 등록.

## 제한 사항

| 항목 | 현재 동작 |
|---|---|
| 여러 브랜치에 흩어진 커밋 | 하나의 선형 이력 안에서 선택합니다 |
| 충돌 파일 | 문제로 표시하고 비교 기준 상태로 두므로 통합 diff에 충돌 표시가 섞이지 않습니다. 필요한 선행 커밋을 함께 선택하면 해소됩니다 |
| 변경 파일 그룹화 | 폴더 계층과 전체 경로 목록만 제공합니다 |
| 파일별 커밋 흐름 | 통합 결과 diff만 제공합니다 |
| 이름 변경 추론 | 이전 경로와 새 경로를 삭제·추가로 표시합니다 |
| 루트 커밋 비교 | 지원하지 않습니다 |
| macOS · Linux | Windows 배포본만 제공합니다 |
| 코드 서명 · 자동 업데이트 | 제공하지 않습니다 |

배포본에는 테스트나 자동화용 장치가 포함되지 않습니다. 프로젝트 자체 종단 테스트는
별도 진입점으로 실행되며, 그 진입점은 릴리스 패키징 과정에서 제거됩니다.

## 문제 해결

<details>
<summary><b>Git 실행 파일을 찾을 수 없음</b></summary>

```powershell
git --version
```

Git `2.30+`가 설치되어 있고 현재 사용자의 `PATH`에서 실행되는지 확인한 뒤 앱을
다시 실행합니다.

</details>

<details>
<summary><b>의도한 범위보다 커밋이 많음</b></summary>

Base 브랜치를 확인합니다. 분기 지점과 실제 범위는 다음으로 확인할 수 있습니다.

```powershell
git merge-base <base> <working>
git log --oneline --first-parent <base>..<working>
git rev-parse --abbrev-ref <working>@{upstream}
```

마지막 명령이 알려주는 브랜치가 대개 원하는 Base입니다.

</details>

<details>
<summary><b>선택한 변경을 적용할 수 없음</b></summary>

선택한 커밋이 고르지 않은 이전 커밋이 만든 파일이나 변경에 의존하는 경우입니다.
안내에 표시된 선행 커밋을 함께 선택한 뒤 다시 실행합니다.

</details>

<details>
<summary><b>잠금·권한·저장 공간 오류</b></summary>

저장소에서 실행 중인 다른 Git 작업을 종료하고, 접근 권한과 남은 저장 공간을
확인한 뒤 다시 실행합니다.

</details>

<details>
<summary><b>계산이나 정리가 오래 걸림</b></summary>

`Cancel`로 계산을 중단할 수 있습니다. 임시 경로 정리 오류가 표시되면 해당
경로를 쓰는 프로그램을 종료한 뒤 정리합니다.

</details>

## 버그 신고와 기능 요청

[이슈](https://github.com/jjj5306/prettifer-release/issues/new/choose)에서 양식을
사용해 주세요.

버그 신고에는 Prettifer 버전, Windows 버전, `git --version` 결과, 재현 순서
(어떤 Base/Working을 골랐고 커밋을 몇 개 선택했는지), 화면에 표시된 오류 문구가
있으면 원인을 훨씬 빨리 찾을 수 있습니다.

> [!CAUTION]
> 이 이슈 트래커는 공개되어 있습니다. 스크린샷과 오류 문구에서 저장소 경로,
> 브랜치명, 커밋 메시지와 소스 코드를 지운 뒤 올려 주세요.

## 라이선스

[Apache License 2.0](LICENSE) + [Commons Clause](https://commonsclause.com/) 조건.

| | |
|---|---|
| ✅ | 개인이든 회사 업무든 무료로 사용 |
| ✅ | 소스 열람·수정·재배포 |
| ✅ | 포크해서 Pull Request 기여 |
| ❌ | 판매, 또는 이 소프트웨어의 기능에서 가치가 나오는 제품·서비스로 대가를 받는 행위 |

Commons Clause는 **판매 권리만** 제거합니다. 특허 허여와 기여 조항을 포함한 Apache
2.0의 나머지 권리는 그대로 유지됩니다.

상업적 재판매를 제한하므로 Prettifer는 OSI 공인 오픈소스가 아니라
**source-available**입니다. "오픈소스"로 표현하지 말아 주세요. 서드파티 라이선스는
[NOTICE](NOTICE)를 참고하세요.
