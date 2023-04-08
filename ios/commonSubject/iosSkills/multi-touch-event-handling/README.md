# 멀티터치 이벤트 핸들링

## 참고 링크
- [멀티터치 앱 구현하기_애플공식문서](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/handling_touches_in_your_view/implementing_a_multi-touch_app)

## 예시
### 구현할 내용
간단한 가이드가 적힌 레이블과 멀티 터치를 일어날 뷰로 이루어진 뷰 컨트롤러를 구현합니다.

![공식문서예시](https://user-images.githubusercontent.com/116094622/230618363-e949cd86-6269-455e-99c5-094b6e4f4563.png)

뷰에 터치가 감지되면 100*100 크기의 작은 원형 회색 뷰가 생성되며, 손을 떼면 소멸합니다. 멀티 터치 구현이 목적이기 때문에 터치되는 모든 부분에 뷰가 생성되어야 합니다.

### 상세 구현
구현이 이뤄질 최상위 뷰의 이름은 `TouchableView`입니다. UIView는 기본적으로 UIResponder 프로토콜을 상속하여 그 내부에 터치와 관련된 메서드들을 사용하여 터치이벤트를 조작할 수 있습니다.

	touchesBegan(_:with:) 터치가 시작될 때 호출됩니다.
	touchesMoved(_:with:) 사용자가 터치한 부분을 이동할 때 호출됩니다.
	touchesEnded(_:with:) 터치가 끝날 때 호출됩니다.

해당 메서드들의 파라미터로 `touches`가 들어오고, `Set<UITouch>` 타입이기 때문에 멀티 터치시 모든 UITouch 객체들을 포함하고 있습니다.
우리는 반복문을 순회하면서 각 메서드마다 원하는 구현을 해주면 될 것입니다.

	touchesBegan(_:with:) 뷰를 만드는 메서드를 호출합니다
	touchesMoved(_:with:) 현재 UITouch 객체의 location을 가져와 view의 위치에 할당합니다.
	touchesEnded(_:with:) 뷰를 소멸시키는 메서드를 호출합니다.

예시 코드

```swift
class TouchableView: UIView {
   var touchViews = [UITouch:TouchSpotView]() 
 
   override init(frame: CGRect) {
      super.init(frame: frame)
      isMultipleTouchEnabled = true
   }
 
   required init?(coder aDecoder: NSCoder) {
      super.init(coder: aDecoder)
      isMultipleTouchEnabled = true
   }
 
   override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
      for touch in touches {
         createViewForTouch(touch: touch)
      }
   }
 
   override func touchesMoved(_ touches: Set<UITouch>, with event: UIEvent?) {
      for touch in touches {
         let view = viewForTouch(touch: touch) 
         // Move the view to the new location.
         let newLocation = touch.location(in: self)
         view?.center = newLocation
      }
   }
 
   override func touchesEnded(_ touches: Set<UITouch>, with event: UIEvent?) {
      for touch in touches {
         removeViewForTouch(touch: touch)
      }
   }
 
   override func touchesCancelled(_ touches: Set<UITouch>, with event: UIEvent?) {
      for touch in touches {
         removeViewForTouch(touch: touch)
      }
   }
  
   // Other methods. . . 
}
```

아래는 UIResponder 메서드들 내부에서 호출했던 메서드들의 상세 구현입니다. UITouch 객체들을 저장했던 딕셔너리에서 하나씩 꺼내어 뷰를 생성, 위치 변경 또는 소멸시켜주고 있습니다.
```swift
func createViewForTouch( touch : UITouch ) {
   let newView = TouchSpotView()
   newView.bounds = CGRect(x: 0, y: 0, width: 1, height: 1)
   newView.center = touch.location(in: self)
 
   // Add the view and animate it to a new size.
   addSubview(newView)
   UIView.animate(withDuration: 0.2) {
      newView.bounds.size = CGSize(width: 100, height: 100)
   }
 
   // Save the views internally
   touchViews[touch] = newView
}
 
func viewForTouch (touch : UITouch) -> TouchSpotView? {
   return touchViews[touch]
}
 
func removeViewForTouch (touch : UITouch ) {
   if let view = touchViews[touch] {
      view.removeFromSuperview()
      touchViews.removeValue(forKey: touch)
   }
}
```
마지막으로 각 터치마다 생성되는 뷰 클래스입니다. 계산속성 bounds를 통해 원형을 유지하고 있습니다.
```swift
class TouchSpotView : UIView {
   override init(frame: CGRect) {
      super.init(frame: frame)
      backgroundColor = UIColor.lightGray
   }
 
   // Update the corner radius when the bounds change.
   override var bounds: CGRect {
      get { return super.bounds }
      set(newBounds) {
         super.bounds = newBounds
         layer.cornerRadius = newBounds.size.width / 2.0
      }
   }
}
```

## 마치며..
단일 터치에 비해 굉장히 어려울 것으로 예상되었으나, 
UIResponder가 멀티 터치를 모두 감지해주기 때문에 저희는 `Set<UITouch>` 형태로 저장된 UITouch 객체들에 대해 로직을 모두 적용시켜 주면 되는 간단한 내용이었습니다. 