# Tuist 삽질기(Tuist 제거 후 다시 복원하기)

이전에 SwiftUI + TCA 를 이용하여 클론앱을 제작했던 적이 있었습니다.

Tuist도 관심이 있었던 시절이라, Tuist template로 프로젝트를 생성하고 이것저것 개발하던 중, tuist의 설정법이 익숙치않아 배보다 배꼽이 더 큰것 같아서 tuist를 clean 하고 저장소에 push를 한 채로 다시 클론앱을 개발하였었습니다.

그러던 중 개인맥북 판매를 위하여, 맥북 초기화를 진행하여 당근마켓에 등록을 하게 됩니다.

회사 장비에서는 개인프로젝트를 진행하는것이 맞지 않다고 생각해서, 맥북이 팔리면 돈을 좀 더 보태서 m1중고로 사려고 했으나, 장기간동안 팔리지 않아, 다시 맥북에 셋팅을 하게 되었습니다.

개발환경을 셋팅하고, git 저장소에서 해당 프로젝트를 clone 받고나서야 상황이 좋지 않음을 감지하였습니다.😵‍💫

<aside>
😳 최초 Tuist로 생성한 프로젝트에서 .gitIgnore 파일에. xcodeproj파일과 .xcworkspace파일이 등록되어있어, 저장소에는 해당 프로젝트 구성파일이 올라가져있지 않은 상황이었고, tuist관련 설정파일은 clean했기 때문에 다 없어진 상황이었습니다.

</aside>

결국 소스코드 + 리소스 들만 존재하는 (소스폴더 개념) 상태였던 것이죠.

코드양이 크게 많지도 않았고, 프로젝트 전체로 보면 진행도가 매우 초반이었기에 새로 설정해서 옮겨서 하면 그만이었지만, 이런 상황에서 복원해보는것도 경험이겠다 싶어서 진행해보았습니다.

---

- 다행히도 commit history에 tuist 최초 설정시 설정했던 파일을 볼 수 있었기에

```bash
tuist init --platform ios 
```

- 아래 명령으로 만들어지는 구조대로 그대로 폴더 및 파일을 복원해 주었습니다.
- 그리고 나서 tuist generate.. 될리가 없죠.

```bash
Plugin.swift not found at path /Users/xxx/xxxx
```

위 오류가 발생하여 검색해본 결과 Tuist/Config.swift에서의 path문제인것을 알게 되었고 실제 위치하는 path를 찾도록 수정하여 해결하였습니다.

- 그리고 다시 tuist generate.. 역시나 될리가 없죠.

```bash
Dependencies resolved and fetched successfully.
Resolved cache profile 'Development' from Tuist's defaults
`Snapkit` is not a valid configured external dependency for platform ios
Consider creating an issue using the following link: https://github.com/tuist/tuist/issues/new/choose
```

external dependency에 설정된 의존성 라이브러리가 not valid하다는 메시지였습니다.

- 해당 이슈를 찾아보니 tuist fetch 를 먼저 해야한다고 하더군요.
- tuist fetch 이후 tuist generate를 진행하니 드디어 프로젝트가 노출되었습니다만.. 기존에 만들어져있던 소스코드들은 하나도 노출이 되지 않은 말그대로 빈 프로젝트가 오픈되었습니다.

---

> 프로젝트는 살렸는데.. 기존 코드는 나오지 않으면, 프로젝트를 살린 이유가 무었이며, 복원했다 말할 수 있을까? 라는 생각과 함께 다시 이슈트래킹을 시작합니다.
> 

```swift
import ProjectDescription

let project = Project(
    name: "???",
    organizationName: "???",
    targets: [
        Target(
            name: "???",
            platform: .iOS,
            product: .app,
            bundleId: "com.???",
            infoPlist: .extendingDefault(with: [:]),
            sources: ["Sources/**"],
            resources: ["Resources/**"],
            dependencies: [
                .external(name: "SnapKit"),
                .external(name: "ComposableArchitecture"),
                .external(name: "Lottie")
            ]
        ),
        Target(
            name: "???Tests",
            platform: .iOS,
            product: .unitTests,
            bundleId: "com.???",
            infoPlist: .extendingDefault(with: [:]),
            sources: ["Tests/**"],
            dependencies: [
                .target(name: "???")
            ]
        )
    ]
)
```

- project.swift에서 sources,resources 가 없다는 메시지에 대응하기 위해서 빈 Sources폴더와 Resources 폴더를 생성 후에 generate를 했는데, targer에 해당하는 소스와 리소스들의 폴더에 내용물이 없으니 당연히 저렇게 노출될 수 밖엔 없었던 거죠.
- 기존 코드에서 asset 들을 만들어둔 resources 폴더에 넣어주었습니다. (이미지, lottie파일 등등 resource로 사용되어질 것들)
- 기존 코드에서 resource를 뺸 나머지 폴더 및 파일들은 Sources폴더 내로 이동시켜 주었습니다.
- 다시 tuist generate를 수행하였습니다.

![tuistProjectTree.png](/assets/img/blog/fitners/tuistProjectTree.png)

![myf.gif](/assets/img/blog/fitners/myf.gif)

위아래 여백이 갑자기 왜 나오는지 알아보긴 해야겠으나.. 결론은 죽었던 프로젝트를 살려서 빌드까지 성공했다는데에 의미를 두려고 합니다.

---
😁 별거 아닌 이슈였고 해결했습니다~!   
[[보러가기]](https://aske0115.github.io/develop/2023-03-07-swiftui-fullscreen/)

