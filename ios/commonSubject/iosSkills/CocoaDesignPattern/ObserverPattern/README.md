# 옵저버 패턴

## 구조 및 동작
### 동작 
- model의 특정 데이터를 뷰와 연결하고 변화가 발생했다면 데이터를 업데이트한 후 업데이트 된 데이터를 뷰에도 갱신합니다.

### 구조
![observer](https://user-images.githubusercontent.com/116094622/236803608-dd614f07-7692-4a9a-affa-94914fae46c1.png)

- subscriber : value의 변화마다 값을 갱신받고 싶은 view의 객체입니다.
- publisher : subscriber(view의 객체)의 사용자 상호작용에 따른 변화를 모델의 value에 반영하여 업데이트하고 view의 값을 갱신합니다.
- value : 현재 관찰하고 있는 값입니다. 실시간으로 변화가 반영됩니다.

## MVC에서의 사용예시
### Model
- Combine 프레임워크를 import합니다.
- 변화를 관찰하고 싶은 모델의 프로퍼티에 `@published` prefix를 붙입니다.
- publisher 속성에 영향을 주는 다른 속성들의 속성감시자를 설정하고 변화시마다 publisher를 갱신하도록 합니다.

### View
- Combine 프레임워크를 import합니다.
- AnyCancellable? 타입으로 subscriber 속성을 만듭니다.

### ViewController
- subscriber 속성과 publisher를 연결합니다.
- Combine 프레임워크의 메서드를 활용하여 여러가지 설정이 가능합니다.
  - `receive()` : 작업이 일어날 대기열(main,global) 지정
  - `map()` : 가공하여 subscriber에 전달할 value의 형태 지정
  - `assign()` : value가 표시될 객체 지정
