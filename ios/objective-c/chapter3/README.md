##  속성
- `인스턴스명.프로퍼티 명` 이런 식으로 접근가능
### 선언
```objective-c
@property (copy) NSString *name;
@property unsigned int age;
```
- `copy`는 속성에 접근할 때 수행할 작업을 런타임에 알려주는 역할을 한다.
- `@synthesize`를 통해 쉽게 변수에 접근할 수 있다.(getter, setter가 쉽게 만들어진다.)
- Foundation 유형이 아닌 원시 타입으로 선언시, 포인터 변수를 사용하지 않아도 된다!

### 인스턴스 변수(ivar)
- 클래스 내부에서 선언되는 변수 = swift의 전역변수
- 접근제한자(@private, @protect..)를 붙혀 접근 범위 제한 가능
	- 단, public으로 설정된 변수는  Objective-c 표준이 아니기 때문에 클래스를 C 구조체처럼 작동하게 만든다..
```objective-c
@interface Person : NSObject {
	@private
		NSString *_ssn;
	@protected
		unsigned int _age;
	@public
		NSString *job;
}

Person *frank = [[Person alloc] init];
frank -> job = @“Astronaut”; // [frank job]이 불가능하다.
NSLog(@“%@“, frank->job);
```

- @implemented에 선언된 인스턴스 변수는 private로 최초 설정된다. (@interface는 protected가  default)

### Accessors
- 접근자 메서드는 속성 선언 특성을 부여가능하다.
- 종류
	-getter = getterName : 미설정시 `get속성이름`
	- setter = setterName : 미설정시`set속성이름`
	- read only : getter만 가능하도록 만든다.
	- monatomic : thread-safe하지 않도록 만드는 것을 의미한다. 멀티 쓰레딩 환경이 아니라면 monatomic 속성이 기본 속성보다 더 빠르다.  속성은 기본적으로 thread-safe하나, 멀티 쓰레딩 환경에서 무결성을 보장하지 않고 getter, setter가 안전하다는 뜻이다.
- 쉼표 구분자를 통해 한번에 여러가지 적용 가능하다.
