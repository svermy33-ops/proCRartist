# BREAK NORTH — 3D 에셋 제작 규칙 및 작업 인계서

**정리일: 2026-09-13 · 기준: M7 Priority A 납품 이후**

**추가 인계: 2026-09-14 · M6 Architecture v3 스타일 사용자 승인.** 기존 1~20절은 원문을 유지했다. 새 작업자는 **21~25절의 최신 추가 기준도 반드시 함께 읽는다.** 기존의 밝고 읽기 쉬운 산업 세계, 쿼드·모듈·재사용·검증 원칙을 유지하면서 이번에 승인된 재질과 디테일을 이어가는 보충 지침이다. 기존 절의 이전 작업 범위·파일 위치·승인 상태는 당시 기록이며, 현재 제작 결과는 24절을 참고한다.

이 문서는 이전 대화가 없는 새 Codex 인스턴스가 BREAK NORTH 에셋 제작을 이어가기 위한 독립적인 작업 기준이다. 사용자 요구, 이후 수정된 기준, 기존 에셋의 기술 계약, 검증 절차를 통합했다. 모델 파일 자체는 별도 납품 ZIP에 있다.

## 1. 처음 읽을 핵심

1. **밝고 읽기 쉬운 스타일라이즈드 산업 세계**를 만든다. 단순한 형상, 명확한 기능, 부드러운 shading, 작고 적절한 bevel이 기본이다.
2. **쿼드는 처음 모델링할 때부터 구성한다.** 마지막에 삼각형을 무작정 합쳐 쿼드로 바꾸는 방식은 피한다. `.blend`와 FBX에 쿼드를 유지하고 런타임 Tris는 별도로 보고한다.
3. 사용자는 **찰흙 같은 표면과 부족한 디테일**을 지적했다. 넓은 평면을 유지하고 재질별 반사·거칠기를 구분하며, 절제된 긁힘·도장 마모·입자감을 텍스처로 보완한다.
4. 구조물은 **한 Space 안에서 통일된 배색**을 사용한다. 같은 색 계열에서도 프레임·덮개·연결부의 명도와 채도를 나눈다. 도구는 서로 다른 고유 색을 사용한다.
5. **부품이 떨어지거나 장식이 묻히지 않게 한다.** 곡면 장식은 꼭짓점뿐 아니라 면 내부까지 검사한다. 표지의 위치·방향도 확인한다.
6. 실루엣과 기능을 훼손하면서 폴리곤 수를 줄이지 않는다. 최신 예산은 목표 범위이며, 초과가 필요하면 이유와 실측값을 기록한다.
7. 색만 다른 모델은 **같은 메시를 재사용**한다. 공용 재질·atlas·trim과 neutral base/tint 영역을 우선한다.
8. 벽의 파괴 cell은 논리 단위다. **파괴 그리드를 벽 디자인에 새기지 않는다.**
9. **새 미리보기 렌더 이미지는 사용자가 다시 요청하기 전까지 생성하지 않는다.** 편집 가능한 비교 장면은 제공할 수 있다.
10. Blender/FBX 검사와 Unity 실제 실행·외형 검증을 분리한다. 수행하지 않은 검증을 완료했다고 말하지 않는다.

## 2. 규칙의 우선순위와 현재 범위

- 이후 사용자가 새로 지시한 내용이 이 문서의 이전 요구보다 우선한다. 충돌이 없으면 기존 규칙을 계속 유지한다.
- 개발자 전달 문서는 기술 요구와 근거로 읽되, 첨부 문서의 모든 후보·향후 항목을 현재 제작 요청으로 확대하지 않는다.
- 최신 제작 규칙은 새 작업부터 적용한다. 새 규칙을 받았다는 이유만으로 승인된 기존 모델 전체를 재제작하거나 덮어쓰지 않는다.
- **현재까지 요청받은 M7 제작 범위는 Priority A이다.** B/C 제작은 후속 사용자 요청이 필요하다.
- 자잘한 구현 선택은 요구 범위 안에서 판단하여 진행한다. 이미 받은 허락을 반복해서 묻지 않는다. 다만 모델러 작업을 넘어 프로젝트 변경·배포 등으로 범위를 임의 확대하지 않는다.

### 이전 기준과 혼동하지 말아야 할 변경

| 항목 | 최신 해석 |
|---|---|
| 폴리곤 예산 | 최초의 더 좁은 표보다 이 문서의 최신 목표 범위를 우선한다. |
| 금속 구조물 배색 | 전부 같은 파랑 한 색이 아니다. 부품별 명도·채도 차이, M7 Space Theme별 색 변형을 허용한다. |
| 금속 벽 초기 색 | 사용자가 제시한 `333366`은 기존 초기 색 참고이며, 모든 M7 구조물을 이 색으로 고정하는 규칙이 아니다. |
| 표면 디테일 | 지나치게 단순하고 균일한 무광을 피한다. 과하지 않은 긁힘·마모와 약간 더 현실적인 재질감을 허용한다. |
| 재질 슬롯 | 최신 새 에셋은 가능하면 1~3개. M6의 기존 단일 슬롯 계약을 불필요하게 바꾸지 않는다. |
| Collider | 새 가구는 visual과 단순 collision을 분리한다. M6의 일부 비볼록 visual MeshCollider 구성을 새 가구의 기본으로 답습하지 않는다. |
| 소켓 | 기존 `HandleSocket`을 새 문서의 `GripSocket` 표현만 보고 조용히 변경하지 않는다. 역할 매핑과 호환성을 기록한다. |
| 구버전 정리 | 실제로 대체되어 쓰지 않는 배포본만 보관함으로 이동한다. M7에 없는 도구 등을 가진 M6는 여전히 필요한 키트다. |

## 3. 아트 방향과 감정

핵심 문장:

> 밝고 읽기 쉬운 스타일라이즈드 산업 세계.
>
> 낮은 polygon 자체가 목적이 아니다. 단순한 geometry와 smooth shading으로 강한 형태를 만든다.
>
> 환경은 공간을 만들고, 도구는 행동을 보여주며, 재질은 기능을 설명한다.

기본 구성은 **Simple Geometry + Smooth Shading + Clear Silhouette + Moderate Bevel + Stylized PBR**이다.

형태는 Rounded / Chunky / Functional / Slightly Angular를 지향한다. 건축물은 큰 직선·직각·넓은 평면·반복 가능한 모듈로 구성한다. 도구와 기계는 모터, 실린더, 손잡이, 밸브, 파이프, 날, 탱크 같은 기능 부품으로 리듬을 만든다.

플레이어가 느낄 감정은 Curiosity, Discovery, Scale, Improvisation, Ownership, Adventure이다. 버려졌지만 탐험하고 싶은 거대한 인공 세계를 목표로 한다.

피해야 할 방향:

- 삼각형 면이 드러나는 flat-shaded low-poly, PS1 스타일.
- 극단적으로 적은 폴리곤을 의도적으로 노출한 실루엣.
- 모든 모서리가 날카로운 사실적 하드서피스 또는 장난감처럼 과도한 둥글림.
- Horror Backrooms, grimdark, 폐병원 분위기, 지속적으로 어두운 공간.
- 녹·오염·피·고주파 노이즈가 화면을 지배하는 표현.
- 환경 소품을 전부 hero prop 수준으로 과밀하게 만드는 것.

## 4. 색채와 기능색

### 기본 환경

밝은 회색, 청회색, 옅은 베이지, 스틸 그레이, 밝은 콘크리트를 사용한다. **철은 푸르스름하게, 콘크리트는 베이지 중심**, 채도는 파스텔보다 살짝 높은 정도가 기본 출발점이다. 과도하게 번쩍이는 금속 느낌은 피한다.

한 구조물에서도 프레임은 조금 어둡게, 덮개는 밝게, 연결부는 다른 청회색 명도로 나누어 읽히게 할 수 있다. 대비가 기능이나 조립 구조를 설명하도록 한다.

### 도구

도구들이 모두 환경의 청회색을 공유하면 안 된다. 서로 구분되는 hue를 사용하면서 채도·명암·재질 반응은 같은 세계에 맞춘다. 기존 승인 예시는 검은 헤드/나무 손잡이의 망치, 황토·모래·차콜·테라코타의 드릴, 적갈·붉은 회색·차콜의 절단기이다. 후속 변형에서도 서로의 식별성을 유지한다.

### 기능색

| 기능 | 기본 방향 |
|---|---|
| Electric | Blue / Cyan |
| Oil / Fuel | Orange / Dark Yellow |
| Gas | Yellow |
| Chemical | Green / Lime |
| Danger | Red |
| Traversal / Utility | Orange / Yellow |

색은 장식보다 기능 전달에 쓴다. M7 파이프의 Blue=water/cooling, Yellow=gas, Orange=fuel, Green=chemical은 **테스트용 매핑**이며 최종 게임 규칙으로 확정했다고 말하지 않는다.

### M7 Space Theme

벽마다 무작위 색을 섞지 않는다. 한 Space는 기본적으로 하나의 Primary Wall Color를 가진다. 동일 모델의 cream, blue, green, yellow, gray, orange 변형은 허용되며, 이를 같은 Space 안에 모두 섞으라는 의미가 아니다.

| 비교 Space | 벽 | 바닥/트림 | Accent / 분위기 |
|---|---|---|---|
| Storage Concrete | Beige Concrete | Gray Concrete / Dark Steel | Yellow, gray/orange shelf |
| Storage Metal | Cream Painted Metal | Gray / Steel | Blue, blue/gray furniture |
| Electric Utility | Pale Blue Gray Metal | Dark Gray / White·Steel | Cyan·Blue, neutral industrial room |
| Oil Utility | Warm Gray·Beige | Dark Steel / Black | Orange·Yellow |
| Transit | Cool Gray | Dark Gray / Steel | Blue·Yellow, 방향성 |
| Settlement | Warm Concrete·Cream | Neutral / Gray | Warm Orange, 향후 Wood·Fabric |

Electric은 파란 네온 방이 아니라 중성 산업 공간에 전기 기능색이 더해진 모습이다. 같은 geometry·배치에 material/color/light만 바꿔 Space 차이를 비교한다.

## 5. 찰흙 느낌을 줄이는 재질 제작

- 모든 재질에 같은 roughness와 균일한 무광 반응을 쓰지 않는다.
- Painted Metal과 Bare Metal을 구분한다. 도장은 낮은 metallic/중간 roughness, 노출 철은 더 금속적인 반응을 사용한다.
- Plastic은 금속보다 부드러운 반사, Rubber는 어둡고 높은 roughness로 구분한다.
- Concrete는 옅은 입자·저대비 얼룩, Wood는 단순한 결, Fabric은 큰 색면과 약한 조직을 사용한다.
- Glass는 읽기 쉬운 투명도를 우선하며 과한 굴절을 피한다.
- 짧고 드문 긁힘, 국소 도장 마모, 약한 먼지·오일·녹은 허용한다. 반복 모듈마다 같은 큰 흠집이 눈에 띄지 않게 한다.
- 작은 표면 자국은 BaseColor/Roughness/Normal로 표현한다. 모든 볼트·스크래치·미세 패널선을 geometry로 만들지 않는다.
- 넓은 평면은 평평하게 읽혀야 한다. 판이 부풀거나 녹아내린 것처럼 보이면 bevel 크기와 normals부터 점검한다.
- 더 현실적인 표현을 전체 고광택·고 metallic 또는 포토리얼 오염으로 잘못 해석하지 않는다.

## 6. 모델링·쿼드·shading

### 반드시 지킬 것

- 쿼드 topology를 제작 중 구성한다. 실루엣을 읽기 쉽게 유지한다.
- Blender 원본과 조립 FBX는 all-quad를 유지한다. Unity 렌더링의 삼각형 변환은 별도 단계다.
- 주요 hard-surface 모서리에 작은 bevel을 둔다. 환경은 얇게, 가까이 보는 도구·가구는 조금 더 강조할 수 있다.
- 기본 Smooth Shading을 사용하고 필요한 hard edge만 분리한다. 평면이 휘어 보이지 않게 weighted/custom normals를 확인한다.
- 작은 Pipe는 8~12각, 큰 Pipe/Cylinder는 12~16각이 기준이다. 가까이 보는 도구 원통은 필요하면 더 세분화한다.
- 주요 형상·모터·손잡이·프레임·하우징·날은 geometry로 읽히게 만든다.
- 편집 가능한 부품 이름과 구조를 보존한다. 런타임 조립 메시를 합치는 것과 기능 부품 구분을 없애는 것은 다르다.

### 깨끗한 쿼드 검사

각 quad를 같은 기준의 두 triangle로 나눠 다음을 검사한다.

1. 꼭짓점 중복·길이 0인 edge·면적 0인 face/triangle이 없는가.
2. 두 triangle의 normal 방향이 반대가 되거나 bow-tie처럼 꼬이지 않았는가.
3. 지나치게 비틀린 비평면 quad가 shading 오류를 만들지 않는가.
4. 닫혀야 하는 부품의 열린 경계·non-manifold edge·뒤집힌 표면이 없는가.
5. 동일 위치 중복 면과 실제 부품 접촉면을 구분했는가.
6. UV0와 UV1에 NaN/Inf·면적 0인 UV face가 없는가.

`len(face.vertices)==4`만으로 쿼드가 깨끗하다고 판정하지 않는다. 동일 방향 중복 표면, 반대 방향의 내부 접촉면, 의도적인 단면 overlay는 각각 구분한다.

## 7. 부착 디테일의 정렬과 접촉

과거 반복된 오류는 드릴 손잡이 커버·장식 어긋남, 도구의 떨어진 부품, 곡면에 묻히거나 떠 있는 표시류, 전기 표지 위치 불일치였다. 이후 제작에서도 우선 검사한다.

- grip/cover/battery와 회전축의 정렬을 확인한다.
- 장식의 뒤쪽은 지지 표면 안으로 조금 맞물리고, 바깥 면은 의도한 만큼 드러나게 한다.
- **Bounding box 겹침과 꼭짓점 검사만으로 접촉을 증명하지 않는다.**
- 곡면 장식은 실제 지지 메시와 면 내부 샘플을 비교한다. 원통이 low-poly이면 이상적인 매끈한 원이 아니라 실제 각진 단면을 기준으로 한다.
- 나선·튜브는 단면 frame의 회전이 연속인지 확인한다. 갑자기 뒤집힌 단면은 쿼드를 꼬이게 한다.
- 기능적인 움직임 간극과 단순한 잘못된 틈을 구분한다. 모든 부품을 억지로 겹치게 만들지는 않는다.
- 표지는 장착 면 안에 들어가는지, 기호가 정방향인지, 화살표 방향·좌우 반전·UV 회전이 맞는지 확인한다.

기존 검사 사례는 방법 참고이지 모든 신규 에셋의 고정 수치가 아니다.

| 사례 | 확인된 설계/검사 기준 |
|---|---|
| M6 부유 플랫폼 | 판과 하부 프레임 약 5mm 맞물림 |
| M7 펌프 냉각부 | 같은 16각 단면, 내부 반경 0.152m / 본체 0.155m / 외부 0.163m; 면 내부 노출 검사 |
| M7 표지 글자판 | 뒤쪽 0.3mm 맞물림, 앞쪽 0.7mm 돌출, +X→+U / +Z→+V 확인 |
| M7 크레이트 grip | 옆 벽 표면 안팎에 걸쳐 배치, 약 2mm 맞물림 |

## 8. 단위·축·피벗

`1 Unity Unit = 1 metre`, Unity는 Y Up이다. 실제 크기를 현실적인 범위로 만들고 export 전 Apply Scale/Rotation을 확인한다. Unity 기본 Transform Scale은 `(1,1,1)`을 목표로 한다.

기존 Blender export는 **-Z Forward / Y Up**이다. Blender 내부는 Z Up, 벽·가구의 주요 정면은 보통 -Y다. 이 설정을 프로젝트 전체에서 일관되게 사용한다. 서로 다른 프로그램의 좌표·handedness 변환을 추측만으로 처리하지 말고 export/reimport와 실제 Unity 기준으로 확인한다.

| 용도 | 새 에셋 피벗 기준 |
|---|---|
| 선반·테이블·캐비닛·상자 | 바닥 접촉면 중앙 |
| 벽 부착 패널/장치/표지 | 벽 접촉면 중앙 |
| 천장 부착 조명/표지 | 천장 접촉면 중앙 |
| 천장 모듈 | 정해진 천장 접촉/모듈 원점, 문서에 명시 |
| 바닥·부유 플랫폼 | 보행면 중앙 |
| 파이프·연결 모듈 | 가능하면 연결 끝점, 또는 정해진 modular origin |
| 도구 | 실제 손 grip 기준으로 작업하기 쉬운 위치 |
| 빔 등 | 명시된 modular origin |

기존 파일의 피벗을 바꾸면 기존 배치와 anchor가 달라진다. 조용히 변경하지 말고 이전/새 위치와 영향, 새 key 여부를 기록한다.

## 9. 최신 Runtime Tris 목표

| 종류 | 목표 Tris |
|---|---:|
| Wall | 50~300 |
| Floor / Ceiling | 20~200 |
| Column / Beam | 100~500 |
| Door / Hatch Frame | 300~1,000 |
| Shelf | 600~1,500 |
| Table / Workbench | 400~1,000 |
| Cabinet / Locker | 500~1,500 |
| Box | 100~500 |
| Electrical Panel | 400~1,200 |
| Ceiling Light | 200~700 |
| Pipe | 100~500 |
| Vent / Cable Tray | 200~800 |
| Hammer | 1,000~2,500 |
| Drill / Cutter | 2,000~4,500 |
| 향후 Hero Tool | 필요 시 5,000~8,000 |
| Concrete / Metal debris | 각 20~100, 기존 3종씩 기준 유지 |

난간·플랫폼·펌프·탱크 등 별도 최신 범위가 지정되지 않은 항목에 보편적인 예산을 임의로 확정하지 않는다. 해당 작업에서 잡은 목표와 실제 수치를 기록한다. 초과가 필요하면 실루엣/기능상의 이유를 설명한다.

## 10. 개별 에셋에서 유지할 의미

- **벽:** 기본 요구는 가로로 긴 2:1 직사각형이다. 기존 대표 모듈은 5m×2.5m, 약 0.2m 두께이다. 모든 후속 벽을 무조건 이 크기로 만들라는 뜻은 아니며 모듈과 용도를 함께 고려한다.
- **바닥/천장:** 정사각형 모듈. 기존 대표는 2.5m×2.5m이다.
- **플랫폼:** 탁자나 네 다리 가구가 아니라 **공중에 떠 있는 보행용 발판**이다. 얇은 보행판과 필요한 하부 보강만 둔다. M6 수정본은 1.5m 정사각형, 전체 두께 0.155m, 220 Tris, 보행면 중앙 원점이다. 공중 고정/이동 기능은 게임 로직이다.
- **망치:** 일반 공구처럼 단순하고 실용적인 망치. 검정/차콜 계열 헤드, 명확한 grip, 앞쪽에 무게가 느껴지는 실루엣. 복잡한 장식으로 만들지 않는다.
- **드릴:** 실제 드릴 복제보다 조금 더 카툰스러운 디자인. 모터 하우징·회전축·grip·전원부를 읽을 수 있어야 하며 커버·배터리·장식 정렬을 특히 확인한다.
- **절단기:** 날, guard, grip, motor와 연결축이 읽혀야 한다. 날과 하우징이 떠 있거나 보호 덮개가 지지 없이 떨어져 있으면 안 된다.
- **종이 상자:** 택배용 종이 박스, 테이프 흔적과 라벨 방향을 표현한다. 플라스틱/금속 상자 변형은 별도 재질·형태로 구분한다.
- **금속 벽:** 테두리·도장 면·금속 부품 등으로 재질 특성을 전달한다. 승인된 모서리 나사처럼 중요한 디테일을 무조건 텍스처로 없애지 않는다.
- **천장 조명:** 약간 둥근 형태를 허용한다. Housing, diffuser, mounting 관계가 읽혀야 한다.
- **가구:** 선반·로커·작업대·패널·상자의 기능적 실루엣을 우선한다. 지나치게 복잡한 장식을 붙이지 않는다.

## 11. Cell, 모듈, 파괴

- 논리 Cell은 `10m × 5m × 10m`인 generation unit이다. visual room module이 아니다.
- 1m, 2m, 2.5m, 5m 같은 모듈을 조합할 수 있다. 여러 Cell의 Polycube Space가 하나의 연속 공간으로 읽혀야 한다.
- 벽에 2m/2.5m 파괴 패널선을 규칙적으로 새겨 Cell 또는 destruction grid를 노출하지 않는다. 기능상 필요한 frame/trim과 파괴 그리드 강조는 다르다.
- 기존 벽 파괴 검토안은 10m×5m 면의 5×2 segments, 바닥/천장은 10m×10m 면의 4×4 segments였다. **이 숫자는 texture 반복 주기가 아니다.** 최신 게임 구현은 개발 문서에서 다시 확인한다.
- 상태는 Intact / Damaged / Broken Segment / Opening을 geometry/decal로 설명한다. 완전 voxel 파괴나 고밀도 금속 변형 simulation을 전제로 만들지 않는다.
- 물리 boundary는 Face A / Face B / Cut Surface를 독립적으로 사용할 수 있다. 앞뒤가 반드시 같은 재질일 필요는 없다.
- Wall FBX는 style/frame/border/trim/material reference로 사용할 수 있다. 모든 벽을 arbitrary runtime boolean용으로 만드는 것은 요구가 아니다.
- Concrete 단면은 rough/broad/chunky, Metal 단면은 angular/sharp/torn/cut로 읽히게 한다. 콘크리트 파편은 큰 덩어리 위주다.

## 12. 재질·텍스처·UV 공통 규칙

### 재사용

Material Family는 Concrete, PaintedConcrete, PaintedMetal, BareMetal, Plastic, Rubber, Wood, Fabric, Glass를 기본으로 한다. 불필요한 bespoke shader를 늘리지 않는다. 가구는 shared atlas/trim, 색 변형은 neutral base+tint 영역을 우선한다.

재질 슬롯은 가능하면 1~3개, 기능상 필요한 도구 등은 예외를 설명할 수 있다. 같은 mesh에서 색만 다른 경우 별도 FBX를 만들지 않는다. 실루엣이 의미 있게 달라질 때 geometry variant를 만든다.

| 용도 | 텍스처 목표 |
|---|---|
| 환경 shared texture | 1K~2K |
| Trim sheet | 2K |
| Furniture | shared atlas/trim 우선, 필요 시 1K |
| Tool | 1K |
| Hero Tool | 필요 시 2K |
| 작은 item | 256~512 |

4K는 특별한 이유 없이 사용하지 않는다.

### 채널과 UV

- UV0=재질, UV1=별도 lightmap. 실제 Blender layer 이름과 Unity channel을 문서화한다.
- 타일 표면은 실제 metre/UV주기와 offset 규칙을 기록한다. 세그먼트마다 UV를 리셋해 늘림/밀도 변화를 만들지 않는다.
- Atlas의 bounds 사각형을 실제 island 모양으로 착각하지 않는다. 회전/반전/비사각 island는 코너 UV 자료로 전달한다.
- 재질 offset/tiling을 임의 변경해 잘못된 매핑을 감추지 않는다. atlas는 기본 offset `(0,0)`, tiling `(1,1)`이다. 표지 cell 선택 등 명시된 변환은 예외다.
- BaseColor/Emission은 sRGB. Normal/MetallicSmoothness/TintMask는 linear data이다.
- MetallicSmoothness의 R=metallic, A=smoothness. Normal은 Blender/OpenGL +Y tangent-space이며 Unity NormalMap import를 기본으로 한다. 실제 tangent/handedness 문제를 확인하지 않고 green을 임의 반전하지 않는다.
- Emission map은 실제 Light가 아니다. 조명 모델·발광 재질·Light 컴포넌트를 구분한다.
- Padding과 mip 색 번짐, normal seam, 투영 방향을 점검한다. 채널 존재만으로 lightmap bake 품질이 검증된 것은 아니다.

## 13. M6와 M7 기술 계약을 섞지 말 것

| 항목 | M6 v4 | M7 A |
|---|---|---|
| Unity 경로 | `Assets/BREAK_NORTH_FinalKit` | `Assets/BREAK_NORTH_M7` |
| 기본 방식 | 기존 유색 atlas 및 전용 도구 atlas | neutral/tint 영역, 공용 family와 atlas |
| Normal strength | ConcreteWall .45 / Industrial .22 / 기타 .3 | Concrete 계열 .35 / 기타 .24 |
| Tangent | FBX에 없으며 importer가 Mikk 계산 | FBX에도 포함, importer는 Mikk 재계산 설정 |
| Collider | 일부 정적 구조물 비볼록 MeshCollider | 별도 단순 box proxy FBX → BoxCollider |
| 역할 | 기존 전체 키트·도구 등 | Priority A 테마/재질 변형 키트 |

새 코드가 기존 atlas/normal 강도/pivot을 전역 교체하면 안 된다. 해당 버전의 manifest와 계약을 읽는다.

### M6에서 개발자와 구분한 문제

개발자 전달에 따르면 생성 벽·바닥·천장이 세그먼트마다 임의 UV를 쓰고 tangent를 누락한 것이 주요 원인이었다. 원본 손상이나 texture GUID 연결 오류가 확인된 상황은 아니었다.

따라서 Unity 생성 UV를 보상하려고 원본 atlas를 재배치하지 않았다. 모델러는 실제 UV 영역·물리 주기·geometry detail을 전달하고, 개발자는 생성 메시 UV/tangent와 조명·override를 수정한다. 기능 테스트 통과는 외형 승인 근거를 대신하지 않는다.

### M7 PaintedMetalAtlas

4×4 atlas이며 TintMask R=Primary, G=Secondary, B=Fixed이다.

- Primary: zone 0/4/10/12.
- Secondary: zone 1/6.
- Fixed: zone 2/3/5/7/8/9/11/13/14/15.
- 새 매핑은 cell 경계에서 0.018UV, 1024² 기준 약18.4px 안쪽을 기준으로 한다. 실제 값은 측정 자료를 우선한다.
- 기본 Standard/URP Lit 구현은 역할을 **면별 재질 슬롯**으로 나누어 tint한다. 기본 shader가 TintMask를 자동 소비하는 것은 아니다.
- Fixed의 고무·나사·기능 표시까지 전체 tint로 물들이지 않는다. Steel 변형은 주/보조 부위를 BareMetal로 전환하고 Fixed는 유지한다.
- M6 atlas 사각 영역을 M7 모델에 적용하지 않는다.

### 기존 표면 주기와 참조 자료

M7 `WallConcrete` 주 평면은 `U=(X+2.5)/2, V=Z/2`, 2m/UV주기이다. 5×2.5m 모듈에 2.5×1.25주기가 들어간다. M7 주요 Floor 평면은 `U=(X+1.25)/2.5, V=(Y+1.25)/2.5`, 2.5m/UV주기이다. 위 식의 좌표는 **Blender local XYZ**이다.

M7 `CeilingConcrete`는 smart-project 참고 슬래브이며 이 모델 UV에 독립적인 월드 반복 주기를 지정하지 않았다. 생성 천장에 연속성을 적용할 때는 별도 물리 기준 planar UV를 사용한다. 금속 벽/패널/천장 atlas에 단일 물리 주기가 있다고 가정하지 않는다.

정확한 자료는 M7 `Reports/Surface_UV_Spec.csv`, `Reports/Surface_UV_Corners.json`, `Reports/Atlas_Contract.json`, `MATERIAL_UV_CONTRACT.md`에 있다. M6에는 별도의 `SURFACE_UV_SPEC.csv`, `SURFACE_UV_CORNERS.json`, `SURFACE_UV_GUIDE.md`가 있다. 면 번호는 Blender 측 기준이며 Unity 최적화 후 인덱스와 같다고 가정하지 않는다.

## 14. 상호작용·소켓·충돌체

게임 규모의 독립된 물체처럼 보이는 사물은 가능하면 Destructible / Salvageable / Movable / Container / Usable 중 하나의 의미를 갖도록 설계한다. 다만 모델링만 했을 때 해당 게임 기능까지 구현했다고 주장하지 않는다.

먼지·녹·페인트·스티커·경고표시는 decal/texture/normal 등으로 표현하고, 아무 기능도 없는 독립 장식을 과도하게 만들지 않는다.

도구는 Body / Head / Grip / Power가 시각적으로 구분되되 물리적으로 연결되어야 한다. 기존 소켓은 `HeadSocket`, `HandleSocket`, `PowerSocket`, `UtilitySocket`, `SideSocket`이다. 후속 규칙의 `GripSocket`과 기존 `HandleSocket`은 역할을 명시적으로 매핑한다. Unity의 별도 `GripPoint`/gameplay anchor는 원본 소켓과 구분한다.

가구는 `Support_FL`, `Support_FR`, `Support_BL`, `Support_BR`, 벽 장치는 `WallSupport`, 천장 장치는 `CeilingSupport`를 논리적으로 배치할 수 있어야 한다. 이 점들을 FBX에 반드시 넣어야 한다는 요구는 아니다.

Visual mesh와 collision은 분리한다. simple/compound collision을 사용하며 UCX 이름만으로 Unity에 자동 collider가 만들어진다고 말하지 않는다. 문틀·선반·계단 등의 빈 공간을 거대한 하나의 collider로 무조건 막지 않는다. 곡면의 단순 박스 근사나 파이프 내부 미재현 같은 한계는 기록한다.

Basic 도구도 일부러 약해 보이게 만들지 않는다. Basic은 practical/exposed functional parts, Advanced는 integrated/protected/efficient-looking으로 구분한다. 티어가 높다는 이유만으로 크기와 발광만 늘리지 않는다.

## 15. 재현 가능한 제작 순서

### 시작

1. 새 요청과 이 문서를 읽고 범위를 정한다. 전체 후보 목록과 현재 우선순위를 구분한다.
2. 실제 파일/ZIP/manifest를 확인한다. 이전 답변에 폴더가 있다고 적혀 있어도 현재 존재한다고 단정하지 않는다.
3. 사용할 원본·버전·key·치수·피벗·재질 계약을 확인한다. 필요한 ZIP은 `work/`의 작업 사본으로 푼다.
4. 기존 승인 파일은 보존하고 새 작업 버전/namespace를 정한다. 색만 다른 모델을 복제하지 않는다.

### 모델링·재질

5. 기능과 silhouette을 먼저 잡고 quad topology를 구성한다.
6. 적절한 bevel과 smooth/custom normals를 적용한다. 큰 평면이 부풀지 않는지 확인한다.
7. 주 부품, grip, 회전축, frame과 장식의 장착 관계를 점검한다.
8. UV0/UV1, 공용 재질, tint 역할을 만든다. subtle surface detail은 texture/normal에 배분한다.
9. 기능색·도구 간 색 구분·Space Theme 통일성·반복 패턴을 비교한다.

### 검사·납품

10. 원본에서 쿼드/UV/경계/정렬/접촉/피벗을 검사한다. 미해결 항목이 있으면 원인을 수정한다.
11. `.blend`의 필요한 텍스처를 pack하고 편집 가능한 부품을 보존한다. 조립 FBX를 export한다.
12. **export한 FBX를 다시 import**하여 원본과 치수·원점·방향·면 수·UV·재질·normals/tangents·소켓을 비교한다.
13. 필요하면 벽·가구·도구를 같이 둔 비교 장면을 구성한다. M7는 색 보드와 같은 geometry의 6개 Space 비교를 사용한다. 새 렌더 이미지는 별도 요청이 있을 때만 만든다.
14. manifest, 재질/UV 계약, 변경 내역, 검사 결과, 미검증 사항을 기록한다.
15. ZIP 내부 파일/CRC/개수/참조를 확인하고 링크를 제공한다. 실제 안 쓴 구버전은 검증 후 보관함으로 이동한다.

### 구현 시 주의

Blender Python 자동화는 사용할 수 있다. 생성 스크립트도 실제 결과 검사를 대체하지 않는다. 기존 helper는 참고하되 dimension, bevel 반경, 연결부, UV, 상수, 경로를 그대로 믿고 재사용하지 않는다.

이 작업 환경에서는 Blender Python 예외가 로그에 기록되면서 프로세스 exit code가 0인 경우가 있었다. 종료 코드만 보지 말고 `Traceback`, assertion과 명시적인 완료 표시를 확인한다. 이미지 cache 경로 오류와 실제 모델/텍스처 저장 실패도 구분한다.

## 16. 최소 검증 기록

에셋별로 다음을 남긴다.

| 분야 | 기록 |
|---|---|
| 식별 | key, 원본 참조/버전, 파일명 |
| 형상 | quads, runtime tris, 목표 예산, 실측 크기 |
| 변환 | metre 단위, pivot 의미, 적용 scale/rotation, export 축 |
| Topology | non-quad, 0면적, 뒤집힌/꼬인 quad, 열린 경계와 예외 |
| UV | 2개 채널, 유한 값, UV 면적, 타일 주기/atlas 영역/방향/padding |
| 재질 | 슬롯 순서·family·texture 경로·tint 역할·색 공간·normal strength |
| 부착 | 실제 검사한 부품·방법·접촉/돌출 수치·의도된 간극 |
| Export | FBX 재import 비교, normal/tangent/socket 유지 |
| 한계 | Unity 실행/컴파일, 외형, mip, bake, collision 등 미검증 범위 |

숫자 검사만 했다면 숫자 검사라고 보고한다. 하나의 접촉 사례를 검사한 것을 모든 부품의 관통/접촉을 완전 증명한 것으로 과장하지 않는다.

## 17. 납품 구조와 버전 관리

권장 구조:

```text
BREAK_NORTH_<Stage>_<Version>/
  README_KO.md
  ASSET_CATALOG.md
  MATERIAL_UV_CONTRACT.md
  SCOPE_AND_REVIEW.md 또는 ASSET_REVIEW.md
  CHANGELOG.md                 # 기존 버전 수정 시
  BlenderSources/
  Optional_PartsFBX/
  ComparisonScenes/           # 필요 시, 렌더 이미지와 구분
  Assets/<ProjectNamespace>/
    Models/
    Textures/
    Colliders/                # 별도 단순 collision을 제공할 때
    Editor/
    KitManifest.json
  Reports/
```

- 실제 프로젝트 naming convention을 우선한다. 새 일반 후보는 ENV_/FURN_/PROP_/UTIL_/TOOL_/MACH_ 등으로 분류할 수 있지만 기존 key를 임의 교체하지 않는다.
- 현재 M7 조립 FBX는 `SM_BN_M7_<key>.fbx`, M6는 `SM_BN_<key>.fbx`이다.
- 기존 Unity `.meta`/GUID를 보존한다. 승인받지 않은 프로젝트 폴더 삭제/재생성으로 GUID를 바꾸지 않는다.
- 재질 프리셋 생성 코드를 제공한 것과 실제 `.prefab`/`.unity` 파일을 생성·실행한 것을 구분한다.
- 작업 중간 파일/스크립트/추출 사본은 `work/`, 사용자용 최종 파일은 `outputs/`에 둔다.
- 불필요한 구버전 배포본은 `work/archive/`로 이동하여 복구 가능하게 보존한다. 이동 전 실제 절대 경로가 의도한 작업 공간 안인지 확인한다.
- M6처럼 다른 역할의 현재 키트는 M7라는 새 이름이 생겼다는 이유만으로 폐기하지 않는다.

## 18. 현재 전달된 에셋과 한계

### M6 v4

`BREAK_NORTH_M6_v4.zip`: 기존 31종 전체 키트. 벽/바닥/천장, 선반/패널/조명/박스, 망치/드릴/절단기, 콘크리트·금속 파편 각3종, 문틀/해치/기둥/빔/작업대/로커/파이프/덕트/트레이/난간/계단/플랫폼/팔레트 등이 포함된다.

도구의 이전 접촉·쿼드 오류 수정본을 보존한다. 망치 1,000 Tris, 드릴 2,876 Tris, 절단기 3,044 Tris이다. M6 v4 플랫폼은 다리 없는 발판이다. 구조물 부품의 청회색 명도/채도 분배를 조정했으며 벽·바닥·천장 기본 4종과 atlas는 개발자의 생성 UV 문제를 보상하려고 바꾸지 않았다.

### M7 Priority A

`BREAK_NORTH_M7_A.zip`: 공용 모델 40종, 기본 프리셋 231개. 이 수에는 색뿐 아니라 표면·표시 방식도 포함된다. 조명색/표지 cell을 조합하면 제공 Unity 메뉴가 343개 프리팹을 생성하도록 구성되어 있다. **실제 Unity에서 그 메뉴를 실행한 것은 아니다.**

| A 분류 | 모델 key |
|---|---|
| Wall | WallConcrete, WallPaintedMetal, WallReinforcedMetal |
| Floor | FloorConcrete, FloorMetalPlate, FloorIndustrialTile |
| Ceiling | CeilingConcrete, CeilingMetalPanel, CeilingUtilityPanel |
| Trim/Reinforcement | TrimStraight, TrimCorner, ReinforcementHorizontal, ReinforcementVertical, WallBottomGuard |
| Column | ColumnSquare, ColumnRounded |
| Beam | BeamI, BeamBox |
| Railing | RailingStraight, RailingCorner, RailingShort |
| Shelf | ShelfA, ShelfB |
| Cabinet | LockerTall, CabinetLow, CabinetDrawer |
| Box/Crate | CardboardBoxSmall, CardboardBoxLarge, PlasticCrate, MetalStorageBox |
| Pipe | PipeStraight, PipeElbow |
| Light | LightLong, LightRound |
| Electric | ElectricalPanel |
| Fuel | Pump, TankVertical |
| Signage | SignRectangular, SignWarning, SignHanging |

Rough Concrete Floor 등은 같은 메시의 재질 변형이다. 모든 형태 후보를 전부 제작한 전체 키트가 아니라, M7의 색/재질 조합 검증을 위한 대표 A 형상 세트이다.

M7에는 40개 `.blend`, 조립 FBX 40개, 부품 FBX 40개, collision proxy FBX 40개, 1K 텍스처 59개가 포함된다. `ComparisonScenes/M7_Comparison_Boards.blend`는 11개 비교 장면과 공유 메시 보관 scene을 포함한다.

제공한 M7 Unity 코드는 Built-in Standard / URP Lit 대상이다. 다른 pipeline은 별도 연결이 필요하다. Glass는 단순 투명 근사이며, collision은 박스 근사다. 파이프 내부 구멍까지 정밀 충돌로 구현하지 않았다.

**M6/M7 모두 여기서 수행한 Blender/FBX 검사와 별도로 실제 Unity 통합·게임 화면 검증이 남아 있다.** M7의 A 납품이 끝났다는 사실을 이후 사용자 외형 승인까지 받은 것으로 해석하지 않는다.

## 19. 새 인스턴스에 넘길 파일과 시작 문구

이 문서 하나로 스타일과 절차는 이해할 수 있다. 기존 모델을 수정하거나 같은 재질을 정확히 이어갈 때는 해당 ZIP과 manifest도 전달해야 한다.

이 작업 공간에서의 상대 위치:

```text
outputs/BREAK_NORTH_ARTIST_HANDOFF.md   # 이 문서
outputs/BREAK_NORTH_M6_v4.zip
outputs/BREAK_NORTH_M7_A.zip
outputs/BREAK_NORTH_M7_A/              # 현재 펼쳐진 M7 폴더
AGENTS.md                            # 이 작업 공간용 요약 규칙
work/rules/BREAK_NORTH_3D_Asset_Production_Rules.md
work/rules/M7_Asset_Request.md
work/m7_materials.py
work/m7_build.py
work/m7_verify.py
work/m7_boards.py
work/m7_delivery.py
```

이 문서는 원본 제작 지침·대화 수정 사항을 통합했으므로 `work/rules`가 없는 새 환경에서도 핵심 기준을 사용할 수 있다. 제작 스크립트와 외부 경로는 이 Markdown에 포함되어 있지 않으며, 새 환경에서는 존재 여부와 의존 파일을 확인해야 한다. 현재 사용한 Blender 실행 경로는 `C:/blender5.2/blender.exe`였지만 다른 컴퓨터에서도 같다고 가정하지 않는다.

새 인스턴스에 다음 문구와 이 문서, 필요한 에셋 ZIP을 함께 전달하면 된다.

> 첨부한 BREAK_NORTH_ARTIST_HANDOFF.md를 제작 기준으로 읽고, 함께 전달한 ZIP의 manifest·재질 계약·검증 기록을 확인한 뒤 다음 요청을 수행해줘. 최신 사용자 지시를 우선하고, 쿼드 모델링·부품 접촉·Space 배색 통일·도구 색 구분·절제된 현실적 재질감을 유지해줘. M6/M7 계약을 섞거나 기존 승인 파일을 덮어쓰지 말고, 새 미리보기 렌더는 별도 요청 전까지 만들지 마. 실제로 수행한 검사와 Unity 미검증 항목을 구분해서 보고해줘. 이번 작업 범위는: [여기에 새 요청 입력].

## 20. 마지막 판단 순서

1. 실루엣이 읽히는가?
2. 기능이 읽히는가?
3. 기존 에셋과 같은 세계처럼 보이는가?
4. 재질이 구분되고 찰흙처럼 뭉개지지 않는가?
5. 불필요한 geometry가 있는가?
6. 반복 배치할 때 고유 디테일이 지나치게 눈에 띄는가?
7. 상호작용 가능한 물체처럼 보이면서 쓸 수 없는 장식으로 오해될 여지가 있는가?
8. 쿼드·정렬·접촉·UV·export 검사가 실제 결과로 확인되었는가?

**모델 하나를 독립 작품처럼 만드는 것보다 BREAK NORTH 세계 전체의 부품으로 만드는 것을 우선한다.**

---

## 21. 2026-09-14 사용자 승인 스타일 — M6 Architecture v3

사용자는 v3 제작 결과에 대해 **“네가 지금 만든 스타일 매우 좋아”**라고 명시적으로 평가했다. 이번 v3를 이후 신규 제작의 구체적인 시각적 기준으로 삼는다. 이는 이전 M6 v4 / M7 A 전체를 재제작하거나 그 버전의 계약을 변경하라는 지시가 아니다.

승인된 방향은 **밝은 스타일라이즈드 산업 공간 + 기능이 읽히는 단순한 형상 + 현실적인 표면 디테일**이다. 현실감은 주로 normal, roughness, 재질별 반사 차이로 더한다. 포토리얼의 어둡고 탁한 배색을 따라가지 않는다. 기존 3~5절의 감정·색채·기능색·Space 배색 원칙은 그대로 유효하다.

- 콘크리트: 밝은 베이지, 기공과 골재가 있는 표면. 단면은 표면보다 어둡고 거칠게 구분하되 전체를 어둡게 만들지 않는다.
- 도장 금속: 밝은 청회색, 넓은 평면과 얇은 테두리. 약한 도장 요철·긁힘을 normal로 표현한다.
- 구조용 철재: 청회색 계열의 중간 명도, 도장 판과 구분되는 부드러운 반사. 지나치게 검은 금속이나 거울 같은 광택을 기본으로 삼지 않는다.
- 바닥: 밝은 중성 회색. 천장: 따뜻하고 밝은 크림 계열. 한 Space 안에서 색을 무작위로 섞지 않는다.
- 기존 도구의 고유 색 구분과 기능색은 유지한다. 이번 건축 팔레트를 모든 도구에 일괄 적용하지 않는다.

사용자는 처음부터 **폴리곤 수를 많이 늘리지 않으면서 normal map으로 더 현실적인 텍스처**를 원했다. 이후 지적한 것은 표면 디테일의 존재가 아니라 금속의 모자이크 같은 반사와 어둡고 현실적인 색감이었다. 따라서 디테일을 다시 지워 균일한 찰흙 같은 표면으로 되돌리지 않는다.

## 22. 재질과 색감의 실제 구현 — v2/v3 기준

### 중립 BaseColor와 기본 tint

v3 텍스처 24장과 기본 tint는 v2와 동일하다. **중립색 BaseColor × material tint**로 색을 만든다. Blender에서는 `Handoff_Default_Tint` multiply node, Unity에서는 Built-in `Color` / URP `Base Color`에 tint가 적용된다. 실제 화면은 그 뒤 조명·환경 반사·톤매핑의 영향을 받는다.

텍스처 PNG만 열었을 때 베이지·청회색이 약하게 보이는 것은 이 구조의 정상적인 결과다. PNG 자체를 채색한 후 기존 tint를 그대로 두어 색을 이중 적용하지 않는다. Normal과 MetallicSmoothness는 색상 그림이 아닌 데이터이다. 파일 단독 인상과 완성된 material의 외형을 혼동하지 않는다.

아래는 **승인된 건축 키트의 기본 sRGB tint**이며 최종 화면 픽셀 색이나 모든 후속 에셋의 고정색이 아니다. 같은 메시의 색 변형은 계속 material로 처리한다.

| Family | 기본 tint |
|---|---|
| ConcreteSurfaceNeutral | `#E4D9C3` |
| ConcreteInterior | `#C5BBA5` |
| PaintedMetalNeutral | `#B5C8D8` |
| BareCutMetal | `#CBD4DC` |
| StructuralSteel | `#AABECE` |
| FloorNeutral | `#C6C9C5` |
| CeilingNeutral | `#EBE5D6` |
| ReinforcedInterior | `#B8B3A5` |

Blender node 값은 필요한 sRGB→linear 변환을 적용한다. Unity color 필드와 Blender 내부 선형 수치를 숫자 그대로 대입하여 색을 어긋나게 하지 않는다. 정확한 구현은 v3의 manifest와 재질 노드/Editor 코드를 참고한다.

### 금속의 모자이크 반사 재발 방지

v1에는 금속 roughness에 44×44 사각 보간 노이즈와 높은 metallic 값이 있었다. 사용자 화면의 원인을 직접 렌더로 확정한 것은 아니지만, 해당 패턴이 반사에서 도드라질 수 있어 v2에서 제거했고 v3에서도 유지했다.

- 사각 셀 단위의 roughness 변화나 고대비 불규칙 광택을 기본으로 사용하지 않는다.
- 현재 StructuralSteel은 metallic 약 **0.72**, roughness 약 **0.56**. BareCutMetal은 약 **0.90 / 0.48**이다. 연속적인 저대비 변화를 더한다.
- 금속 normal의 픽셀 단위에 가까운 진동을 줄이고 미세한 방향성 표면은 남겼다. 새 작업도 mip/압축에서 깨져 보일 수 있는 고주파 패턴에 주의한다.
- 모든 재질의 roughness/metallic을 같게 만드는 방식으로 해결하지 않는다. 도장과 노출 금속을 구분한다.
- 이 수치는 이번 키트의 승인된 출발점이다. 다른 형상/재질/조명에 무조건 전역 적용할 규칙이 아니다.

### 앞면·뒷면 계약 유지

Wall은 **Face A / Face B / Interior**의 독립된 슬롯과 재질을 유지한다. 앞면 베이지, 뒷면 청회색처럼 각각 색을 바꿀 수 있고 서로 다른 family의 재질로 교체할 수도 있다. Slab도 **Top / Bottom / Interior**를 유지한다.

v3 금속 벽의 테두리는 해당 Face A/B 도장 재질을 따라간다. 나사는 기존 Interior 슬롯의 BareCutMetal을 공유한다. 즉 **나사용 새 독립 슬롯은 없으며**, Interior 재질을 교체하면 나사에도 영향을 준다. 기존 응답의 “별도 금속 재질”은 앞·뒷면 도장과 구분된다는 뜻이지 단면과 독립된 네 번째 슬롯이라는 뜻이 아니다. 후속 작업에서 나사와 단면까지 독립 제어가 필요하면 슬롯/재질 계약을 명시적으로 설계한다.

## 23. 승인된 기능 디테일과 과장 허용 범위

사용자는 금속 벽의 얇은 직사각 테두리와 모서리 나사가 있는 참고 그림을 제공했다. v3는 이를 **양면의 45° 맞댐 테두리, 각 면 네 모서리 체결부**로 구현했다. 기둥 collar, 빔 flange, 금속 joint, 문틀/해치틀, end cap, reinforcement trim에도 기능적인 볼트를 추가했다. 콘크리트 넓은 면에 이유 없이 나사를 뿌리지는 않았다.

마지막 사용자 지시:

> “나사 등의 디테일은 조금의 과장은 있어도 괜찮을 것 같아. 수정하라는 얘기는 아니고…”

이는 **향후 제작의 허용 범위**이다. 이 지시만으로 승인된 v3의 나사 크기나 형상을 다시 변경하지 않는다. 현재 작업은 인계서 보완이며 에셋 수정 요청이 아니다.

이후 신규 모델에서는 게임 시점에서 체결부가 읽히도록 나사 머리·와셔·테두리 폭·돌출을 실제 비례보다 조금 강조해도 된다. 고정 배율은 사용자가 정하지 않았으므로 임의의 수치를 전역 규칙으로 만들지 않는다. 주 형상보다 나사가 먼저 보이거나 모든 모서리가 과도하게 둥글어지는 장난감 같은 과장은 피한다.

- 테두리와 체결부는 기능과 조립 관계를 설명한다. 논리 Cell이나 파괴 그리드를 장식 패널선으로 드러내지 않는다.
- 가까이서 실루엣을 만드는 나사 머리·얇은 프레임은 geometry로 표현해도 된다. 나사산·미세 홈·스크래치 전부를 geometry로 만들 필요는 없다.
- v3 볼트는 작은 chamfer가 있는 닫힌 육각 머리이다. 실제 나사산이나 십자 홈을 구현했다고 해석하지 않는다.
- 현재 bolt head는 지지면 안으로 약 1mm, 금속 벽 테두리는 도장 면 안으로 약 2mm 맞물린다. 나사 중심의 지지면 raycast를 검사했다. 새 부품의 크기·지지면이 달라지면 다시 측정한다.
- 추가 디테일로 UV1 packing이 바뀔 수 있다. all-quad, 닫힌 부품, UV 면적/겹침, tangent, FBX reimport 검사를 계속 수행한다.
- 기능 없는 작은 hardware마다 collider를 추가하지 않는다. 구조 collider와 visual detail을 구분하고 실제 보행 개구부를 유지한다.

v3 실측 예: MetalWallThick **460 tris**, Column/Beam **452 tris**, DoorFrame **668 tris**, HatchFrame **560 tris**, XJoint **668 tris**. 금속 벽 구조 두께는 **0.15m**, 테두리를 포함한 visual 두께는 **0.174m**이다. **visual bounds를 snapping/구조 두께로 오인하지 않는다.** 피벗·구조 thickness·collider 기준은 별도 항목으로 보존한다.

## 24. 현재 실제 전달 파일과 검증 상태

이번에 제작한 것은 **M6 Architectural Foundation 필수 11종 + 권장 6종**이다. 두께별 형상 변형을 포함한 실제 모델 **27개**, 개구부·파괴 상태 참고용 fixture **6개**, 총 **FBX 33개**이다. 기존 M6 v4 / M7 A 전체를 대체하는 패키지가 아니다.

현재 작업 공간 기준:

```text
BREAK_NORTH_ARTIST_HANDOFF.md                # 최신 인계서: 이 파일
outputs/BREAK_NORTH_M6_Architecture_v3.zip    # 사용자 승인 스타일 참조 납품본
outputs/BREAK_NORTH_M6_Architecture_v3/
  README_KO.md
  ASSET_CATALOG.md
  MATERIAL_UV_CONTRACT.md
  ASSEMBLY_AND_GAME_INTEGRATION.md
  BlenderSources/BN_M6_Architecture_Library.blend
  ComparisonScenes/BN_M6_Assembly_And_Cut_References.blend
  Assets/BREAK_NORTH_M6_Architecture/
    KitManifest.json
    Models/
    Textures/
    Editor/BN675ArchitectureImporter.cs
  Reports/Hardware_V3_Changes.json
  Reports/Geometry_And_FBX_Checks.json
  Reports/Material_UV_Normal_QA.json
  RebuildScripts/
```

새 인스턴스에는 **이 인계서와 v3 ZIP을 함께 전달**한다. 문서만으로 geometry와 material node를 정확히 복원할 수 있다고 가정하지 않는다. 이전 19절의 M6/M7 파일 경로 및 생성 스크립트는 이전 환경 기록이므로 현재 존재 여부를 다시 확인한다. 이 작업에서는 `C:/blender/blender.exe`, Blender 5.2.1 LTS를 사용했다. 다른 컴퓨터에서도 같은 경로라고 가정하지 않는다.

Unity namespace는 `Assets/BREAK_NORTH_M6_Architecture`이다. 기존 `Assets/BREAK_NORTH_FinalKit` 및 `Assets/BREAK_NORTH_M7`와 구분한다. 이 키트는 atlas가 아닌 **2m/UV주기 타일 재질**, 1K 텍스처 24장, normal strength 기본 1.0을 사용한다. M6 v4/M7의 atlas와 normal strength 규칙을 섞지 않는다.

Unity Editor 도구는 Built-in Standard / URP Lit의 재질·프리팹 생성, 임포트 검사, 참고 scene 생성을 제공한다. Build 메뉴는 이번 기본 tint 팔레트를 다시 적용한다. 사용자 커스텀 재질이나 override가 있다면 먼저 확인한다. `.meta`/GUID를 보존하며, 코드가 제공되었다는 사실을 Unity에서 이미 실행되었다는 뜻으로 해석하지 않는다.

**사용자 스타일 승인은 있음. 실제 Unity 실행 검증은 아직 없음.** Blender/FBX의 형상·UV·normal·tangent·부착 검사는 수행했지만 Unity C# compile/menu, 게임 화면, physics, lightmap, runtime destruction, Save/Load/Host/Late Join은 수행하지 않았다. 참고 파괴 장면은 정적 geometry 배치이다. 새 렌더 이미지를 만들지 않는 기존 원칙도 유지한다.

## 25. 새 인스턴스 시작 문구 — 최신

> BREAK_NORTH_ARTIST_HANDOFF.md의 기존 핵심과 21~25절의 최신 추가 기준을 함께 읽고, BREAK_NORTH_M6_Architecture_v3.zip을 실제 스타일 참조로 사용해줘. 사용자는 v3의 밝은 베이지·청회색 산업 스타일, normal 기반 표면 디테일, 얇은 금속 테두리와 기능적인 볼트를 승인했어. 낮은 폴리곤과 쿼드·모듈·부착 검증을 유지하고, 금속의 사각 roughness 패턴이나 어둡고 탁한 색감으로 되돌리지 마. 앞·뒷면의 독립 재질 계약과 neutral BaseColor × tint 구조를 유지해줘. 향후 새 디테일은 나사 머리 등이 게임 시점에서 읽히도록 조금 과장해도 되지만, 기존 승인 모델을 이 이유만으로 재수정하지 마. 실제 Unity 미검증 항목과 사용자 스타일 승인을 구분해서 보고해줘. 이번 새 작업 범위는: [여기에 요청 입력].
