# SOLID principles

# SOLID 원칙에 대한 정리

### Swift Code로 돌아보는 SOLID principles를 다뤄보도록 하겠습니다.

---

SOLID 원칙은 객체 지향 소프트웨어 개발을 위한 설계 원칙입니다. SOLID는 다음 다섯 가지 원칙을 나타냅니다.

- 단일 책임 원칙 (Single Responsibility Principle)
- 개방-폐쇄 원칙 (Open-Closed Principle)
- 리스코프 치환 원칙 (Liskov Substitution Principle)
- 인터페이스 분리 원칙 (Interface Segregation Principle)
- 의존성 역전 원칙 (Dependency Inversion Principle)

---

그렇다면 개발자라면 SOLID 원칙을 왜 알고있어야 하며, 개발간에 왜 고민을 해야할까요?

> SOLID 원칙은 객체 지향 소프트웨어 개발을 위한 설계 원칙으로, 유지보수 가능하고 확장성이 높은 소프트웨어를 만들기 위한 지침입니다. 이를 적용하면 코드가 더 깔끔하고 유지보수하기 쉬워지며, 새로운 기능 추가나 변경도 더 쉬워집니다. SOLID 원칙을 이해하면 보다 효율적인 소프트웨어 개발이 가능해지고, 코드의 품질을 향상시킬 수 있습니다.
> 

> 이러한 원칙은 유지보수 가능하고 확장성이 높은 소프트웨어를 만들기 위한 지침입니다.
> 

---

SOLID principles의 각각 항목은 어떤 원칙을 설명하는지 알아보겠습니다.

- **단일 책임 원칙(Single Responsibility Principle)**: 클래스는 한 가지 역할만 해야 합니다. 여러 가지 역할을 수행하면 코드를 유지 관리하고 테스트하기가 어려워집니다. 예를 들면, 네트워크 및 UI 업데이트를 처리하는 클래스는 두 개의 별도 클래스로 분리해야 합니다.
- **개방-폐쇄 원칙(Open-Closed Principle)**: 클래스는 수정하지 않고 확장할 수 있어야 합니다. 새로운 기능을 추가하려면 기존 코드를 변경하지 않아야 합니다. 이는 프로토콜과 확장을 사용하여 구현할 수 있습니다.
- **리스코프 치환 원칙( Liskov Substitution Principle)**: 하위 유형은 기본 유형으로 대체 가능해야 합니다. 부모 클래스에서 상속하는 모든 클래스는 부모 클래스 대신 사용할 수 있어야 합니다. 예를 들어, UIViewController의 하위 클래스는 UIViewController을 사용하는 모든 곳에서 사용할 수 있어야 합니다.
- **인터페이스 분리 원칙(Interface Segregation Principle)**: 클라이언트는 사용하지 않는 인터페이스에 의존하면 안 됩니다. 클래스는 클라이언트가 사용해야 하는 방법과 속성만 노출해야 합니다. 예를 들어, 네트워킹 클래스를 위한 프로토콜은 UI 업데이트와 관련된 방법이 아니라 네트워킹과 관련된 방법만 포함해야 합니다.
- **의존성 역전 원칙(Dependency Inversion Principle)**: 고수준 모듈은 저수준 모듈에 의존하면 안 됩니다. 대신, 둘 다 추상화에 의존해야 합니다. 이는 클래스가 구체적인 구현 클래스 대신 인터페이스 또는 프로토콜에 의존해야 함을 의미합니다. 예를 들어, 네트워킹 클래스는 종속성에 대한 프로토콜에 따라야 하며 특정 구현 클래스가 아니어야 합니다.

---

다음은 각각의 원칙에 대한 swift  예제코드를 살펴보겠습니다.

- **단일 책임 원칙**
    
    단일 책임 원칙은 각 클래스가 한 가지 책임만 가지도록 하는 원칙입니다. 이는 클래스를 단순하고 이해하기 쉽게 만들어 주며, 클래스를 작은 단위로 분리하여 유지보수하기 쉽게 만들어 줍니다.
    
    예를 들어, 네트워크 및 UI 업데이트를 처리하는 클래스는 두 개의 별도 클래스로 분리해야 합니다. 이를 적용한 예제 코드는 다음과 같습니다.
    

```swift
class NetworkManager {
  func fetchData(completion: @escaping ([String]) -> Void) {
    // 네트워크 요청 코드
    // ...
    completion(["data1", "data2", "data3"])
  }
}

class ViewController: UIViewController {
  let networkManager = NetworkManager()

  override func viewDidLoad() {
    super.viewDidLoad()
    fetchData()
  }

  func fetchData() {
    networkManager.fetchData { [weak self] data in
      // UI 업데이트 코드
      // ...
    }
  }
}

```

- **개방-폐쇄 원칙**
    
    개방-폐쇄 원칙은 클래스를 수정하지 않고 확장할 수 있어야 한다는 원칙입니다. 이는 새로운 기능을 추가하려면 기존 코드를 변경하지 않아야 함을 의미합니다.
    
    Swift에서는 프로토콜과 확장을 사용하여 이를 구현할 수 있습니다. 다음은 개방-폐쇄 원칙을 적용한 예제 코드입니다.
    

```swift
protocol DataFetching {
  func fetchData(completion: @escaping ([String]) -> Void)
}

class NetworkManager: DataFetching {
  func fetchData(completion: @escaping ([String]) -> Void) {
    // 네트워크 요청 코드
    // ...
    completion(["data1", "data2", "data3"])
  }
}

class CacheManager: DataFetching {
  func fetchData(completion: @escaping ([String]) -> Void) {
    // 캐시 데이터 요청 코드
    // ...
    completion(["cachedData1", "cachedData2", "cachedData3"])
  }
}

class ViewController: UIViewController {
  let dataFetcher: DataFetching

  // 새로운 데이터 소스 추가
  init(dataFetcher: DataFetching = NetworkManager()) {
    self.dataFetcher = dataFetcher
    super.init(nibName: nil, bundle: nil)
  }

  required init?(coder: NSCoder) {
    fatalError("init(coder:) has not been implemented")
  }

  override func viewDidLoad() {
    super.viewDidLoad()
    fetchData()
  }

  func fetchData() {
    dataFetcher.fetchData { [weak self] data in
      // UI 업데이트 코드
      // ...
    }
  }
}

```

- **리스코프 치환 원칙**
    
    리스코프 치환 원칙은 하위 유형은 기본 유형으로 대체 가능해야 한다는 원칙입니다. 즉, 부모 클래스에서 상속하는 모든 클래스는 부모 클래스 대신 사용할 수 있어야 합니다.
    
    예를 들어, UIViewController의 하위 클래스는 UIViewController을 사용하는 모든 곳에서 사용할 수 있어야 합니다. 이를 적용한 예제 코드는 다음과 같습니다.
    

```swift
class CustomViewController: UIViewController {
  // CustomViewController에 대한 추가적인 로직
}

class MyViewController: UIViewController {
  let customViewController = CustomViewController()

  override func viewDidLoad() {
    super.viewDidLoad()
    present(customViewController, animated: true, completion: nil)
  }
}

```

- **인터페이스 분리 원칙**
    
    인터페이스 분리 원칙은 클라이언트가 사용하지 않는 인터페이스에 의존하지 않도록 하는 원칙입니다. 이를 위해 클래스는 클라이언트가 사용해야 하는 방법과 속성만 노출해야 합니다.
    
    예를 들어, 네트워킹 클래스를 위한 프로토콜은 UI 업데이트와 관련된 방법이 아니라 네트워킹과 관련된 방법만 포함해야 합니다. 이를 적용한 예제 코드는 다음과 같습니다.
    

```swift
protocol NetworkFetching {
  func fetchData(completion: @escaping ([String]) -> Void)
}

class NetworkManager: NetworkFetching {
  func fetchData(completion: @escaping ([String]) -> Void) {
    // 네트워크 요청 코드
    // ...
    completion(["data1", "data2", "data3"])
  }
}

class ViewController: UIViewController {
  let networkFetcher: NetworkFetching

  // NetworkFetching 프로토콜에 대한 의존성 주입
  init(networkFetcher: NetworkFetching = NetworkManager()) {
    self.networkFetcher = networkFetcher
    super.init(nibName: nil, bundle: nil)
  }

  required init?(coder: NSCoder) {
    fatalError("init(coder:) has not been implemented")
  }

  override func viewDidLoad() {
    super.viewDidLoad()
    fetchData()
  }

  func fetchData() {
    networkFetcher.fetchData { [weak self] data in
      // UI 업데이트 코드
      // ...
    }
  }
}

```

- **의존성 역전 원칙**
    
    의존성 역전 원칙은 고수준 모듈은 저수준 모듈에 의존하면 안 되며, 둘 다 추상화에 의존해야 한다는 원칙입니다. 이를 위해 클래스가 구체적인 구현 클래스 대신 인터페이스 또는 프로토콜에 의존해야 합니다.
    
    예를 들어, 네트워킹 클래스는 종속성에 대한 프로토콜에 따라야 하며 특정 구현 클래스가 아니어야 합니다. 이를 적용한 예제 코드는 다음과 같습니다.
    

```swift
protocol DataFetching {
  func fetchData(completion: @escaping ([String]) -> Void)
}

class NetworkManager: DataFetching {
  func fetchData(completion: @escaping ([String]) -> Void) {
    // 네트워크 요청 코드
    // ...
    completion(["data1", "data2", "data3"])
  }
}

class CacheManager: DataFetching {
  func fetchData(completion: @escaping ([String]) -> Void) {
    // 캐시 데이터 요청 코드
    // ...
    completion(["cachedData1", "cachedData2", "cachedData3"])
  }
}

class ViewController: UIViewController {
  let dataFetcher: DataFetching

  // DataFetching 프로토콜에 대한 의존성 주입
  init(dataFetcher: DataFetching = NetworkManager()) {
    self.dataFetcher = dataFetcher
    super.init(nibName: nil, bundle: nil)
  }

  required init?(coder: NSCoder) {
    fatalError("init(coder:) has not been implemented")
  }

  override func viewDidLoad() {
    super.viewDidLoad()
    fetchData()
  }

  func fetchData() {
    dataFetcher.fetchData { [weak self] data in
      // UI 업데이트 코드
      // ...
    }
  }
}

```

---

SOLID 원칙은 유지보수 가능하고 확장성이 높은 소프트웨어를 만들기 위한 지침입니다. 이를 Swift 코드에 적용하면 코드를 이해하기 쉽고 유지보수하기 쉬운 소프트웨어를 만들 수 있습니다.
