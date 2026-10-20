# CS2-ZephyR-Bot

> ZephyR 디스코드 봇, 스팀 계정 연동·내전 생성·맵 투표 (Java · JDA)

ZephyR는 2024년에 만든 Counter-Strike 2 내전용 커뮤니티 서버다. 이 봇은 디스코드 계정과 스팀 계정을 연결해 가입을 마무리하고, 디스코드에서 내전을 열고 팀을 나누는 일을 맡는다.

## 주요 기능
- 가입 안내 메시지 고정과 "연동" 버튼. 웹에서 로그인해 가입 대기 중인 스팀 계정을 골라 디스코드 계정과 연결한다
- `/생성 인원` 슬래시 명령으로 내전 생성(2~20명), 참여 버튼으로 인원 모집
- 팀 구성: 무작위 배정 또는 `/팀지정`으로 직접 지정
- 맵 투표(dust2, mirage, inferno, vertigo, ancient, nuke, anubis)
- 게임 서버 플러그인과 WebSocket으로 통신해 서버 준비(`server_open`)와 경기 종료(`server_close`)를 받아 메시지와 음성 채널을 정리한다

## 기술 스택
| 영역 | 기술 |
|---|---|
| 언어 | Java 17 |
| 프레임워크 | Spring Boot 3.2.4 (WebSocket), JDA 5.0.0-beta.21, Lombok |
| 데이터 | MongoDB (Spring Data MongoDB) |
| 인프라 | Gradle |

## 구조
```
src/main/java/com/github/ioloolo/zephyrbot/
  ZephyrBotApplication.java   JDA 봇 시작, 가입 안내 메시지
  interaction/command/        /생성, /팀지정
  interaction/button/         참여, 연동, 팀 무작위·지정, 경기 종료
  interaction/dropdown/       계정 연동 선택, 맵 투표
  interaction/modal/          계정 연동 입력
  socket/                     게임 서버 플러그인과의 WebSocket
  repository/                 User, Match
```

## 실행
```bash
cp src/main/resources/application_template.yaml src/main/resources/application.yaml
./gradlew bootRun
```
`application.yaml`에 MongoDB 접속 정보(`spring.data.mongodb.*`), 디스코드 봇 토큰과 채널 ID(`discord.*`), 서버 경로(`server.path`)를 채운다.

## 관련 저장소
- [CS2-ZephyR-Server](https://github.com/son-daehyeon/CS2-ZephyR-Server) — 백엔드 API
- [CS2-ZephyR-Client](https://github.com/son-daehyeon/CS2-ZephyR-Client) — 스킨 설정 웹
- [CS2-ZephyR-Plugin](https://github.com/son-daehyeon/CS2-ZephyR-Plugin) — 게임 서버 플러그인

---
2024 · 개인 프로젝트 · 보관됨
