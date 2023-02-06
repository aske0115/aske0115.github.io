---
layout: post
title: iOS Interview Question Part1 
description: >
  iOS Tech Interview에서 자주 나오는 질문들에 대한 모음집입니다.
  [참고](https://chetan-aggarwal.medium.com/ios-interview-questions-part-1-differentiate-99e8f574a3f1) 
  위 링크를 참고하여 한글로 풀어 설명하고, 추가적인 설명은 덧붙히고, 불필요해 보이는 것은 제거하려고 합니다.
sitemap: false
---

## iOS Interview Question Part1   

**Q : Categoty VS Protocol**
- Category : 기존에 생성되어 있는 Class들을 상속하지 않고, 메소드(기능)을 확장하기 위하여 사용합니다.   
~~~objective-c
 @interface NSString (URL)
 - (BOOL)isHTTPProtocol;
 @end
 
 @implementation NSString (URL)
 - (BOOL)isHTTPProtocol {
    return [[self lowercastString] hasPrefix:@"http://"] || [[self lowercastString] hasPrefix:@"https://];
 }
~~~
