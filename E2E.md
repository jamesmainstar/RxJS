#### 용어정리
- 호스트 시스템 : 네트워크상에서 서비스를 제공하기 위한 컴퓨터
- Selenium : 브라우저 자동화를 위한 툴과 라이브러리들을 포괄하는 범위의 프로젝트이다.
- WebDriver : W3C WebDriver API는 프로그램 및 스크립트가 웹 브라우저의 동작을 제어 할 수 있게 해주는 **플랫폼 및 언어 중립 인터페이스 및 와이어 프로토콜**이다.
- 기능 테스트
  - 소프트웨어 전반이 제대로 돌아가는 지 확인하는 것
  - 고객에게 품질 보증만 할 뿐 생산성과는 무관
  - 기능 테스트 코드는 별도의 버그 발견 전문팀이 개발해야 함
  - 시스템 전반을 최대한 블랙박스로 취급

#### E2E 테스트 목적
- 사용자 관점 테스트 자동화
- 시각적 변경 테스트 자동화
- 기능 테스트

### Nightwatch
#### Install
```bash
npm i nightwatch chromedriver -D
```
#### Config
`nightwatch.conf.js` 파일을 만든다.
```js
module.exports = {
  src_folders : ["tests"],

  webdriver : {
    start_process: true,
    server_path: "node_modules/.bin/chromedriver",
    port: 9515
  },

  test_settings : {
    default : {
      desiredCapabilities: {
        browserName: "chrome"
      }
    }
  },

  test_workers: false
}
```
#### Sample Suite
`test.js` 파일을 만든다.
```js
module.exports = {
  'Demo test Google' : function (browser) {
    browser
      .url('http://www.google.com')
      .waitForElementVisible('body')
      .setValue('input[type=text]', 'nightwatch')
      .waitForElementVisible('input[name=btnK]')
      .click('input[name=btnK]')
      .pause(1000)
      .assert.containsText('#main', 'Nightwatch.js | Node.js powered End-to-End testing framework')
      .end();
  }
};
```
#### Run
```
./node_modules/.bin/nightwatch test.js
```