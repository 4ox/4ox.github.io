---
layout: post
title:  "자바 콜렉션 테스트"
date:   2015-12-24 12:00:00 +0900
categories: java collection
---

## JAVA8

### 크리스마스에 자바7 과 8의 비교 컬렉션에대해 공부해봤다.

http://www.tutorialspoint.com/java8/java8_overview.htm

```JAVA
package test;

import java.util.Collections;
import java.util.List;
import java.util.ArrayList;
import java.util.Comparator;

public class Java8Tester {
    private void sortUsingJava7( List<String> names ) {
       Collections.sort( names , new Comparator<String>() {
            @Override
            public int compare(String s1, String s2) {
                return s1.compareTo(s2);
            }
       });
    }
    private void sortUsingJava8(List<String> names ) {
        Collections.sort( names, (s1, s2 ) -> s1.compareTo(s2) );
    }
    public static void main(String args[]) {

        List<String> names1 = new ArrayList<String>();
        names1.add("ys ");
        names1.add("mhk ");
        names1.add("bjh ");
        names1.add("jjk ");
        names1.add("kdw ");
        names1.add("jih ");
        names1.add("4ox ");
        names1.add("khs ");
        names1.add("jsh ");

        List<String> names2 = new ArrayList<String>();
        names2.add("ys ");
        names2.add("mhk ");
        names2.add("bjh ");
        names2.add("jjk ");
        names2.add("kdw ");
        names2.add("jih ");
        names2.add("4ox ");
        names2.add("khs ");
        names2.add("jsh ");
        
        Java8Tester tester = new Java8Tester();
        System.out.println("JAVA7");
        tester.sortUsingJava7(names1);
        System.out.println(names1);
        
        System.out.println("JAVA8");
        tester.sortUsingJava8(names2);
        System.out.println(names2);
    }


}
```

### 자바8의 람다 표선식을 테스트 해보았다.


```JAVA
package test;

import java.util.Collections;
import java.util.List;
import java.util.ArrayList;
import java.util.Comparator;

public class Java8Tester {
    interface MathOperation {
        int operation(int a, int b);
    }

    interface GreetingService {
        void sayMessage(String message);
    }

    private int operate(int a, int b, MathOperation mathOperation) {
        return mathOperation.operation(a, b);
    }

    public static void main(String[] args) {
        Java8Tester tester = new Java8Tester();

        MathOperation addition = (int a, int b) -> a + b;
        
        MathOperation subtraction = ( a, b ) -> a - b;
        
        MathOperation multiplication = (int a, int b ) -> { return a * b; };
        
        MathOperation division = (int a, int b ) -> a / b;
        
        int a = 10, b = 5;
        System.out.println( a + " + " + b + " = " + tester.operate( a, b, addition ) );
        System.out.println( a + " - " + b + " = " + tester.operate( a, b, subtraction ) );
        System.out.println( a + " x " + b + " = " + tester.operate( a, b, multiplication ) );
        System.out.println( a + " / " + b + " = " + tester.operate( a, b, division ) );
        
        GreetingService greetingService1 = message -> System.out.println("Hello" + message );
        GreetingService greetingService2 = message -> System.out.println("Hello" + message );
        
        greetingService1.sayMessage("WTF");
        greetingService2.sayMessage("WTF2");
    }
}
```

### 자바8의 메소드 레퍼런스를 테스트해보았다.
http://www.tutorialspoint.com/java8/java8_method_references.htm

```JAVA
package test;

import java.util.ArrayList;

public class Java8Tester {
    public static void main(String[] args) {
        
        ArrayList<String> names = new ArrayList<String>();
        names.add("A");
        names.add("B");
        names.add("C");
        names.add("D");
        names.add("E");
        names.add("F");
        names.add("G");
        
        names.forEach(System.out::println);
    }
}
```


### 자바8의 펑셔널 인터페이스를 테스트해보았다.
http://www.tutorialspoint.com/java8/java8_functional_interfaces.htm

```JAVA
package test;

import java.util.Arrays;
import java.util.List;
import java.util.function.Predicate;

public class Java8Tester {
    
    public static void eval( List<Integer> list, Predicate<Integer> predicate ) {
        for(Integer n:list) 
            if(predicate.test(n))
                System.out.print( n + " ");
        System.out.println("");
    }
    
    public static void main(String[] args) {
        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9);
        
        System.out.print("Print all numbers : ");
        eval(list , n -> true );
        
        System.out.print("Print even numbers : ");
        eval(list , n -> n % 2 == 0 );

        System.out.print("Print greater than 3 numbers : ");
        eval(list , n -> n > 3 );
    }
}
```



### 자바8의 스트림을 공부중이다가 집에감
http://www.tutorialspoint.com/java8/java8_streams.htm

```JAVA
package test;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.function.Predicate;

public class Java8Tester {


    private static int getCountEmptyStringUsingJava7(List<String> strings) {
        int count = 0;
        for (String string : strings) {
            if (string.isEmpty())
                count++;
        }
        return count;
    }

    private static int getCountLength3UsingJava7(List<String> strings) {
        int count = 0;
        for (String string : strings) {
            if (string.length() == 3)
                count++;
        }
        return count;
    }

    private static List<String> deleteEmptyStringsUsingJava7(List<String> strings) {
        List<String> filteredList = new ArrayList<String>();
        for (String string : strings) {
            if (!string.isEmpty())
                filteredList.add(string);
        }
        return filteredList;
    }

    private static String getMergedStringUsingJava7(List<String> strings, String separator) {
        StringBuilder stringBuilder = new StringBuilder();
        for (String string : strings) {
            if (!string.isEmpty()) {
                stringBuilder.append(string);
                stringBuilder.append(separator);
            }
        }
        String mergedString = stringBuilder.toString();
        return mergedString.substring(0, mergedString.length() - 2);
    }

    private static List<Integer> getSquares(List<Integer> numbers) {
        List<Integer> squaresList = new ArrayList<Integer>();

        for (Integer number : numbers) {
            Integer square = new Integer(number.intValue() * number.intValue());
            if (!squaresList.contains(square)) {
                squaresList.add(square);
            }
        }
        return squaresList;
    }

    private static int getMax(List<Integer> numbers) {
        int max = numbers.get(0);

        for (int i = 1; i < numbers.size(); i++) {
            Integer number = numbers.get(i);
            if (number.intValue() > max) {
                max = number.intValue();
            }
        }
        return max;
    }

    private static int getMin(List<Integer> numbers) {
        int min = numbers.get(0);
        for (int i = 1; i < numbers.size(); i++) {
            Integer number = numbers.get(i);
            if( number.intValue() < min ) {
                min = number.intValue();
            }
        }
        return min;
    }

    private static int getSum(List numbers) {
        int sum = (int)numbers.get(0);
        for (int i = 1; i < numbers.size(); i++) {
            sum += (int)numbers.get(i);
        }
        return sum;
    }

    private static int getAverage(List<Integer> numbers) {
        return getSum(numbers) / numbers.size();
    }

    public static void main(String[] args) {
        System.out.println("Using Java7 : ");
        
        List<String> strings = Arrays.asList("abc", "", "bc", "efg", "abcd", "", "jkl");
        System.out.println("List : " + strings );
        
        long count = getCountEmptyStringUsingJava7(strings);
        System.out.println("Empty Strings : " + count );
        
        count = getCountLength3UsingJava7(strings);
        System.out.println("Strings of length 3 : " + count );
        
        List<String> filtered = deleteEmptyStringsUsingJava7(strings);
        System.out.println("Filtered List : " + filtered);
        
        String mergedString = getMergedStringUsingJava7(strings, ", ");
        System.out.println(mergedString);
        
        List<Integer> numbers = Arrays.asList(3,2,2,3,7,3,5);
                
        List<Integer> squaresList = getSquares(numbers);
        System.out.println("Squares List : " + squaresList);
        
        List<Integer> integers = Arrays.asList(1,2,13,4,15,6,17,8,19);
        
        System.out.println("List : " + integers );
        System.out.println("Highest number in List : " + getMax(integers) );
        System.out.println("Lowest  number in List : " + getMin(integers) );
        System.out.println("List : " + integers );
        System.out.println("List : " + integers );
        System.out.println("List : " + integers );
        
    }
}

```