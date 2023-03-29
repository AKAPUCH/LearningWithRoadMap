# 4장 : 메모리 관리
- 자바나 C#과 달리 메모리를 관리해주는 GC(Garbage Collector)가 없습니다.
- 대신, 객체에 대한 참조를 계산하여 메모리를 관리합니다. (객체를 가리키는 포인터 존재 시 +1, 소멸 시 -1)
- 객체의 참조가 존재 시 메모리에 계속 유지하고, 참조가 없다면 메모리에서 객체를 해제하고 이후 액세스 시 런타임 에러를 발생시킵니다.
- 방법
	- MRC(Manual Reference Counting) : `retain()`, `release()`같은 메서드를 통해 수동으로 참조 횟수를 관리
		- 메서드 종류
			- (id)alloc : 새 인스턴스에 메모리를 할당으로써 RC + 1, 인스턴스 객체에 대한 포인터를 반환한다.
			- (id)retain : 기존 객체를 참조(포인터로 가리킴). 이미 기존 객체를 참조하고 있는 다른 객체가 있을 수도 있다. RC +1, 참조한 객체에 대한 포인터 반환
			- (void)release : 참조를 해제하면서 RC를 1 감소시킨다. 그러나, 해당 (포인터는 소멸되지 않고 존재한다.(dangling pointer)
			- (id)auto release : `@autoreleasepool {}`을 통해서 최종 동작은 release와같으나, RC가 감소하는 시점을 오토 릴리즈 풀 블록이 끝나는 시점까지 미뤄줍니다.
	- ARC(Auto Reference Counting) : GC처럼 참조 횟수를 관리해주는 도우미를 통해 메모리를 관리합니다.
		- 프로젝트 최초 생성시 기본적으로 ARC가 설정되어 있고, 설정에서 비활성화 시킨 후 MRC를 사용할 수도 있습니다.
- RC는 최종 사용 시점 이후에 0으로 유지되어야 한다. 0보다 클 시 메모리 누수(leak), 작을 시 없는 객체에 대한 접근 시도로 런타임 에러가 발생한다.

## 약한 참조

```objective-c
//Person.h 
#import <Foundation/Foundation.h>
 @interface Person : NSObject
 @property (copy) NSString* name;
  @end
  
//Ship.h 
#import <Foundation/Foundation.h>
#import "Person.h"
 @interface Ship : NSObject
 - (Person *)captain;
 - (void)setCaptain:(Person *)theCaptain;
 @end 
 
 //ship.m
 #import "Ship.h"
 @implementation Ship{
  Person* _captain; 
  } 
 - (Person *)captain {
	 return _captain; 
	 } 
 - (void)setCaptain:(Person *)theCaptain {
	  _captain = theCaptain;
	} 

@end
```

- 위의 코드에서 setCaptain 메서드는 `theCaptain`파라미터에 외부 지역변수를 할당받아 Ship 클래스 내에 _captain에 할당합니다.
	- theCaptain은 함수의 파라미터로서 함수 호출 시 메모리의 스택에 할당되었다가 함수가 종료되는 시점에 소멸됩니다.
	- 객체를 가리키는 변수가 함수 블록내에서 생성된 후 다음 행에서 바로 소멸되기 때문에  `discoveryOne` 객체의 참조 카운트는 증가하지 않습니다.
	- 이 때, `theCaptain` 파라미터를 retain을 통해 유지시켜주면, 강한 참조로 만들 수 있습니다.
  
