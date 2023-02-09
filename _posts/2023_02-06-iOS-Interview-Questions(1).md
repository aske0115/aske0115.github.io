---
layout: post
title: iOS Interview Question Part1 
sitemap: false
---


* iOS Tech Interview에서 자주 나오는 질문들에 대한 모음집입니다.   
  
  > [참고사이트](https://chetan-aggarwal.medium.com/ios-interview-questions-part-1-differentiate-99e8f574a3f1)   
  
  > 위 링크를 참고하여 한글로 풀어 설명하고, 추가적인 설명은 덧붙히고, 불필요해 보이는 것은 제거하려고 합니다.   
  

## iOS Interview Question Part1   

**Q : Categoty VS Protocol**
- Category : 기존에 생성되어 있는 Class들을 상속하지 않고, 메소드(기능)을 확장하기 위하여 사용합니다. 

 
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



