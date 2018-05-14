---
layout: post
title:  "자바 람다 테스트"
date:   2015-12-23 12:00:00 +0900
categories: java lambda
---

## JAVA8

자바8의 람다식을 테스트해봤다.

```JAVA
package test;

import java.util.ArrayList;

public class main {
    public static void main(String[] args) {
        ArrayList<Integer> arrayList = new ArrayList<>();
        ArrayList<Integer> arrayList2 = new ArrayList<>();
        
        for(int i = 1; i < 100; i++ ) arrayList.add(i);
        
        //람다 테스트
        arrayList.forEach( i -> arrayList2.add(i * 11) );
        arrayList2.forEach( i -> System.out.println(i) );
    }
}
```