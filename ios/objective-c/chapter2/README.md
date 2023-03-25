## Objective-C의 타입

|이름|	Objective-c|설명
| ---- | ---- | ---- |
|콘솔 출력|	NSLog	|print|	
|참/거짓	|Bool |%i, 숫자나 “YES”, “NO”등도 담을 수 있음.(조건문에 숫자비교 가능)		
|문자|char/unsinged char|%c는 문자로 받고 ,%i / %u는 숫자로 받는다.		 
|짧은 정수|(unsigned) short int|%hu/%hi, unsigned시 양수로만 범위 2배	
|일반정수|(unsigned ) int|%lu/%i, unsigned시 short와 동일하게 2배
|긴 정수|(unsigned) long int|%lu/%li		
|실수(부정확)|float|%f, 앞 숫자 조작을 통해 표시 자릿수 조절가능 but 부동소수점 방식이라 부정확
|실수(좀 더 정확)|double|%f, 굳이 안써도 인식.

#### 구조체 - 오히려 Obejctive-C에서는 사용을 지양!
````objective-c
typedef struct {
	float x;
	float y;
} Point2D;
````
- typedef : 새로운 데이터 유형 정의 알림
- 구조체는 Foundation 데이터 구조체와 통합은 어렵기 때문에, 지양하고 클래스에 커스텀 데이터 구조를 사용하는걸 권장한다.

#### 배열
- 자체 데이터 유형으로 존재하나 C 언어 타입의 배열에 대한 접근도 제공한다. C언어의 배열은 모두 같은 타입이며 배열의 길이를 정해줘야한다.
- 배열의 요소 수를 자동 결정할 방법이 없어 NSLog() 형식 지정자 또한 존재하지 않는다. -> 서브스크립트로 접근

#### 포인터
- 특정 객체의 메모리 주소(4바이트라고 한다면, 그 첫번째 비트를 가리킴)를 저장하는 변수이다.
- 이것을 통해 포인터 변수에 배열을 할당한다면, 배열의 첫 요소 값을 가리키게 될 것이다.
- 포인터값을 증감시키면서 배열에서 가리키는 요소를 바꿀 수 있다.
- 옵젝씨의 모든 객체는 포인터로 선언된다.
#### void
- swift와 동일하다.
#### nil, null
- 모두 빈 포인터를 의미한다. nil은 옵젝씨, 스위프트에서만 사용되고 c 원시 타입에는 할당할 수 없다. null은 옵젝씨에 할당할 수 있으나 일반적으로 nil을 선호한다.

## Foundation 자료 구조
- 원시타입을 데이터 저장 방법 보다는 앱 작동 방식에 집중할 수 있도록 만든 높은 수준의 추상화된 객체지향도구

#### NSNumber
- 숫자 타입(BOOL, char, short, int, long, float, double)의 컨테이너.
- 내부의 메서드인 numberWIth`원시숫자타입이름`을 사용하여 원시타입을 NSNumber에 저장합니다.
- 접근파라미터 명은 `원시숫자타입이름`Value로 명명되어있습니다.
- 출력시 `%@` 를 사용하여 간단하게 객체를 출력할 수 있습니다.(객체 내부 데이터인 원시타입이 출력됨)
- 단, 불변 타입이기 때문에 저장 값 변경을 원할 시 새 인스턴스를 생성해야 한다.(성능에 큰 무리가 갈 정도는 아님)
- 객체이기 때문에 nil을 활용할 수 있다.

#### NSDecimalNumber
- 고정 소수점(!) 클래스이다. 부동 소수점 방식의 float, double보다 훨씬 정확한 값을 표현할 수 있어 자주 사용된다.
-  `deciamlNumberWIthString` 메서드를 사용한다. 말 그대로 문자열을 고정 소수점의 실수로 만든다.
- 일반적인 숫자와 연산 방식이 틀려 사칙연산을 사용할 수 없다. 대신 메서드로 계산
	- decimalNumberByAdding, decimalNumberBySubtracting, decimalNumberByMultiplyingBy, decimalNumberByDividingBy
	- 반올림 또한 지원한다. NSDecimalNumberHandler를 사용
- 다른 타입으로 변환시, doubleValue로 바꾸는 걸 지양하고 stringValue를 통해 NSString 타입으로 바꾸는 걸 선호한다.
- `참고 : core data 프레임 워크가 NSDecimalNumber의 기본 저장 매커니즘을 제공한다.`

#### NSString
- 불변 문자열 클래스
- length와 characterAtIndex: theIndex 메서드를 이용해 내부 문자 접근 가능. 
- 이외에도 다양한 메서드들이 많이 내장되어 있다.
- 정수의 범위를 나타내는 NSRange를 통해 부분 문자열을 만들어 낼 수 있다.
- `파일의 내용을 직접 읽고 쓰는 기능이 존재`

#### NSMutableString
- 수정이 가능한 문자열 클래스로, 새로운 객체 인스턴스 생성하지 않고도 문자열을 수정할 수 있다.

#### NSArray, MSMutableArray
- NSArray는 불변 Array 객체로, 내부의 데이터는 객체만 가능하다.(원시타입은 불가능)
- NSMutableArray는 NSMutableString처럼 수정가능하므로 `쓰기` 메서드들이 정의되어 있다.
- 메서드는 swift의 메서드들과 이름은 다르지만 기능은 유사하다.
- 내부의 데이터 객체 인스턴스들(NSNumber, NSString 등..)의 메서드들로 원시타입들을 관리할수는 있으나, 그때마다 NS객체를 생성하는건 효율적인 방법이 아니기 때문에 원시타입으로 관리해야 되는 배열에 대해서는 기존 c 배열을 사용하는 것이 바람직하다.

- NSSet, NSDictionary도 존재하나 불변하고 Mutable 키워드가 붙으면 수정이 가능한 클래스라는 점 외에는 swift와 거의 동일하므로 참고만 하자.

### id, Class 데이터 타입
- 클래스 객체 그자체를 지칭하며 변수에 저장 가능하다.
- typeOf 메서드처럼 객체가 어떤 클래스인지 알아낼 수 있다.

## 2장 정리
- Objective-c의 자료형은 기존 C의 원시 타입 + 원시타입을 추상화하여 만든 Foundation 프레임워크
- 성능상으로는 원시타입을 사용하는 것이 우세하나, 편의성 면에서는 추상화한 고수준의 Foundation 우위
