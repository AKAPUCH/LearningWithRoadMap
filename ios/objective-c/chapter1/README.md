## 1장 : 기초 문법

- 이상한 문법 : 개체에 바인딩된 메서드를 호출하는 대신 객체 to 객체 메시지 전송을 통한 동작
-  C의 상위 언어로 설계되어 c, c++과 상호 호환된다. **(Swift는 c++ 라이브러리를 사용 불가!)**
```objective-c
person.sayHello(); // C#의 방법
[person sayHello]; // Objective-C의 방법. 옵젝씨에서의 용어는 메서드 호출이 아닌 "메시지 보내기"
```

- objective-c 단일은 .m, 다른 c와 혼재된 파일은 .mm의 확장자를 가진다. .h확장자 파일은 헤더파일로, .m파일 클래스의 인터페이스를 제공한다.(자바의 인터페이스-구현체(클래스) 관계)
- 문자열은 큰따옴표 전 @를 반드시 붙인다.
- 콘솔 출력 메서드 `NSLog()` 
- Foundation 프레임워크에서 기본 구조를 정의한다. -> 거의 필수적으로 Foundation을 import `#import <Foundation/Foundation.h>
- 모든 메서드와 속성은 @end 앞에서 선언된다. -> @end가 클래스의 끝!
- .m 파일의 import는 로컬 헤더의 경우 큰따옴표, 글로벌 헤더 파일의 경우 대괄호로 표기한다. `#import "Person.h"` 
- .m 파일의 이름 앞에는 `@implementation`, .h파일의 이름 앞에는 `@Interface` 어노테이션이 붙는다.
- 함수의 기본 선언 형태 : `- (반환타입)함수이름:(파라미터타입 *)파라미터이름 {};`
- 다른 C 계열처럼 main()에서 빌드 가능하기 때문에 main.m 파일에서 만든 메서드를 호출한다.
- 변수 선언시 포인터를 활용해 해당 타입(클래스)의 인스턴스를 보유할 것을 알린다. `Person* somePerson` 
- 대괄호와 alloc, init을 통해 인스턴스를 생성합니다. `[Person alloc] init]`
- Swift의 String.format처럼, %@를 통해 변수를 문자열에서 받을 수 있습니다.
- 메시지 전송시 파라미터가 있다면 `[인스턴스이름 함수이름:파라미터에 넣을 변수];` 처럼 표기합니다.
- 프로퍼티는 인터페이스에서 `@property(동작)타입 *이름;` 과 같이 선언됩니다.
- 이후 구현체에서 `@synthesize 프로퍼티명 = 인스턴스변수명;` 을 통해 인스턴스 변수명으로 프로퍼티에 접근할 수 있습니다.
- 또, `set프로퍼티명, get프로퍼티명` 메서드를 통해 해당 프로퍼티의 getter/setter 동작을 할 수 있습니다.


```objective-c
//Person.h
#import <Foundation/Foundation.h>

@interface Person : NSObject
@property (copy)NSString *name;
-(void)sayHello;
- (void)sayHelloToName:(NSString *)aName;
@end

//Person.m
#import "Person.h"

@implementation Person
@synthesize name = _name;
-(void)sayHello{
    NSLog(@"Hello, my name is HAL.");
}
- (void)sayHelloToName:(NSString *)aName {
    NSLog(@"Hello %@, my name is HAL.", aName);
}
@end
```

