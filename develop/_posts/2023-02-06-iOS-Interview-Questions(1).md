---
layout: post
title: iOS Interview Question Part1

---


* iOS Tech Interview에서 자주 나오는 질문들에 대한 모음집입니다.   
  
  > [참고사이트](https://chetan-aggarwal.medium.com/ios-interview-questions-part-1-differentiate-99e8f574a3f1)   
  
  > 위 링크를 참고하여 한글로 풀어 설명하고, 추가적인 설명은 덧붙히고, 불필요해 보이는 것은 제거하려고 합니다.   
  

## iOS Interview Question Part1   

**Q : Categoty VS Protocol**
- Category : 기존에 생성되어 있는 Class들을 상속하지 않고, 메소드(기능)을 확장하기 위하여 사용합니다.   
  - Inheritance(상속) 과의 차이점은 Category는 객체를 변형하지 않은 채로 메소드(기능)을 확장가능하지만   
    상속은 Subclassing을 통하여 새로운 기능을 추가합니다.   
  - 또한 상속은 Subclassing을 통해 새로운 Property도 추가할 수 있습니다.   
     _- 기본적으로는 Category에 Property추가가 불가하지만, AssociatedObject를 사용하면 Category의 property 추가도 가능합니다._

 
~~~objc
 @interface NSString (URL)
 - (BOOL)isHTTPProtocol;
 @end
 
 @implementation NSString (URL)
 - (BOOL)isHTTPProtocol {
    return [[self lowercastString] hasPrefix:@"http://"] || [[self lowercastString] hasPrefix:@"https://];
 }
 
 
 //사용예
 [@"https://aske0115.github.io" isHTTPProtocol];

~~~     

- Protocol : 필요한 기능을 묶어서 명시하고, 해당 프로토콜을 따르는 객체에서는 해당 프로토콜에 선언된 함수들을 처리합니다.
  + 반드시 처리해야 하는 함수들은 @required 로 묶어서 나열합니다 (기본값은 required입니다.)
  + 필요에 따라 처리해도 되고 안해도 되는 함수들은 @optional 키워드 아래에 나열합니다.
   
~~~objc
 @protocol Loggable <NSObject>
 @required
  - (void)trackingObject:(id object);
 @optional
  - (void)dumpLog;
 @end
 
 
 @interface LoggableView: UIView <Loggable>
 @end
 
 @implementation LoggableView {
  - (void)trackingObject:(id object) {
  
  }
  
  - (void)dumpLog {
  
  }
~~~   

---
**Q : Delegate VS Notifications**
- Delegate : Delegate는 클래스 사이의 1:1의 연결관계를 맺고, 서로 데이터들을 주고받거나     
             이벤트 처리에 대한 위임을 통하여 이벤트를 처리할 수 있습니다.   
             (ex : UITableViewDelegate, UIScrollViewDelegate, UICollectionViewDelegate..datasource..등등)   
  
- Notifications : Broadcasting과 같은 형태로 사용되며 발신자와 수신자는 긴밀한 관계를 가지지 않습니다.   
  +  발신자는 수신자가 누구인지, 있는지 없는지, 몇명이나 있는지에 대한 확인은 하지 않습니다.
  +  그저 필요한 시점에 앱 전반에 해당 이벤트가 발생했다는 것을 알립니다.
  +  수신자는 notificationName을 기반으로 특정 Notification에 대응하도록 Observing 합니다.
  +  수신자는 발신자가 알림을 방출하면, 그에 해당하는 Observing중인 Notification을 전달받습니다.
  +  긴밀한 연결관계가 아니기 때문에, 발신자와 수신자는 서로가 잘 보내고 받았는지에 대한 확인작업이 불가능합니다.(하지않습니다.)

- 차이점   
  + 클래스 사이의 1:1 결합을 통하여 데이터를 주고받거나, 특정 이벤트 처리를 위임해야 할 경우 Delegate를 사용합니다.
  + 클래스 사이의 참조포인트가 너무 멀거나, 특정 이벤트의 발생을 여러 객체에서 동시에 처리해야 할 경우, Notification을 사용합니다. (ex..로그인 상태 변경 등)

---
**Q : Weak vs Strong (assign vs retain)**
- Weak : 메모리 관리에서 필요한 부분으로, 단어 뜻과 같이 약한 참조입니다.   
  - weak으로 선언된 property에 값을 할당하면, 소유권을 가지지 않고 해당 값의 주소만 약하게 참조합니다.
  - 할당된 객체는 누군가는 소유권을 가지고 있어야 하며, 소유권이 없어지는 경우, nil로 셋팅되며 참조는 끊기게 됩니다.   
     _- assign은 weak과 같은 쓰임새와 기능을 가지고 있으나, 참조하고있는 객체의 소유권이 사라져도 자동으로 nil로 설정되지 않고 쓰레기 주소를 가리키게 됩니다._
  - 대표적으로 delegate 를 사용할 때, retain Cycle을 피하기 위해 사용합니다.   

- Strong : 역시 메모리 관리에서 필요한 부분으로, 단어 뜻과 같이 강한 참조입니다.   
  - strong으로 선언된 property에 값을 할당하면, 해당 값에 대한 소유권을 가지며 retain count가 증가하게 됩니다.
  - 할당된 객체는 retain Count가 증가하게 되며, 할당된 객체의 원래 소유권자가 소유권을 해제하더라도 본인의 소유권이 남아있기 때문에, 해제되지 않습니다.   
    _- retain은 strong과 동일하며, arc 환경 이전에 사용하였습니다._   
    
    
---
<script src="https://utteranc.es/client.js"
        repo="aske0115/blog-comments"
        issue-term="pathname"
        label="utterences"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>
