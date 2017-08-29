---
layout: post
title:  "자바 스트림 테스트"
date:   2015-12-29 12:00:00 +0900
categories: java stream
---

##JAVA

### 자바8의 스트림

자바7 과 8의 비교 스트림
http://www.tutorialspoint.com/java8/java8_streams.htm

```JAVA
package test;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.IntSummaryStatistics;
import java.util.List;
import java.util.Optional;
import java.util.Random;
import java.util.stream.Collector;
import java.util.stream.Collectors;

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
        System.out.println("Sum  number in List : " + getSum(integers) );
        System.out.println("Average  number in List : " + getAverage(integers) );
        System.out.println("Random   number in List : ");
        
        //print ten random numbers
        Random random = new Random();
        for(int i=0; i < 10; i++){
          // System.out.println(random.nextInt());
        }
        
        System.out.println("---------------------------------------------------------------------------------");
        
        System.out.println("Using Java 8: ");
        System.out.println("List: " +strings);
        
        count = strings.stream().filter(string->string.isEmpty()).count();
        System.out.println("Empty Strings: " + count);
        
        count = strings.stream().filter(string->string.length() == 3 ).count();
        System.out.println("Strings of length 3 : " + count );
        
        filtered = strings.stream().filter(string-> !string.isEmpty() ).collect(Collectors.toList());
        System.out.println("Filtered List : " + filtered);
        
        mergedString = strings.stream().filter(string-> !string.isEmpty()).collect(Collectors.joining(", "));
        System.out.println(mergedString);
        
        squaresList = numbers.stream().map( i -> i*i ).distinct().collect(Collectors.toList());
        System.out.println("Squares List : " + squaresList);
        
        IntSummaryStatistics stats = integers.stream().mapToInt((x)->x).summaryStatistics();
        
        System.out.println("List : " + integers );
        System.out.println("Highest number in List : " + stats.getMax() );
        System.out.println("Lowest  number in List : " + stats.getMin() );
        System.out.println("Sum  number in List : " + stats.getSum() );
        System.out.println("Average  number in List : " + stats.getAverage() );
        System.out.println("Random   number in List : ");
        
        //random.ints().limit(10).sorted().forEach(System.out::println);
        
        count = strings.parallelStream().filter(string->string.isEmpty()).count();
        System.out.println("Empty Strings: " + count);
        
        System.out.println("---------------------------------------------------------------------------------");
        
        System.out.println(stats.toString());
        
    }
}

```


### Base64, Nashorn, Optional, Stream, Time

관련 클래스 확인함.