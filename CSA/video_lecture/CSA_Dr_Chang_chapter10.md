# CSA Chapter 10 : 컴퓨터 산술 연산
### 1. 덧셈과 뺄셈(Addition and Substraction)
- 기본 컴퓨터의 데이터 형식
	- 부호절대값으로 표시된 고정소수점 이진 데이터(34 : 0 0100010)
	- 부호화된 2의 보수로 표현되는 고정소수점 이진 데이터(-34 : 1 1011110)
	- 부동소수점 이진 데이터(0.34x10^2 : 0 0100010 00000010)
	- 이진화된 십진수(BCD)데이터 (1264 : 0001 0010 0110 1000)
		> 4bit씩 십진수를 이진수로 변환
- 부호절대값 데이터를 이용한 덧셈과 뺄셈
```
Operation	Add Magnitudes	Substract Magnitudes
				when A > B	When A < B	When A = B
(+A) + (+B)	+(A + B)
(+A) + (-B)			+(A - B)	-(B - A)	+(A - B)
(-A) + (+B)			-(A - B)	+(B - A)	+(A - B)
(-A) + (-B)	-(A + B)
(+A) - (+B)			+(A - B)	-(B - A)	+(A - B)
(+A) - (-B)	+(A + B)
(-A) - (+B)	-(A + B)
(-A) - (-B)			-(A - B)	+(B - A)	+(A - B)
```
- 하드웨어 구성

[이미지 자리]
- 하드웨어 알고리즘
	- 덧셈 알고리즘
	- 뺄셈 알고리즘
	- 부호의 의미
		- Exclusive OR에 의하여 비교
			- 0: 동일부호
			- 1: 다른부호
		- 오버플로우의 처리 필요
			- 같은 부호 연산 : YES
			- 다른 부호 연산 : NO
				> 서로 부호가 다를 경우에는 오버플로우가 발생할 수가 없음
		- 절대값의 비교
			- A < B, A > B인 경우의 처리

[이미지자리:플로우맵]
- 부호가 있는 2의 보수 데이터를 이용한 덧셈과 뺄셈
	- 하드웨어 구조
		- A --> AC register, B --> BR register
	- 덧셈/뺄셈 알고리즘
		- 오버플로우의 조사  V <-- Overflow
			> V bit 가 1일 경우 overflow라고 판단
### 2. 곱셈 알고리즘(Multiplication Algorithm)
- 곱셈의 원리
	- 연속적인 시프트와 덧셈으로 구성
		> Multiplier의 값이 1일 경우 Multiplicand를 시프트 후 덧셈 / 0일경우 시프트만 시행
- 하드웨어 구성
	- A --> AC(계산값) B --> 피승수
	- Q --> 승수
	- SC --> 시퀀스 카운터
		> 시프트에 대한 카운터(자리수를 결정)
	- As ,Bs, Qs --> 부호 비트
	- EAQ --> 결과값
		> E: carry 오버플로우 값 / 총 결과의 비트수는 E(1bit) + A 비트크기 + Q비트크기

[이미지 자리 : 하드웨어 구성]
- 하드웨어 알고리즘

[이미지 자리 : 플로우차트]
- Booth의 곱셉 알고리즘
	- 부호가 있는 2의 보수로 표현된 정수에 대한 곱셈 수행
		> 이미 보수로 표현된 수에 대한 연산을 진행하므로 별도의 부호비트를 표시하지 않음
	- 승수값이 0인 경우 --> 시프트만 수행
	- 2^k ~ 2^m까지의 값이 1인 경우 --> 2^(k+1) - 2^m과 동등하게 취급
		- (14: 001110) =  2^(k+1) - 2^m = 2^4 - 2^1 = 14
		- M x 14 = M x 2^4 - M x 2^1 = 피승수 M을 왼쪽으로 4번 이동한 값 - 1번 이동한 값
- 하드웨어 구성
	- Q(n+1) : 승수의 두 비트 비교
		> 다음자리도 연속적으로 1인지 확인하는 것이 중요하므로, 별도의 FF존재
		- 승수 비트가 1인 경우
		- 승수 비트가 0인 경우
- Booth 의 곱셈 알고리즘 수행 예

[이미지 자리 : 플로우 차트]
- 배열 승산기
	> 비용이 많이들고 곱셈연산은 시프터와 덧셈만 있으면 되므로 일반적인 cpu에 들어가지는 않음
	- 조합회로에 의한 논리곱 마이크로 연산 수행
	- 2x2배열 승산기
	
		[이미지 자리 : 2x2승산기 회로]
	- 4x3배열 승산기
	
		[이미지 자리 : 4x3승산기 회로]
### 3. 나눗셈 알고리즘(Division Algorithm)
- 이진 나눗셈
	- 하드웨어는 곱셈과 동일
		> EAQ로 결과 비트수 결정 / divider를 위한 카운터 존재
	- 나눗셈 오버플로우 처리
- 나눗셈의 처리
### 4. 부동 소수점 산술 연산(Floating-Point Arithmetic Operations)
### 5. 십진 산술 장치(Decimal Arithmetic Unit)
### 6. 십진 산술 연산(Decimal Arithmetic Operations)
