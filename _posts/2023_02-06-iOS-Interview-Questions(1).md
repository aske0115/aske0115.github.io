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

