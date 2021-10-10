---
layout: post
title: 자바 Array 배열 정리
comments: true
categories: [Java]

# Insight
# Project
# Retrospect
# PS
# LogicDesign
# Contest
# DataStructure
# Java

---


>목차
- Array
  - Copying
  - Array Class

## Array
---
Array는 자바에서 배열을 저장하기 위한 자료구조이다.

```java
int [] intArray1 = new int[10]; // 1번 방법 (추천)
int intArray2 [] = new int[10]; // 2번 방법 (c-style)
```
위와 같이 선언할 수 있다.

초기화 블럭 `{}`으로 선언과 동시에 초기화 할 수 있다.
```java
int [] ia = {0, 1, 2, 3} ;
```

아래 예시와 같이 data를 저장하고 조회할 수 있다.
```java
public static void main(String[] args) {

    int [] ia = new int[101];

    for ( int i = 0; i < ia.length; i++ )
        ia[i] = i ; // 0 ~ 100

    int sum = 0;
    for ( int v : ia ) // Enhanced for loop 
       sum += v; // 0 + 1 + ... + 100
} 
```

### Copying Array 배열 복사

- **Shallow Copy 얕은 복사**  

자바에서는 배열도 객체이기 때문에 배열의 identifier는 reference 타입으로 주소를 가르키고 있다. 

그래서 배열을 단순히 복사하기 위해 할당연산자 **=** 만을 사용한다면,  
**두 참조자가 같은 배열 객체를 가르키**고 있게 되는 것이다.

그리하여 아래와 같은 문제가 발생한다.
```java
int [] smallPrimes = {2, 3, 5, 7, 11, 13} ;
int [] luckyNumbers = smallPrimes ;

luckyNumbers[5] = 12 ; // now smallPrimes[5] is also 12
```

- **Deep Copy 깊은 복사**  

객체의 주소만 복사하는게 아니라 값, 객체 자체를 복사하고 싶다면 Deep copy를 위한 메소드 `System.array.copy(from, fromIndex, to, toIndex, count)`를 사용해야한다.

```java
int [] arr1 = {2, 3, 5, 7, 11, 13} ;
int [] arr2 = {101, 102, 103, 104, 105, 106, 107}; 

// arr1의 2 부터 4개의 원소를 복사하여 arr2의 3 부터 대입한다.
System.arraycopy(arr1, 2, arr2, 3, 4) ;
// arr2 = { 101, 102, 103, 5, 7, 11, 13 }
```
*Array.copyOf()라는 대체제 존재*

### Array Class 배열 클래스
java.util.Array 클래스는 여러가지 유용한 배열 메소드들은 제공해준다.

```java
int[] arr1 = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

Arrays.binarySearch(arr1, 7); 
// 6 (index of key)

int[] arr2 = Arrays.copyOf(arr1, 10); 
// deep copy

Arrays.equals(arr1, array2); 
// true

int[] arr3 = Arrays.copyOfRange(arr1, 2, 5); 
// deep copy {2, 3, 4}

int[] arr4 = new int[5];
Arrays.fill(array4, 7); 
// {7, 7, 7, 7, 7}

Arrays.asList("Hello", "Java"); 
// array를 ArrayList로 변환 (주소)
```
