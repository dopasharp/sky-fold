# SKY FOLD ✈️

스마트폰으로 종이비행기를 접고, 폰을 손에 쥔 채 휘둘러 발사하는 모바일 웹게임입니다.

## GitHub Pages 배포
1. GitHub에서 공개 저장소를 만들고 `index.html`을 저장소 최상위에 업로드합니다.
2. 저장소의 **Settings → Pages → Build and deployment**에서 **Deploy from a branch**, `main`, `/ (root)`를 선택합니다.
3. 배포된 HTTPS 주소를 두 스마트폰에서 엽니다.

## 두 폰 실시간 연결 설정
1. [Firebase Console](https://console.firebase.google.com/)에서 프로젝트를 생성하고 웹 앱을 등록합니다.
2. **Realtime Database**를 생성합니다. (Firestore와 다릅니다.)
3. `index.html` 상단의 `firebaseConfig`에 `apiKey`, `authDomain`, `databaseURL`, `projectId`, `appId`를 넣습니다.
4. 테스트 전용 Realtime Database 규칙 예시:

```json
{
  "rules": {
    "rooms": {
      "$room": {
        ".read": true,
        ".write": true
      }
    }
  }
}
```

**주의:** 위 규칙은 공개 테스트 전용입니다. 방 코드를 아는 누구나 읽고 쓸 수 있고, 공격자가 임의의 방 코드를 생성하거나 데이터를 남용할 수 있습니다. 공개 운영 시 Firebase Authentication(익명 로그인 포함), 데이터 구조/크기 검증, App Check 및 접근 제한을 적용하세요. 이 데모는 최신 이벤트 하나만 저장하며 별도의 방 입장 인증을 제공하지 않습니다.

## 게임 방법
- 접기 슬라이더로 날개/대칭/접기 강도/기수 각도를 조절합니다.
- 모바일에서 **센서 허용** → **발사 준비**를 누른 뒤 폰을 단단히 잡고 짧게 앞으로 휘두릅니다.
- 센서가 동작하지 않으면 **연습 발사**를 누릅니다.
- 두 폰에서 같은 6자리 방 코드로 연결하면 발사/착륙 이벤트를 공유합니다.
- 받은 폰은 다시 접고 발사하여 릴레이를 이어갈 수 있습니다.

## 구현 참고
- HTML/CSS/Canvas 2D + JavaScript ES modules, Firebase Realtime Database 선택 연동.
- 간단한 게임용 물리 모델이며 실제 공기역학을 정밀 재현하지 않습니다.
- 기종별 센서 축과 가속도 범위가 달라 실제 던지는 방향/힘과 완전히 일치하지 않을 수 있습니다.
- 두 폰은 동일한 이벤트를 받아 각각 시뮬레이션하므로 물리 결과가 항상 같지는 않습니다.
- 스마트폰을 실제로 던지거나 놓지 마세요.