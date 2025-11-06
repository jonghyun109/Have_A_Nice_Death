<div align="center">


# [<img width="60" height="60" alt="Youtube_logo" src="https://github.com/user-attachments/assets/9d483d59-aafd-46a6-b2af-960d668ad166" />](https://www.youtube.com/watch?v=cBADKkWetoM&t=6s)  Have A Nice Death 모작

### 죽음의 CEO가 반란을 진압한다! 스타일리시한 2D 로그라이크 액션!

<br>

<table>
  <tr>
    <td align="center" width="33%">
      <img src="https://github.com/user-attachments/assets/ca443e86-8ec0-4569-a282-cf626764d344" /> 
      <br/>
      <b>보스 연출</b>
    </td>
    <td align="center" width="33%">
      <img src="https://github.com/user-attachments/assets/280d3da7-190b-4f3c-849b-38e9781cacf3" /> 
      <br/>
      <b>메인 로비</b>
    </td>
    <td align="center" width="33%">
      <img src="https://github.com/user-attachments/assets/4bac775f-b7d3-4db8-a9b3-f7c41c329473" />
      <br/>
      <b>맵</b>
    </td>
  </tr>
</table>



<br>
<br>

⭐ **부드러운 카메라 연출과 다채로운 씬 전환 시스템**

⭐ **패턴 기반 적 AI와 발사체 공격 시스템**

⭐ **엘리베이터 및 인터랙션 시스템**

</div>

<br>
<br>
<br>


---

</div>

<br>
<br>

## 📋 목차

- [게임 소개](#-게임-소개)
- [프로젝트 개요](#-프로젝트-개요)
- [주요 스크립트](#-주요-스크립트)
  - [카메라 시스템](#-카메라-시스템)
  - [씬 및 UI 관리](#-씬-및-ui-관리)
  - [엘리베이터 시스템](#-엘리베이터-시스템)
  - [적 AI 시스템](#-적-ai-시스템)
  - [인터페이스 및 유틸리티](#-인터페이스-및-유틸리티)
- [기술 스택](#-주요-기술-스택)
- [참고사항](#-참고사항)
- [개발자](#-개발자)

<br>
<br>

---

<br>
<br>

## 🎯 게임 소개

**Have A Nice Death**는 **2D 플랫포머 액션 게임**으로,  
부드러운 카메라 연출, 상태 패턴 기반의 적 AI, 다채로운 씬 전환 효과를 중심으로 제작되었습니다.  

플레이어는 다양한 스테이지를 탐험하며, 유령형 적들과 전투를 펼치고,  
보스전을 위한 엘리베이터를 타고 최종 보스를 마주하게 됩니다.  

Lerp 기반의 부드러운 카메라 무빙, 카메라 셰이크 연출, Fade In/Out 효과,  
패럴랙스 배경 시스템 등으로 몰입감 있는 게임 경험을 제공합니다.

<br>
<br>

---

<br>
<br>

## 📌 프로젝트 개요

| 항목     | 내용                          |
|----------|-------------------------------|
| 유형     | 2D 팀 프로젝트                 |
| 기간     | 2025. 01. 13 ~ 2025. 01. 23 (9일) |
| 인원     | 개발자 4명                     |
| 도구     | Unity, Notion                 |

<br>
<br>

---

<br>
<br>

# 📁 JongHyun Scripts

> Have A Nice Death 프로젝트의 JongHyun 폴더 스크립트 모음입니다.

<br>
<br>

---

## 💻 주요 스크립트

<br>

## 🎥 카메라 시스템

<br>

### [`BossCamera.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/BossCamera.cs)

**💡 기능**: 보스 전투 전용 카메라 제어

**📌 주요 기능**:
- **3가지 카메라 모드**: Follow (플레이어 추적), Shake (진동 효과), BossRoom (고정)
- 플레이어가 일정 위치(-8f)에 도달하면 보스룸으로 부드럽게 이동
- 보스룸 도착 시 카메라 사이즈를 9로 확대 및 벽 활성화
- ITriggerShake 인터페이스 구현으로 외부에서 카메라 진동 트리거

**📌 주요 메서드**:
- `FollowPlayer()`: 플레이어 추적 및 보스룸 도착 시 전환
- `MaxDistanceCamera()`: 카메라 이동 범위 제한 (x: -44f 이상, y: 0~0.5f)
- `ShakeCamera()`: 0.3초 동안 랜덤 진동 효과
- `TriggerShake()`: 외부에서 카메라 진동 시작

**✨ 특징**: 
- Vector3.Lerp로 부드러운 카메라 이동 (속도: 4f)
- 보스룸 도착 여부를 isArrive 플래그로 관리
- 카메라 셰이크 시 originalPos 기준으로 랜덤 오프셋 적용

<br>

### [`CameraController.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/CameraController.cs)

**💡 기능**: 일반 스테이지 카메라 제어

**📌 주요 기능**:
- **2가지 카메라 모드**: Follow (플레이어 추적), Shake (진동 효과)
- 플레이어 Y축 위치에서 +3 오프셋으로 상단 시야 확보
- X축 이동 범위 제한 (Clamp: -6f ~ 316f)
- ITriggerShake 인터페이스 구현

**📌 주요 메서드**:
- `FollowPlayer()`: 플레이어를 부드럽게 추적 (Lerp 속도: 4f)
- `ShakeCamera()`: 0.3초 동안 랜덤 진동 효과
- `TriggerShake()`: 외부에서 카메라 진동 시작

**✨ 특징**: 
- Y축 오프셋 +3으로 플레이어 상단 시야 확보
- 셰이크 종료 후 Follow 모드로 자동 복귀

<br>

### [`FollowCamera.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/FollowCamera.cs)

**💡 기능**: 패럴랙스 배경 카메라 효과

**📌 주요 기능**:
- 메인 카메라의 움직임을 추적하여 배경이 입체감 있게 이동
- backgroundSpeed 값으로 배경 속도 조절 (0~1: 느리게, 1 초과: 빠르게)
- 초기 오프셋 저장으로 배경 시작 위치 유지

**📌 주요 메서드**:
- `Update()`: 카메라 위치 * backgroundSpeed + offset으로 배경 위치 계산

**✨ 특징**: 
- 간단한 수식으로 패럴랙스 효과 구현
- 다층 배경 시스템에 적합 (각 배경마다 다른 backgroundSpeed 설정)

<br>
<br>

---

<br>
<br>

## 🎬 씬 및 UI 관리

<br>

### [`SceneChange.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/SceneChange.cs)

**💡 기능**: Fade 애니메이션을 통한 씬 전환

**📌 주요 기능**:
- 버튼 클릭 시 Fade 애니메이션 패널 활성화
- Image의 Green 채널이 0이 되면 "JonghyunTest" 씬으로 이동
- Animator와 연동하여 자연스러운 페이드 효과

**📌 주요 메서드**:
- `MainSceneChanger()`: Fade 패널 활성화
- `FixedUpdate()`: Green 채널 체크 후 씬 로드

**✨ 특징**: 
- Animator의 Color 변화와 스크립트 연동
- FixedUpdate로 정확한 타이밍 체크

<br>

### [`PressAnyKey.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/PressAnyKey.cs)

**💡 기능**: 아무 키나 눌러 인트로 씬으로 이동

**📌 주요 기능**:
- Input.anyKeyDown으로 모든 키 입력 감지
- 사망 화면 또는 타이틀 화면에서 재시작

**✨ 특징**: 
- 간결한 입력 처리
- 인트로 씬(IntroScene)으로 이동

<br>

### [`DeadScript.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/DeadScript.cs)

**💡 기능**: 사망 화면 UI 제어

**📌 주요 기능**:
- deadImage의 알파값이 0이 되면 deadText 활성화
- Fade In 완료 후 사망 메시지 표시

**✨ 특징**: 
- Animator와 연동하여 단계별 UI 표시
- 알파값 체크로 타이밍 제어

<br>

### [`ChangeColorA.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/ChangeColorA.cs)

**💡 기능**: 텍스트 알파값 페이드 인/아웃 애니메이션

**📌 주요 기능**:
- 알파값을 0 ↔ 1 사이에서 반복 증감
- isForward 플래그로 방향 전환
- 0.01씩 증감하여 부드러운 애니메이션

**📌 주요 메서드**:
- `Update()`: 매 프레임 알파값 조정 및 텍스트 색상 업데이트

**✨ 특징**: 
- "Press Any Key" 등 깜빡이는 텍스트 연출에 적합
- Update에서 직접 제어하여 Animator 불필요

<br>

### [`GameExit.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/GameExit.cs)

**💡 기능**: 게임 종료 버튼

**📌 주요 기능**:
- 에디터에서는 플레이 모드 종료
- 빌드에서는 Application.Quit() 호출

**✨ 특징**: 
- 전처리기 지시문으로 에디터/빌드 분기
- UI 버튼의 OnClick 이벤트에 연결

<br>
<br>

---

<br>
<br>

## 🛗 엘리베이터 시스템

<br>

### [`ElevatorInPlayer.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/ElevatorInPlayer.cs)

**💡 기능**: 플레이어 엘리베이터 탑승 및 씬 전환

**📌 주요 기능**:
- F키 입력으로 엘리베이터 탑승
- 탑승 시 엘리베이터와 플레이어 애니메이션 동기화
- 엘리베이터 SpriteRenderer의 Red 값이 0이 되면 Fade In 시작
- Fade In 완료 후 "BossTestRoom" 씬으로 전환
- 인터랙션 범위 진입 시 F 버튼 UI 표시

**📌 주요 메서드**:
- `OnTriggerStay2D()`: F키 입력 감지 및 애니메이션 시작
- `OnTriggerExit2D()`: 범위 벗어나면 F 버튼 UI 비활성화
- `FixedUpdate()`: 엘리베이터 색상 체크 후 Fade 및 씬 로드

**✨ 특징**: 
- 애니메이션 speed를 0으로 초기화하여 대기 상태 유지
- F키 입력 시 speed를 1f로 설정하여 애니메이션 재생
- SpriteRenderer의 Red 값과 Image의 Red 값을 순차적으로 체크

<br>

### [`BossElevator.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/BossElevator.cs)

**💡 기능**: 엘리베이터 내부 플레이어 표시 제어

**📌 주요 기능**:
- _playerOut 플래그로 플레이어 오브젝트 활성화/비활성화
- 엘리베이터 내부에서는 플레이어 숨김, 외부에서는 표시

**✨ 특징**: 
- Player 컴포넌트 자동 할당
- Update에서 매 프레임 체크

<br>

### [`PlayerElevatorOut.cs (PlayerOut 클래스)`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/PlayerElevatorOut.cs)

**💡 기능**: 엘리베이터 하차 시 플레이어 표시 제어

**📌 주요 기능**:
- _playerOut 플래그와 elevatorIn 애니메이션 속도를 체크
- 엘리베이터 애니메이션 재생 중에는 플레이어 숨김
- 애니메이션 종료 후 플레이어 표시

**✨ 특징**: 
- BossElevator와 유사하지만 elevatorIn 애니메이션 체크 추가
- 엘리베이터 문 열림/닫힘과 동기화

<br>
<br>

---

<br>
<br>

## 👻 적 AI 시스템

<br>

### [`WomanGhostAi_Clone.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/WomanGhostAi_Clone.cs)

**💡 기능**: 여자 유령 적 AI (순찰, 감지, 공격)

**📌 주요 기능**:
- Walker 클래스 상속 및 IHittable, ILootable 인터페이스 구현
- **좌우 순찰 AI**: 시작 위치 기준 moveDistance 범위 내 왕복
- **플레이어 감지**: Physics2D.OverlapCircle로 시야 범위 내 플레이어 탐지
- **발사체 공격**: 플레이어 감지 시 1.3초마다 womanFire 발사
- **피격 처리**: HP 감소 및 Hit 애니메이션 재생, 사망 시 0.3초 후 비활성화
- **느낌표 이모티콘**: 플레이어 발견 시 surprisedAnimator 활성화

**📌 주요 메서드**:
- `Move()`: 좌우 순찰 로직 (uturn 애니메이션 포함)
- `DetectPlayer()`: 시야 범위 내 플레이어 감지 및 공격 코루틴 시작
- `FireShot()`: Projectile 풀링으로 발사체 생성 및 발사
- `SpottedPlayer()`: 플레이어 방향으로 회전 및 이동 정지
- `Hit(Strike strike)`: 피격 처리 및 HP 감소, 사망 판정
- `HandleRotation()`: 이동 방향에 따라 Y축 회전 (0° / 180°)

**✨ 특징**: 
- AnimatorPlayer 기반 애니메이션 제어 (idleClip, spottedClip, attackClip, hitClip, deathClip)
- 코루틴 DoFire로 주기적 발사 (isHit 플래그로 중단)
- GameManager.GetProjectile로 오브젝트 풀링 활용
- 플레이어 감지 시 StopAllCoroutines로 기존 공격 코루틴 정리
- isAlive 프로퍼티로 생존 여부 확인 (womanGhostHP > 0)

<br>

### [`StunEnemy.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/StunEnemy.cs)

**💡 기능**: 적 스턴 상태 관리

**📌 주요 기능**:
- stun 플래그로 적의 스턴 상태 저장
- 다른 스크립트에서 참조하여 적의 행동 제어

**✨ 특징**: 
- 간단한 플래그 클래스
- 적 AI에서 stun 여부를 체크하여 이동/공격 정지

<br>

### [`surpriseImote.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/surpriseImote.cs)

**💡 기능**: 느낌표 이모티콘 표시 제어

**📌 주요 기능**:
- stop 플래그로 이모티콘 표시 여부 제어
- WomanGhostAi_Clone에서 플레이어 감지 시 활성화

**✨ 특징**: 
- 애니메이션 오브젝트의 활성화/비활성화 제어
- stop이 false가 되면 이모티콘 숨김

<br>
<br>

---

<br>
<br>

## 🔧 인터페이스 및 유틸리티

<br>

### [`ITriggerShake.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/ITriggerShake.cs)

**💡 기능**: 카메라 진동 인터페이스

**📌 주요 기능**:
- TriggerShake() 메서드 정의
- BossCamera, CameraController가 구현

**✨ 특징**: 
- 외부에서 일관된 방식으로 카메라 진동 트리거
- 다형성을 활용한 카메라 제어

<br>

### [`BossCutScene.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/BossCutScene.cs)

**💡 기능**: 보스 컷신 스크립트 (미구현)

**✨ 특징**: 빈 클래스 (향후 확장 예정)

<br>

### [`WomanFireSkill.cs`](https://github.com/jonghyun109/Have_A_Nice_Death/blob/main/Assets/Scripts/JongHyun/WomanFireSkill.cs)

**💡 기능**: 여자 유령 화염 스킬 (미구현)

**✨ 특징**: 빈 클래스 (WomanGhostAi_Clone에서 Projectile로 구현)

<br>
<br>

<br>
<br>

---

<br>
<br>

## 🔧 주요 기술 스택

<br>

- 🎮 **Unity 2022.3**: 게임 엔진 (2D Built-in Render Pipeline)
- 💻 **C#**: 게임 로직 프로그래밍
- 🎨 **Unity Animator**: 애니메이션 제어 및 상태 관리
- 🔀 **State Pattern**: 카메라 모드 전환 (enum 기반)
- 🎯 **Physics2D**: 플레이어 감지 및 충돌 처리
- 🔁 **Coroutine**: 주기적 발사체 공격 및 비동기 처리
- 🧩 **Interface**: ITriggerShake, IHittable, ILootable

<br>
<br>

---

<br>
<br>

## 📝 참고사항

<br>

💡 **카메라 시스템**
- Vector3.Lerp를 활용한 부드러운 카메라 이동 (Lerp 속도: 2f~4f)
- enum 기반 상태 패턴으로 카메라 모드 전환 (Follow, Shake, BossRoom)
- ITriggerShake 인터페이스로 외부에서 카메라 진동 트리거
- Clamp로 카메라 이동 범위 제한 (맵 경계 설정)

💡 **적 AI 시스템**
- Walker 클래스 상속으로 기본 이동 기능 구현
- AnimatorPlayer로 Animator Controller 없이 조건부 애니메이션 재생
- Physics2D.OverlapCircle로 플레이어 감지 (시야 범위)
- Projectile 오브젝트 풀링으로 발사체 최적화
- IHittable 인터페이스로 피격 처리 통일

💡 **씬 전환 및 Fade**
- Animator의 Color 변화와 스크립트 연동
- FixedUpdate에서 Color 채널 체크로 정확한 타이밍 제어
- SpriteRenderer와 Image의 색상값으로 단계별 전환

💡 **엘리베이터 시스템**
- Animator.speed를 0/1로 제어하여 대기/재생 전환
- OnTriggerStay2D로 F키 인터랙션 구현
- 애니메이션 속도와 색상값을 체크하여 씬 전환

💡 **패럴랙스 배경**
- backgroundSpeed 값으로 배경 속도 조절 (다층 배경 구현)
- 카메라 위치 * speed + offset으로 간단한 수식 구현

<br>
<br>

---

<br>
<br>

<div align="center">

## 👨‍💻 개발자

<br>

**JongHyun (윤종현)**

<br>
<br>

[![GitHub](https://img.shields.io/badge/GitHub-jonghyun109-181717?style=for-the-badge&logo=github)](https://github.com/jonghyun109)

<br>

**📌 모든 스크립트 링크는 위의 GitHub 저장소에서 확인할 수 있습니다.**

</div>

<br>
<br>
