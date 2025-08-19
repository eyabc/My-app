```plaintext
[User Voice]
      ↓
[VoiceCommandApplicationService.handleIncomingVoice(userId, audioData)]
      ↓
[SpeechRecognitionService.recognize(audioData)]
      ↓
  “every day at 6 PM remind me to drink water”
      ↓
[VoiceCommandProcessor.process(rawText, userId)]
      ↓
┌───────────────────────────────────────────────────────────┐
│1. parseIntent(rawText) → ADD_NOTIFICATION                │
│2. extractParameters(rawText) →                           │
│   • message = "drink water"                              │
│   • timeSpec = "every day at 6 PM"                       │
└───────────────────────────────────────────────────────────┘
      ↓
[Build CreateNotificationCommand DTO]
      ↓
┌───────────────────────────────────────────────────────────┐
│CreateNotificationCommand {                                │
│  userId           : UUID                                  │
│  message          : "drink water"                         │
│  startDateTime    : Today at 18:00                        │
│  endDateTime      : null                                  │
│  recurrence       : RecurrencePattern {                   │
│                      type=DAILY,                         │
│                      interval=1,                         │
│                      durationStartTime=18:00,            │
│                      durationEndTime=null                │
│                    }                                      │
└───────────────────────────────────────────────────────────┘
      ↓
[NotificationApplicationService.createNotification(cmd)]
      ↓
[NotificationRepository.save(notificationEntity)]
      ↓
[NotificationScheduler.schedule(notificationEntity)]
      ↓
[Notification Created & Scheduled]
      ↓
[VoiceCommandResult{status:SUCCESS,processedAt,…}]
      ↓
[User Feedback (TTS / UI)]
```

음성 명령 도메인에서 “음성 인식 → 알림 DTO 변환” 흐름은 크게 다음 단계로 이루어집니다. PUML에는 각 컴포넌트간 관계만 보여주었지만, 실제 데이터 흐름을 이해하기 위해서는 아래 과정을 참고하세요.

1. **오디오 캡처 및 텍스트 변환**  
   -  사용자가 “Hey Notify, every day at 6 PM remind me to drink water”라는 음성을 말하면,  
   -  `VoiceCommandApplicationService.handleIncomingVoice(userId, audioData)` 호출  
   -  내부에서 `SpeechRecognitionService.recognize(audioData)`가 실행되어 오디오를 텍스트(예: `"every day at 6 PM remind me to drink water"`)로 변환

2. **명령 처리 및 파싱**  
   -  변환된 텍스트를 `VoiceCommandProcessor.process(rawText, userId)`에 전달  
   -  `parseIntent(rawText)`로 “ADD_NOTIFICATION” 의도를 식별  
   -  `extractParameters(rawText)`로 문구(“drink me to drink water”), 시간 패턴(“every day at 6 PM”) 등을 파싱  
   -  이때 파싱 로직은 정규표현식, NLP 모델, 룰 기반 파서 등을 조합해 구현

3. **Notification DTO 생성**  
   -  `VoiceCommandProcessor`는 파싱된 파라미터를 기반으로 내부 DTO(예: `CreateNotificationCommand`)를 생성  
     ```java
     CreateNotificationCommand cmd = new CreateNotificationCommand(
       userId,
       message = "drink water",
       startDateTime = today at 18:00,
       endDateTime = nullable,
       recurrence = RecurrencePattern(type = DAILY, interval = 1, durationStartTime = 18:00, durationEndTime = null)
     );
     ```
   -  이 DTO는 `NotificationApplicationService.createNotification(cmd)`에 전달되어 실제 알림이 생성됨

4. **음성 명령 기록**  
   -  원본 `rawText`, 파싱 결과, 성공·실패 여부, 생성된 `notificationId` 등은 `VoiceCommandRepository`와 `NotificationResultRepository`에 저장돼 추후 히스토리와 통계에 활용

5. **피드백 및 응답**  
   -  처리 결과(`VoiceCommandResult`)를 사용자에게 TTS로 전달하거나 UI 토스트로 보여줌  
   -  예: “알림이 매일 오후 6시에 ‘drink water’로 설정되었습니다.”

***

정리하면, PUML에서 서비스 간 화살표(`VoiceCommandApplicationService → SpeechRecognitionService`, `→ VoiceCommandProcessor`, `→ NotificationApplicationService`)가 바로 이 물리적 데이터 흐름(오디오→텍스트→인텐트/파라미터→DTO→알림 생성)을 간결하게 표현한 것입니다.  
각 단계에서 사용하는 DTO와 메서드 시그니처를 위와 같이 구체화하면, 음성 입력이 알림 설정으로 이어지는 전체 파이프라인을 명확하게 이해할 수 있습니다.