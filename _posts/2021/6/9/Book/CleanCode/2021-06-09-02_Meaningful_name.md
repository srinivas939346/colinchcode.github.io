---
layout: post
title: "[Clean Code] "
description: " "
date: 2021-06-09
tags: [Book]
comments: true
share: true
---

```
2장 의미 있는 이름
들어가면서
의도를 분명히 밝혀라
그릇된 정보를 피하라
의미 있게 구분하라
발음하기 쉬운 이름을 사용하라
검색하기 쉬운 이름을 사용하라
인코딩을 피하라
__ 헝가리식 표기법
__ 멤버 변수 접두어
__ 인터페이스 클래스와 구현 클래스
자신의 기억력을 자랑하지 마라
클래스 이름
메서드 이름
기발한 이름은 피하라
한 개념에 한 단어를 사용하라
말장난을 하지 마라
해법 영역에서 가져온 이름을 사용하라
문제 영역에서 가져온 이름을 사용하라
의미 있는 맥락을 추가하라
불필요한 맥락을 없애라
```
## 의미 있는 이름

직접적 구체적인 방법에 앞서, 전체적인 이론적 내용을 살펴보면

### 의도를 분명히 밝혀라.
의도를 분명히 밝히라는 말의 뜻은 무엇일까?
작성하고자하는 변수나 함수 그리고 클래스 이름이 모두 이에 해당한다.

코드안에 각 이름과 코드의 가독성이 이에 해당한다.

만약 난독성이 높은 코드라면 볼 필요도 없다.

예를 들어, 살펴본다면?
```java
public List<int[]> getThem(){
  List<int[]> list1 = new ArrayList<int[]>();
  for (int[] x: theList ) {
    if(x[0] == 4)
      list1.add(x);
  return list1;
  }
}
```
 위 코드에서 각각의 변수명과 코드의 가독성을 고려해보면 무엇을 말하는지 짐작하기 어렵다.
문제는 코드의 단순성이 아니라 코드의 함축성이다. 다시 말해, 코드 맥락이 코드 자체에 명시적으로 드러나지 않는다.

아래 코드를 한번 살펴보자.
```java
 public List<int[]> getFlaggedCells(){
   List<int[]> flaggedCells = new ArrayList<int[]>();
   for(int[] cell : gameBoard)
    if(cell[STATUS_VALUE] == FLAGGED)
      flaggedCells.add(cell);
    return flaggedCells;
 }
```

위와 코드에 반해, 변수,메소드 하나하나가 무엇을 말하고자하는지 암시해주는 코드다.
다시말해, 코드가 무슨 일을 할 것이다 라는 의미를 조금더 쉽게 전달해준다.

여기서 더 개선된다면,

```java
 public List<int[]> getFlaggedCells(){
   List<int[]> flaggedCells = new ArrayList<int[]>();
   for(int[] cell : gameBoard)
    if(cell.isFlagged())
      flaggedCells.add(cell);
    return flaggedCells;
 }
```

중간에 if을 바꿔 더욱더 개선해서 한결 더 이해하기 쉬운 코드로 변경 가능하다.

## 그릇된 정보를 피하라.

여기서 말하고자하는 건 **일관성이 떨어지는 표기법은 그릇된 정보이다**

만약, ArrayList를 활용하는 객체라고해서 list라는 마을 활용하는 건, 같은 말을 두번 하는 것과 동일하다. 그러므로, 만약

AccountList 라면, Accounts 이런 방식으로 교체!

또는 서로 흡사한 이름을 사용하지 않도록 주의!

## 의미 있게 구분하라.
 컴파일러나 인터프리터만 통과하려는 생각으로 코드를 구현하는 프로그래머는 스스로 문제를 일으킨다.
사실 위의 말이 중요하다라고 생각한다.
컴파일러를 통과할지라도 연속된 숫자를 덧붙이거나 noise word를 추가하는 방식은 적절치 않다.

책에는 불용어라고 나왔지만, noise word라는 표현이 더 적절하다고 표현된다.

이 말의 뜻은 부수 효과를 최대한 생각하고 단어를 활용하라는 의미이다.

 다음의 예를 살펴보면, 변수 momneyAmount 는 money와 구분이 안되고, cus-tomerInfo는 customer와, AccountData는 account와, theMessage는 message와 구분이 안 된다. 읽는 사람이 차이를 알도록 이름을 지어라.

## 발음하기 쉬운 이름을 사용하라
## 검색하기 쉬운 이름을 사용하라

검색하기 쉽다는 의미는 유지보수를 위해 어떤 변수에 의미를 부여할 때, 너무 과한 변수명보다는 쉬운 명으로 하라는 이야기.

## 인코딩을 피하라.
## 자신의 기억력을 자랑하지 마라.
 명료함으로 무장한 코드를 작성하라. 너무 기억력을 믿으면 큰 코 다친다는 이야기...

## 클래스 이름
 클래스 이름과 객체 이름은 명사나 명사구가 적합하다.
 Customer, WikiPage, Account, AddressParser 등의 좋은 예로, 동사는 사용하지 않는다.
## 메서드 이름
 동사나 동사구가 적절하다. 접근자, 변경자, 조건자는 javabean 표준에 따라 앞에 get,set,is를 붙인다.
 생성자를 중복정의 할 때는 정적 팩토리 메서드를 사용한다. 메서드는 인수를 설명하는 이름을 사용한다.
## 기발한 이름은 피하라.
말이 기발이지, 자기들끼리 쓰는 용어로 이름을 명명하지 말라.

## 한 개념에 한 단어를 사용하라.

추상적인 개념 하나에 단어 하나를 선택해 이를 고수한다.
예를 들어, 똑같은 메서드를 클래스마다 fetch, retrieve, get으로 제각각 부르면 혼란스럽다. 어느 클래스에서 어느 이름을 썼는지 기억하기 어렵다.
그러므로 일관성 있는 어휘는 코드를 사용할 프로그래머가 반갑게 여길 선물이다.
협업이 아니라도, 한 가지 개념에 한 가지 단어는 고수할 필요가 있다라고 생각한다.

흔히 MVC에서 말하는 Controller와 Manager의 차이가 뭔지? 차이를 보기 전 각 함수의 기능을 제대로 파악하고 자신이 정한 개념에 상충하는지 고민해야 될 것이다.

## 의미 있는 맥락을 추가하라.
 스스로 의미가 분명한 이름이 없지않다. 하지만 대다수 이름은 그렇지 못하다. 그래서 클래스, 함수, 이름 공간에 넣어 맥락을 부여한다. 모든 방법이 실패하면 마지막 수단으로 접두어를 붙인다.

이 말은 위에 `의도를 분명히 하라` 와 동일하다.