## 고급 연산자
	 비트연산자, 오버플로우 연산자, 연산자 재정의/선언 등이 있겠다.
- [참고문헌](https://jusung.gitbook.io/the-swift-language-guide/language-guide/26-advanced-operators)
### 비트연산자 : 정수 또는 실수 데이터에 대해 비트단위의 계산을 수행
#### ~
- NOT, 현재 데이터의 비트를 반전시킵니다. 0이면 1, 1이면 0으로 변환
```swift
let initialBits: UInt8 = 0b00001111
let invertedBits = ~initialBits  // equals 11110000
``` 
#### &
- AND, 두 데이터의 비트가 모두 1이면 1, 나머지는 0으로 만듭니다.
```swift
let firstSixBits: UInt8 = 0b11111100
let lastSixBits: UInt8  = 0b00111111
let middleFourBits = firstSixBits & lastSixBits  // equals 00111100
```
#### |
- OR, 두 데이터의 비트 중 1이 하나라도 있다면 1, 나머지는 모두 0으로 만듭니다.
```swift
let someBits: UInt8 = 0b10110010
let moreBits: UInt8 = 0b01011110
let combinedbits = someBits | moreBits  // equals 11111110
```
#### ^
- XOR, 두 데이터의 비트가 같다면 0, 다르면 1로 만듭니다.
```swift
let firstBits: UInt8 = 0b00010100
let otherBits: UInt8 = 0b00000101
let outputBits = firstBits ^ otherBits  // equals 00010001
```
#### <<, >>
- 시프팅, 데이터의 비트를 왼쪽, 오른쪽으로 일정 횟수만큼 이동시킵니다.
- 부호가 없을 경우, 타입의 범위(8,16,32)를 벗어나는 비트는 소멸되고 빈 자리는 0으로 채워집니다.
```swift
let shiftBits: UInt8 = 4   // 00000100 in binary
shiftBits << 1             // 00001000
shiftBits << 2             // 00010000
shiftBits << 5             // 10000000
shiftBits << 6             // 00000000
shiftBits >> 2             // 00000001
```
- 부호가 있을 경우,  벗어나는 비트는 소멸되고, 빈 자리는 부호 비트로 채워집니다.
```swift
let signedValue: Int8 = 0b11000000
let shiftedValue = signedValue >> 2
print(shiftedValue) // 출력 결과: -16이 출력됩니다. (0b11110000)
```
### 오버플로우 연산자
- 정수형, 실수형에서 연산 결과가 예상 타입의 범위를 넘어가는 경우 런타임 에러가 발생합니다.
- 기존 연산자에 &를 붙이면, 에러가 발생하지 않고 오버플로우된 부분은 사라진채로 결과를 반환합니다.
```swift
var signedOverflow = Int8.min
// signedOverflow equals -128, which is the minimum value an Int8 can hold
signedOverflow = signedOverflow &- 1
// signedOverflow is now equal to 127
```
### 연산자 재정의, 커스텀 연산자
- prefix/postfix : 접두,중위, 접미 연산자로 재정의시 func 앞에 붙인다.

```swift
extension Vector2D {
    static prefix func - (vector: Vector2D) -> Vector2D {
        return Vector2D(x: -vector.x, y: -vector.y)
    }
}
```
