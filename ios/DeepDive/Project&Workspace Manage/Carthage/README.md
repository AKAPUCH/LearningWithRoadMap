# Carthage
## 참고문헌
- [carthage tutorial kodeco](https://www.kodeco.com/7649117-carthage-tutorial-getting-started)
## 특징
### 장점
- CocoaPods과의 비교 : 프로젝트를 변경하거나 특정 공간(Podspecs)에서만 작업하도록 강제하지 않습니다.
- SPM과의 비교 : SPM은 블랙박스형 라이브러리 사용에 부적합합니다.
  - SPM은 공유시 소스코드 외의 빌드된 바이너리 파일을 공유하는 것을 지원하지않습니다.
  - 만약 소스코드 공개를 원치않는 라이브러리를 공유하고 싶다면 Cocoapods이나 Carthage를 사용해야합니다.
  - 공유된 framework에 소스코드 추가를 허용하나, 이미지나 다른 데이터파일은 불가능합니다.
### 단점
- 정적 라이브러리는 지원하지 않는다. -> ios버전 최소 8이상을 요구합니다.

## 사용법
### 설치
- xcodeproj 파일의 경로에서 `touch Cartfile` 명령어 실행
- 텍스트 에디터가 아닌 IDE 에디터(vscode, vim, xcode...)로 Cartfile 열기
- Cartfile에 `github "레포지토리 주인명/ 레포지토리 이름" 연산자 버전` 코드 작성 -> 라이브러리 넣기
  - 또는 `git "clone url" ` 해도 상관❌
- `carthage update --platform 타겟플랫폼` 명령어 실행 -> 플랫폼 미명시시 모든 플랫폼의 라이브러리를 가져옵니다

## 관리 구조
### Cartfile.resolved
- 현재 프로젝트에 설치되어 있는 의존성들의 버전 정보가 명시되어 있습니다. 커밋에 포함시키는 것이 작업에 편합니다.
### Carthage
#### Build 폴더
- 각 의존성에 대해 빌드된 프레임워크가 포함되어 있습니다. 이를 통해 쉽게 프로젝트에 의존성을 적용시킬 수 있습니다.
- carthage는 프레임워크 빌드시 소스코드 또는 깃허브의 실제 프로젝트를 사용합니다.
#### Checkouts 폴더
- carthage가 각 의존성에 대한 프레임워크를 빌드하기 위한 소스코드가 포함되어 있습니다.
- 캐시 저장소의 일종으로, 변경사항이 없는한 원본 저장소에서 같은 코드를 계속 가져올 필요가 없어집니다.

