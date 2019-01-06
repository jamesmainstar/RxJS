- [기술적부채란](https://brunch.co.kr/@pubjinson/23)
- [기술적부채 해결은 보이스카웃 규칙으로](https://www.slideshare.net/mobile/jinhyuckkim7/ss-79626046)
- [Code Climate 분석 포인트 10가지](https://codeclimate.com/blog/10-point-technical-debt-assessment/)
  - [DRY 원칙](프로그래밍의-정석#22-drydont-repeat-yourself) 위배면 기술적 부채
- [오버 엔지니어링](https://zetawiki.com/wiki/오버엔지니어링)
  - 요구사항보다 높은 스펙일 때
  - [KISS 원칙](프로그래밍의-정석#21-kisskeep-it-simple-stupid--keep-it-short-and-simple) 위배

#### Code Climate 기술적 부채 분석 포인트 10가지
Argument count - Methods or functions defined with a high number of arguments

Complex boolean logic - Boolean logic that may be hard to understand

File length - Excessive lines of code within a single file

Identical blocks of code - Duplicate code which is syntactically identical (but may be formatted differently)

Method count - Classes defined with a high number of functions or methods

Method length - Excessive lines of code within a single function or method

Nested control flow - Deeply nested control structures like if or case

Return statements - Functions or methods with a high number of return statements

Similar blocks of code - Duplicate code which is not identical but shares the same structure (e.g. variable names may differ)

Method complexity - Functions or methods that may be hard to understand