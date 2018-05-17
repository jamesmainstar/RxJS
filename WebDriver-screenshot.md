### Screen Capture : https://www.w3.org/TR/webdriver/#screen-capture
Viewport의 Framebuffer의 스냅샷을 가져와 PNG 이미지로 만듬.

#### 모니터 출력 원리
1. User Application에서 *Frame Buffer Data 전송
2. LCD *Driver(Frame buffer driver)가 수신
3. LCD Controller(Frame buffer)가 *TFT-LCD에 출력

* [TFT-LCD(Thin Film Transistor)](http://blog.lgdisplay.com/2016/04/tft/) : 디스플레이의 기본 단위인 픽셀(Pixel)을 제어하는, 일종의 스위치 역할을 담당하는 반도체 소자
* Frame Buffer : Linux System에서 그래픽을 표현할 수 있는 Hardware, PC에서는 그래픽 카드를 이야기함
* [Device Driver](https://ko.wikipedia.org/wiki/%EC%9E%A5%EC%B9%98_%EB%93%9C%EB%9D%BC%EC%9D%B4%EB%B2%84) : 특정 하드웨어나 장치를 제어하기 위한 커널의 일부분으로 동작하는 프로그램