## 도메인별 분리(Domain-Driven Design)

## 1. 인증 도메인 (Authentication Domain)

- 책임: 사용자 로그인, 인증 상태 관리, 구글 OAuth 연동
- 주요 객체 및 서비스:
    - User (사용자 정보)
    - AuthService (로그인/로그아웃, 토큰 관리)
    - OAuthIntegration (Google OAuth 2.0 연동 처리)

## 2. 알림 도메인 (Notification Domain)

- 책임: 알림 생성, 수정, 삭제, 반복 주기 및 지속 시간 관리, 알림 상태 관리
- 주요 객체 및 서비스:
    - Notification (알림 엔티티: 문구, 시간, 반복 설정, 활성 상태 등)
    - NotificationScheduler (알림 예약 및 실행 관리)
    - NotificationRepository (알림 저장소 - 로컬/클라우드 연동)

## 3. 알림 기록 및 통계 도메인 (Notification History & Statistics Domain)

- 책임: 알림 이력 관리, 완료/무시 상태 기록, 통계 및 그래프 데이터 계산
- 주요 객체 및 서비스:
    - NotificationRecord (알림 응답 기록)
    - StatisticsService (월간 실행율, 통계 데이터 생성)
    - HistoryRepository (기록 저장소 관리)

## 4. 음성 명령 도메인 (Voice Command Domain)

- 책임: 음성 인식, 음성 명령 처리, 음성 인터페이스와 앱 기능 연동
- 주요 객체 및 서비스:
    - VoiceCommandProcessor (음성 데이터 해석 및 명령 변환)
    - SpeechRecognitionService (플랫폼별 음성 인식 연동)
    - VoiceCommandRepository (사용자 음성 명령 데이터 관리)

## 5. 동기화 도메인 (Synchronization Domain)

- 책임: 여러 기기 간 알림 및 설정 동기화, 클라우드 데이터 관리
- 주요 객체 및 서비스:
    - SyncService (Firebase Firestore 동기화 관리)
    - SyncRepository (동기화 데이터 저장 및 조회)

## 6. UI/UX 도메인 (User Interface Domain)

- 책임: 화면 표시, 사용자 입력 처리, 반응형 UI 관리
- 주요 객체 및 서비스:
    - ScreenController (화면 전환 및 상태 관리)
    - UIComponent (알림 리스트, 알림 설정 화면, 위젯 등 UI 컴포넌트)
    - ThemeManager (테마 및 접근성 옵션 관리)

## 7. 위젯 및 퀵액션 도메인 (Widget & Quick Action Domain)

- 책임: 홈 화면 위젯 관리, 현재 알림 문구 표시, 퀵 액션 제공
- 주요 객체 및 서비스:
    - WidgetController (위젯 상태 및 데이터 관리)
    - QuickActionService (퀵 액션 등록 및 실행)

---

이렇게 도메인별로 책임과 역할을 분리하면, 각 도메인은 독립적으로 개발·테스트·배포할 수 있게 되어 유지보수와 확장성 측면에서 유리합니다. DDD 원칙에 따른 경계 컨텍스트(Bounded Context)도 명확해집니다.