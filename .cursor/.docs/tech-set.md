아래는 요구하신 기능을 크로스플랫폼으로 구현하기 위한 **필수 기술스택** 목록입니다.

---

## 1. 크로스플랫폼 개발 환경

- **Flutter**
    - Android, iOS, MacOS, 태블릿 등 다양한 플랫폼 지원

---

## 2. 인증 및 계정 연동

- **Google OAuth 2.0**
    - Google 계정 기반 로그인
    - 각 플랫폼별 Google Identity Services SDK 혹은 Firebase Authentication 활용

---

## 3. 알림 기능

- **Flutter Local Notifications Plugin**
    - 로컬 & 푸시 알림 기능 구현(Android/iOS/MacOS 대응)
- **Firebase Cloud Messaging**
    - 푸시 알림 및 기기 간 동기화

---

## 4. UI/UX 구성 요소

- **반응형 디자인 프레임워크**
    - Flutter의 `MediaQuery`, `LayoutBuilder`로 화면별 최적화
- **State Management**
    - Bloc, Provider, Riverpod 등(비즈니스 로직과 UI 분리 및 관리)
- **플로팅 액션 버튼(FAB), 리스트 뷰, 토글 스위치 등 기본 위젯**

---

## 5. 데이터베이스 및 동기화

- **Firebase Cloud Firestore**
    - 실시간 데이터 저장/불러오기 및 계정 기반 데이터 동기화
- (대안: SQLite, AWS Amplify, Supabase 등)

---

## 6. 알림 기록/통계 시각화

- **Chart 라이브러리**
    - `fl_chart`, `charts_flutter` 등(알림 이력 및 실천율 그래프)
- **Firestore or Local DB**를 활용한 기록 저장

---

## 7. 음성명령 및 접근성

- **Flutter Speech Recognition Plugin**
    - 앱 내에서 음성 입력받아 알림 추가/수정
- **플랫폼별 음성 비서 연동**
    - SiriKit(Apple), Google Assistant SDK 등
- **Flutter Widgets for Accessibility**
    - 폰트 크기, 색 대비, 다크/라이트 테마 지원

---

## 8. 위젯·퀵액션

- **Flutter App Widget Support**
    - Android/iOS 홈 화면 위젯 구현(`flutter_widgetkit`, `home_widget` 등)
- **빠른 액션 및 현재 문구 표시 기능 구현**

---

## 9. 기타필수

- **에러 처리 및 온보딩**
    - Exception Handling, 인앱 튜토리얼 제공
- **국제화(i18n)**
    - `flutter_localizations` 등 다국어 지원

---

위 기술스택을 활용하면 요구한 모든 기능을 하나의 통합된 크로스플랫폼 환경에서 효과적으로 구현할 수 있습니다.
SS