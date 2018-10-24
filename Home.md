#### 회고록
> 라이브러리 또는 프레임워크를 처음 다룰 때는 [TodoMVC](http://todomvc.com)를 참고한다. 베스트 사용법을 알 수 있다.

> API 데이터를 `normalize`하는 것은 알아야 할게 하나 더 생기는 거나 다름 없다. API 형식을 그대로 사용하는 게 가장 이상적이다.

> 대체로 API 연동은 getter, setter로 해결된다. 만약에 초기 데이터 형식이 다를 경우 init 함수를 만드는 게 가장 비용이 적다.

> 업무 관리는 칸반보드로

#### 자료목차
- [기본기](기본기)
- [도서](도서)
- [문제해결](문제해결)
- 오픈소스
  - [프레임워크n라이브러리](프레임워크n라이브러리)
  - [개발환경](개발환경)
  - [관리도구](관리도구)
- 스터디
  - [코드스피츠](코드스피츠)
  - [BEPECO](BEPECO)
- 연구
  - [No Library No Framework](No-Library-No-Framework)
  - [FP Lab](FP-Lab)
  - [Technical Debt](Technical-Debt)
- 도메인
  - [챗봇](챗봇)
- [참고사이트](참고사이트)

***

#### 소소한팁
- 정적 페이지 개발(SPA x) : Webpack 사용. entry에 각 페이지의 js를 정의.
- [WebDriver screenshot](WebDriver-screenshot)
- [package-lock.json](package-lock.json)
- [Intellij 확장자 안열릴 때](%5Bintellij%5D-확장자-안열릴-때)
- href = Hypertext Reference
- eslint-disable-line
- Pull Request에서 develop과 conflict 발생시 feature 브랜치와 머지를 하지 않는 것이 좋음 : feature에 머지시 conflict의 정상동작을 보장 할 수 없음.
- Intellij 단축키
  - 코드 정리 : option + command + L
  - multi cursor : shift + option(alt) + click
  - 테스크 자동 실행 : control + R
  - 코드 구조 표현 : command + 7
  - 최근 사용 파일 : command + E
- placeholder content
- ADID
  - 개인을 식별하지 않고 맞춤형 광고 서비스를 제공할 수 있도록 부여하는 '광고 식별자'
  - Android : GAID(Google Advertising ID), IOS : IDFA(IDentifier For Advertisers)
- XAMPP 파일 서버 설정을 위한 php.ini 수정
  - upload_max_filesize=2M => upload_max_filesize=4096M