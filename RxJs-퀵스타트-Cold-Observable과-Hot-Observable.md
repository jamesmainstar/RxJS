| 구분                  | Cold Observable                          | Hot Observable                                                     |
|-----------------------|------------------------------------------|--------------------------------------------------------------------|
| 데이터 주제 생성 시기 | Observable 내부                          | Observable 외부                                                    |
| Observer와의 관계     | 1:1                                      | 1:N                                                                |
| 데이터 영역           | Observer마다 독립적                      | N개의 Observer와 공유                                              |
| 데이터 전달 시점      | 구독하는 순간부터 데이터를 전달하기 시작 | 구독과 상관없이 데이터를 중간부터 전달                             |
| RxJS 객체             | Observable                               | fromEvent에 의해 생성된 Observable, ConnectableObservable, Subject |