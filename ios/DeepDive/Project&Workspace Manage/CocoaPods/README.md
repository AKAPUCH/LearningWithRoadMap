# Cocoapods

## 참고문헌

- [Cocoapod 입문 kodeco](https://www.kodeco.com/7076593-cocoapods-tutorial-for-swift-getting-started)
- [Cocoapod vs SPM](https://medium.com/@rashadsh/cocoapod-vs-spm-in-swift-2fe52764b31a)
- [Xcode 14.3 에러 대응](https://lxxyeon.tistory.com/208)
## 사용 목적
### 의존성 관리
- app을 만들 때, 우리는 편의성을 위해 애플에서 제공해주는 모듈들 외에 외부 라이브러리를 사용합니다.
- 이러한 라이브러리들은 창작자에 의해 계속해서 수정되고 변화하기 때문에 그때마다 내 앱에서의 소스를 변경하는건 불편합니다.
- 이러한 라이브러리, 즉 의존성들을 Cocoapods, SPM(Swift Package Manager), Carthage 같은 패키지 매니저로 관리할 수 있습니다.

## 특징
### 장점
- 모든 Apple 플랫폼(iOS, tvOS, watchOS, macOS)을 지원하고, 대부분의 프레임워크에서 지원됩니다.
- 공식 [홈페이지](uides.cocoapods.org)가 있고, 사용할 수 있는 의존성들이 잘 정리되어 있습니다.
- 동적 프레임워크와 정적 라이브러리를 모두 지원합니다(up to 1.5.0 version)
- 앱의 의존성 관리를 위한 Mac 프로그램이 존재합니다.
- 앱의 의존성을 다른 사람들에게 쉽게 공개 가능하고 사용 전 `pod try 라이브러리명`으로 해당 의존성을 테스트 가능합니다.
### 단점
- pod update 또는 pod install시 시간이 오래 걸립니다.
- 기본 프로젝트의 형태가 변경될 수 있습니다.(반드시 workspace에서 작업하도록 변형됨) -> xcodeproj로 빌드시 오류발생
- 프로젝트 빌드시마다 모든 의존성이 함께 빌드되어 더 많이 시간이 소요됩니다.

## 간단한 사용법
### 최초 설치
1. 터미널에서 `brew install cocoapods` 또는 `sudo gem install cocoapods` 실행 (위치 상관 ❌)
2. brew가 아닌 gem으로 설치를 진행한다면 `pop setup --verbose` 명령어 추가로 실행
### 내 프로젝트(앱)에 적용
1. 터미널에서 xcodeproj 파일이 존재하는 경로로 이동
2. `pod init` 실행
3. `open -a Xcode Podfile` 명령어 실행을 통해 생성된 Podfile 열기
  - 기본 텍스트 에디터로 편집시 보이지 않는 쓰레기 값이 삽입될 수 있어 반드시 Xcode에디터로🙏🏻
4. Ruby로 언어로 작성된 # 주석들 제거, `platform:`부분은 #만 제거하여 적용

### 의존성 추가 방법
1. 아래 코드 주석 부분에 `pod '라이브러리 명', '버전'` 코드를 추가하면 됩니다. 

```Ruby
platform : ios, '버전'

target '프로젝트명' do
  use_frameworks!
  # 여기에 가져올 의존성 작성
  
end
```

2. 저장 후, Podfile 디렉토리에서 터미널을 열어 pod install 또는 pop update 명령어 입력
3. 이제 원하는 파일에서 `import 라이브러리`후 사용하면 됩니다😁

## ETC..
### 버전 명시법
- `1.2.3`이라는 알 수 없지만 대충 버전을 의미하는 것 같은 수를 본 적이 있나요? 각 숫자는 다음과 같습니다.
  #### major
  - 첫 숫자 `1`은 앱의 major version number로, 메이저 버전은 이전 버전과 호환되지 않는 수정사항이 포함될 수 있습니다.
  #### minor
  - 두번째 숫자 `2`는 앱의 minor version number로, 새로운 기능이 추가되지만 이전 버전과 호환이 가능한 버전입니다.
  #### patch
  - 세번쨰 숫자 `3`은 앱의 patch version number로, 기존 기능의 버그 픽스는 존재하나 동작의 변경이나 새 기능 추가는 없는 버전입니다.
  #### 규칙
  - 다음 버전이 릴리즈될 때, 하위 번호는 모두 0으로 초기화됩니다.
  
      - ex1) 1.3.4 버전에서 이전과 호환되는 새 기능이 추가된 버전 릴리즈 -> 마이너 버전이므로 1.4.0으로 네이밍
      - ex2) 3.7.3 버전에서 이전과 호환되지 않는 새 버전 출시 -> 메이저 버전이므로 4.0.0으로 네이밍
      - ex3) 1.1.3 버전에서 버그가 수정된 버전 릴리즈 -> 패치 버전으로 1.1.4 네이밍
      
### 관련 에러 대응
- Xcode 14.3 에서 CocoaPod 설치 후 File not Found 에러 및 Linker failed 에러 발생시 podfile에 아래 코드 추가
```Ruby
post_install do |installer|
    installer.generated_projects.each do |project|
          project.targets.each do |target|
              target.build_configurations.each do |config|
                  config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '13.0'
               end
          end
   end
end

