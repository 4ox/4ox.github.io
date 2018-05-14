---
layout: post
title:  "코딩 테스트 : 1이 몇번 들어 있는지 세어라."
date:   2015-10-12 15:16:20 +0900
categories: quiz
---

정수 2개 a,b를 입력받으면 a부터 b까지의 수 중 1이 몇 번 들어 있는지 세는(return) 함수를 작성하고.
다음의 숫자를 입력했을 때 받아온 값을 출력 하는 프로그램을 작성하시오.
(숫자의 어느 위치에든 1이 있으면 개수를 센다)

a=10, b=2000000

## JAVA
```java
public class test {
	public static int count1(int num) {
		int cnt = 0;
		
		int firstInt = 0, tmpInt = num, pow, temp = num, term;
		for( int i = 0, ilen = (int)Math.log10(num)+1; i < ilen ; i++ ) {
			pow = (int)Math.pow(10, i);
			firstInt = tmpInt % 10;
			tmpInt = tmpInt / 10;
			
			cnt += (i * (int)Math.pow(10, i-1) ) * firstInt;
			if( firstInt > 1 ) {
				cnt += pow;
			}
			else if( firstInt == 1 ) {
				term = num-temp;
				cnt+= term > 0 ? term + 1:1;
			}
			temp-= pow*firstInt;
		}
		return cnt;
	}
	public static int countOne(int min, int max) {
		return count1(max)-count1(min);
	}
	public static void main(String[] args) {
		int n = test.countOne(10, 2000000);
        System.out.println( n );
	}
}
```

## JAVASCRIPT
```javascript
function count1(num) {
    var cnt = 0, firstInt = 0, tmpInt = num, pow, temp = num, term;
    for( var i = 0, ilen = Math.log10(num)+1; i < ilen; i++ ) {
        pow = Math.pow(10, i);
        firstInt = tmpInt % 10;
        tmpInt = Math.floor(tmpInt / 10);

        cnt += i * (Math.pow(10,i-1)) * firstInt;
        if( firstInt > 1 ) {
            cnt += pow;
        }
        else if( firstInt == 1 ) {
            term = num - temp;
            cnt+= term > 0 ? term + 1 : 1;
        }
        temp -= pow * firstInt;
    }
    return cnt;
}
function countOne(min,max) {
    return count1(max) - count1(min);
}
var count = countOne(10, 2000000 );
console.log( "COUNT : " + count );
```

> 답 : 2199998

