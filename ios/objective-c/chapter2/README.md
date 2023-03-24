## Objective-C의 타입 : C의 원시 타입들을 계승한다고 보면 된다.

|이름|	Objective-c|설명
| ---- | ---- | ---- |
|콘솔 출력|	NSLog	|print|	
|참/거짓	|Bool |%i, 숫자나 “YES”, “NO”등도 담을 수 있음.(조건문에 숫자비교 가능)		
|문자|char/unsinged char|%c는 문자로 받고 ,%i / %u는 숫자로 받는다.		 
|짧은 정수|(unsigned) short int|%hu/%hi, unsigned시 양수로만 범위 2배	
|일반정수|(unsigned ) int|%lu/%i, unsigned시 short와 동일하게 2배
|긴 정수|(unsigned) long int|%lu/%li		
|실수(부정확)|float|%f, 앞 숫자 조작을 통해 표시 자릿수 조절가능 but 부동소수점 방식이라 부정확
|실수(좀 더 정확)|short|%f, 굳이 안써도 인식.
