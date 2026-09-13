# BREAK NORTH — Final Asset Backup

최종 에셋과 새 제작 인스턴스를 위한 인계 자료 백업입니다. 백업 기준: 2026-09-13, M7 Priority A 납품 이후.

## 다운로드

에셋 ZIP은 [최종 에셋 백업 Release](https://github.com/svermy33-ops/proCRartist/releases/tag/break-north-assets-m7-a-2026-09-13)의 Assets에서 받습니다.

| 파일 | 내용 |
|---|---|
| `BREAK_NORTH_M6_v4.zip` | 기존 31종 키트. 도구·파편·부유 플랫폼 등을 포함하며 M7와 함께 보존해야 합니다. |
| `BREAK_NORTH_M7_A.zip` | M7 우선순위 A 공용 모델 40종, 재질·색상·표시 프리셋, 비교 장면, Unity 생성 스크립트, 검사 자료. |
| `BREAK_NORTH_ARTIST_HANDOFF.md` | 최신 제작 규칙, 쿼드·접촉 검사, 배색·재질, M6/M7 기술 계약, 새 인스턴스용 시작 문구. |
| `SHA256SUMS.txt` | 위 3개 원본 파일의 SHA-256 체크섬. |

인계 문서는 저장소의 [BREAK_NORTH_ARTIST_HANDOFF.md](BREAK_NORTH_ARTIST_HANDOFF.md)에서도 읽을 수 있습니다.

## 복원과 이어서 작업하기

1. Release에서 ZIP 두 개와 인계 문서를 내려받습니다. Git clone이나 GitHub의 Download ZIP만으로는 Release 첨부파일이 포함되지 않습니다.
2. `SHA256SUMS.txt`와 다운로드 파일의 SHA-256을 비교합니다. PowerShell에서는 `Get-FileHash -Algorithm SHA256 -LiteralPath <파일경로>`를 사용할 수 있습니다.
3. 새 제작 인스턴스에 인계 문서와 필요한 ZIP을 함께 전달합니다.
4. M6는 `Assets/BREAK_NORTH_FinalKit`, M7는 `Assets/BREAK_NORTH_M7`로 구분됩니다. 기존 Unity `.meta`/GUID를 보존하여 병합합니다.
5. 각 패키지 README, manifest, 재질·UV 계약을 읽습니다. M6의 atlas 범위를 M7 모델에 적용하지 않습니다.

M7는 M6 전체를 대체하는 키트가 아닙니다. 색상 변형은 공용 메시를 재사용합니다. 231개 기본 프리셋에서 조명색·표지 내용을 조합하면 제공 메뉴가 343개 Unity 프리팹을 생성하도록 구성되어 있습니다.

## 검증 범위

Blender/FBX의 쿼드, UV, 노멀, 치수 및 주요 부착 디테일을 검사했습니다. 실제 Unity C# 컴파일·메뉴 실행·게임 화면 외형 검증은 수행하지 않았습니다. 메뉴 코드 제공과 실제 프리팹/장면 생성 실행을 구분해야 합니다.

미리보기 렌더 이미지는 별도 요청 전까지 생성하지 않는 제작 원칙을 유지합니다. 게임 기능·파괴 로직·상호작용은 모델 납품과 별도입니다.
