# ios 앱의 생명주기

## 참고 문헌
- [애플 공식 문서 - 앱 라이프 사이클 관리](https://developer.apple.com/documentation/uikit/app_and_environment/managing_your_app_s_life_cycle/#2928645)

## 개요
ios에서는 앱의 현재 상태에 따라 작업의 우선순위가 정해져 있습니다. 

	1순위 : 현재 foreground(background의 반대개념)에 위치한 앱
	2순위 : 시스템 리소스
	3순위 : 현재 background에 위치한 앱
		 
iOS 12 이하에서는  UIApplicationDelegate 객체가, iOS 13 이상부터는 UISceneDelegate 객체가 라이프 사이클 이벤트에 대응 및 관리하게 됩니다.

	ios 13이상에서도 UIApplicationDelegate 객체를 사용할 수 있으나, 
	default는 UISceneDelegate 객체로 설정되어 있습니다.

## Scene 기반 라이프 사이클 이벤트 대응
scene은 여러 개가 존재하며 각각 다른 상태(백그라운드, foreground..)에 있을 수 있습니다. 
재밌게도 ios 13이상에서 라이프 사이클 관리는 UISceneDelegate가 기본으로 설정되어 있으나 Scene 지원 자체는 선택 사항입니다. 활성화를 위해서는 Info에 `UIApplicationSceneManifest` 키를 추가해줘야 합니다.

![scene의 생명주기](https://user-images.githubusercontent.com/116094622/230723552-47acb0b1-b09c-428a-a352-15aac66baf8c.png)
그림으로 표현된 Scene 생명주기의 상세 과정은 다음과 같습니다.
1. 사용자 or 시스템의 scene 요청
2. UIkit이 생성 후 Unattached 상태로 유지
3. 사용자 요청 -> foreground로 이동, 시스템 요청 -> background로 이동
4. 앱 종료시 scene을 background로 이동 후 최종적으로 일시중지시킴(Suspended)

Unattached 상태를 제외하면 모두 리소스를 소모하며(Suspend 포함) 필요시 UIKit이 회수하여 Unattached상태로 만듭니다.

Scene의 상태를 넘나들 때 일어나는 조금 더 구체적인 동작들을 살펴봅시다.
<div>
<details>

1. Unattached 상태의 Scene을 앱에 연결하면 Scene의 UI 초기 설정 후 필요한 데이터를 가져옵니다.
2. foreground-active 상태로 전환을 시도할 때, UI를 다시 설정하고 사용자와 상호작용할 준비를 합니다.
2-1. foreground 진입시 앱의 데이터 모델 업데이트

		먼저 Scene을 foreground-Inactive 상태로 전환시킵니다.
		active상태가 되기 전 준비단계라고 생각하시면 될 것 같습니다. 
		만약 scene이 unattached가 아닌 background 상태라면 `sceneWillEnterForeground(_:) `  메서드를 통해 전환시킬 수 있습니다.
		이후 리소스들을 로드하고 네트워크에서 데이터를 가져옵니다.
	2-2. 활성화 시 사용자 인터페이스 및 초기 작업 구성
	
		 UI를 표시하기 직전에 상태를 active로 전환합니다. 활성 상태에서는 ui 및 런타임 동작을 설정합니다.
		 SceneDidBecomeActive(_:) 메서드 내부에서 해당 동작들에 대한 로직을 처리하게 됩니다.
		 활성화는 UI 준비를 마무리하는 시간이기도 하기 때문에 활성화를 차단시키는 로직을 구현해서는 안됩니다.
	2-3. 뷰가 나타날 때 UI 관련 작업 시작
	
		활성화 방법(SceneDidBecomeActive)이 반환되면 UIKit은 모든 Scene을 표시합니다. 
		또 Scene의 뷰 컨트롤러에서 viewWillAppear(_:) 메서드를 사용하여 UI 최종 업데이트를 수행합니다. 	
3. foreground-active 상태에서 벗어날 때, 데이터를 저장하고 앱의 동작을 최소화할 준비를 합니다.
	3-1. 비활성화 시 앱의 동작 최소화
	
		백그라운드로 이동 전 active 상태를 Inactive 상태로 변경시키고, sceneWillResiginActive(_:) 메서드를 호출합니다. 메서드 내에서 사용자 데이터를 저장하고 모든 작업들을 중지시켜 앱을 가능한 '조용하게' 만듭니다.
	3-2. 백그라운드 진입시 리소스 해제

		백그라운드에 진입하면서 sceneDidEnterBackground(_:) 메서드를 호출하고, 
		앱의 공유 리소스 연결을 모두 해제하고 메모리에서도 해제시킵니다. 

	3-3. 앱 스냅샷을 위한 UI 준비
	
		백그라운드에 진입하고 UISceneDelegate 객체가 반환된 후 현재 UI에 대한 스냅샷을 찍습니다.
		스냅샷은 app switcher에 표시되고 foreground로 재전환될 시 일시적으로 표시하는데 쓰입니다.
		또 불필요한 객체나 민감한 정보가 UI에 포함되어 있다면 해제 및 제거해줍니다.
		어차피 foreground로 진입 준비를 하는 과정에서 새로 세팅해주기 때문에 걱정할 필요 없습니다.
	3-4. 백그라운드에서 중요 이벤트에 대한 처리
	
		일반적으로 백그라운드에서는 앱의 동작을 최소화하려고 하지만, 일부 기능에 한해 지원합니다.
		
			AirPlay 또는 Picture in Picture 비디오를 사용한 오디오 통신.
			위치 기반 서비스.
			VoIP.
			외부 액세서리와의 통신.
			Bluetooth LE 액세서리와의 통신
			서버 정기 업데이트
			APN(Apple 푸시 알림 서비스)
4. Scene 관련 이벤트 외에도 UIApplicationDelegate 객체를 사용한 앱의 실행에 대해서도 대응해야 합니다.
	4-1. 초기 스토리보드 제공(단, ios 14부터 첫 화면에서 정적 이미지 사용시 25MB미만 이어야 합니다. )
	4-2. application(_:willFinishLaunchingWithOptions:) 또는 application(_:didFinishLaunchingWithOptions:)를 앱 빌드시 호출했을 때 앱의 데이터를 초기화 시켜주도록 내부 로직을 구현합니다.
	4-3. 이 때 앱의 실행을 지연시킬 수 있는 작업은 비동기로 처리하거나 다른 쓰레드로 이동시킵니다.
	4-4. application(_:configurationForConnecting:options:)를 통해 scene을 생성한 목적을 application(_:willFinishLaunchingWithOptions:)에 전달합니다.
</details>
</div>

## app 기반 라이프사이클 대응
![앱](https://user-images.githubusercontent.com/116094622/230769328-21457bf7-9df8-4c9d-b950-f0a217ee00c0.png)
Unattached상태가 Not Running으로 대체된 것 외에는 크게 다르지 않습니다.
호출되는 메서드의 종류만 조금 달라졌을 뿐, 전체적인 틀인 같다고 보면 될 것 같습니다.
		
		