---
layout: post
title: EFFECTIVE JAVA 3/E | 2장. 객체 생성과 파괴
hide_title: true     
date: 16 january 2019
excerpt_separator: <!--more-->
---
# EFFECTIVE JAVA 3/E | 2장. 객체 생성과 파괴
<br>
<br>
<br>
<br>

<center><img src="/assets/img/pexels/effectiveJAVA.jpg"></center>  
이펙티브 자바 3판의 정리를 해보겠다.  
JAVA를 이용한 프로젝트를 적어도 한 개 이상 해본 후에 읽어 볼 것을 추천한다.  
내가 공부하면서 내용은 정리하겠지만 무엇보다도 좋은건 책을 사서 프로젝트를 진행하며 읽고 공부하는 것이 제일 좋을 듯 하다.  
<!--more-->
<br>
<br>
<br>
<br>
### 2장 아이템 목록
- [ITEM1. 생성자 대신 정적 팩터리 메소드를 고려하라.](#item1)
- [ITEM2. 생성자에 매개변수가 많다면 빌더를 고려하라.](#item2)  

(2020.01.19) 업데이트
<br>
<br>
<br>
<br>
<div id="item1"/>
### ITEM1. 생성자 대신 정적 팩터리 메소드를 고려하라.
--------------------------------------------------

#### 장점 5가지
- __이름을 가질 수 있다.__  
정적 팩터리는 이름만 잘지으면 반환될 객체의 특성을 쉽게 묘사할 수 있다.
  - 어느 쪽이 '값이 소수인 BigInteger를 반환한다'는 의미를 더 잘 설명하는가  
  `BigInteger(int, int, Random)` vs `BigInteger.probablePrime`  
  <br>
- __호출될 때마다 인스터스를 새로 생성하지는 않아도 된다.__  
불필요한 객체 생성을 피할 수 있다.  
  - 인스턴스 통제(instance-controlled) 클래스 : 반복되는 요청에 같은 객체를 반환하는 식으로 언제 어느 인스턴스를 살아 있게 할지를 철제히 **통제** 할 수 있다.
  - 플라이웨이트패턴(Flyweight pattern) : 동일하거나 유사한 객체들 사이에 가능한 많은 데이터를 서로 공유하여 사용하도록 하여 메모리 사용량을 최소화하는 소프트웨어 디자인 패턴이다.  
<br>
- __반환 타입의 하위 타입 객체를 반환 할 수 있는 능력이 있다.__  
반환할 객체의 클래스를 자유롭게 선택할 수 있는 **'엄청난 유연성'** 을 선물한다.   
  - API를 작게 유지할 수 있다 -> 인터페이스 기반 프레임워크를 만드는 핵심 기술
  - 컬렉션 프레임워크
    - 자바에서 컬렉션 프레임워크(collection framework)란 다수의 데이터를 쉽고 효과적으로 처리할 수 있는 표준화된 방법을 제공하는 클래스의 집합을 의미한다.
    - API외견을 훨씬 작게 만들 수 있다.
    - 정적 팩터리 메서를 사용하는 클라이언트는 얻은 객체를 (그 구현 클래스가 아닌) 인터페이스만으로 다루게 된다.  
<br>
- __입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다.__  
반환 타입의 하위 타입이기만 하면 어떤 클래스의 객체를 반환하든 상관없다.  
  <br>
- __정적 팩터리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.__
  - 서비스 제공자 프레임워크(service provider framework)
    - 제공자 : 서비스 구현체 -> 클라이언트에 제공하는 역할을 프레임워크가 통제하여, 클라이언트를 구현체로부터 분리해준다.
    - 대표적인 서비스 제공자 프레임워크 : JDBC(Java Database Connectivity)
    - 핵심 컴포넌트
      1. 서비스 인터페이스(service insterface) : 구현체의 동작을 정의
      1. 제공자 등록 API(provider registration API) : 제공자가 구현체를 등록 할 떄 사용
      1. 서비스 접근 API(service access API) : 클라이언트가 서비스의 인스턴스를 얻을 때 사용
      1. 서비스 제공자 인터페이스(service provider interface)
        - 위의 3개의 핵심 컴포넌트 외에 종종 쓰이는 컴포넌트
        - 서비스 인터페이스의 인스턴스를 생성하는 팩터리 객체를 설명  


#### 단점 2가지
- __상속을 하려면 public이나 protected 생성자가 필요하니 정적 팩터리 메서드만 제공하면 하위 클래스를 만들 수 없다.__



- __정적 팩터리 메서드는 프로그래머가 찾기 어렵다.__

#### 핵심정리
> 정적 팩터리 메서드와 public 생성자는 각자의 쓰임새가 있으니 상대적인 장단점을 이해하고 사용하는 것이 좋다. 그렇다고 하더라도 정적 팩터리를 사용하는 게 유리한 경우가 더 많으므로 무작정 public 생성자를 제공하던 습관이 있다면 고치자.

<br>
<br>
<br>
<div id="item2"/>
### ITEM2. 생성자에 매개변수가 많다면 빌더를 고려하라.
--------------------------------------------------

정적 팩터리와 생성자에는 똑같이 선택적 매개변수가 많을 때 적절히 대응하기 어렵다는 제약이 있다.  
#### 2-1 점층적 생성자 패턴 - 확장하기 어렵다
``` java
public class NutritionFact {
  private final int servingSize;  // 필수
  private final int servings;     // 필수
  private final int calories;     // 선택
  private final int fat;          // 선택
  private final int sodium;       // 선택
  private final int carbohydrate;  //선택


  public NutritionFact(int servingSize, int servings) {
    this(servingSize, servings, 0);
  }

  public NutritionFact(int servingSize, int servings, int calories) {
    this(servingSize, servings, calories, 0);
  }

  public NutritionFact(int servingSize, int servings, int calories, int fat) {
    this(servingSize, servings, fat, 0);
  }

  public NutritionFact(int servingSize, int servings, int calories, int fat, int sodium) {
    this(servingSize, servings, fat, sodium, 0);
  }

  public NutritionFact(int servingSize, int servings, int calories, int fat, int sodium, int carbohydrate) {
    this.servingSize = servingSize;
    this.servings = servings;
    this.calories = calories;
    this.fat = fat;
    this.sodium = sodium;
    this.carbohydrate = carbohydrate;
  }
}
```
<br>
이 클래스의 인스턴스를 만들려면 매개변수를 모두 포함한 생성자 중 가장 짧은 것을 골라 호출하면 된다.  
<br>
``` java
NutritionFact cocaCola = new NutritionFact(240, 8, 100, 35, 27)
```
<br>
점층적 생성자 패턴도 쓸 수는 있지만, 매개변수 개수가 많아지면 클라이언트 코드를 작성하거나 읽기 어렵다.
<br>
<br>
<br>
#### 2-2 자바빈즈 패턴 - 일관성이 깨지고, 불변으로 만들 수 없다.
``` java
public class NutritionFact {
  private int servingSize   = -1;  // 필수; 기본값 없음
  private int servings      = -1;  // 필수; 기본값 없음
  private int calories      = 0;     
  private int fat           = 0;        
  private int sodium        = 0;     
  private int carbohydrate  = 0;  

  public NutritionFact() {  }
  // setter 메서드들
  public void setServingSize(int val) { servingSize = val; }
  public void setservings(int val) { servings = val; }
  public void setCalories(int val) { calories = val; }
  public void setFat(int val) { fat = val; }
  public void setSodium(int val) { sodium = val; }
  public void setCarbohydrate(int val) { carbohydrate = val; }
}
```
<br>
점층적 생성자 패턴의 단덤들이 자바빈즈 패턴에서는 더 이상 보이지 않는다
<br>
``` java
NutritionFact cocaCola = new NutritionFact();
cocaCola.setServingSize(240);
cocaCola.setservings(8);
cocaCola.setCalories(100);
cocaCola.setSodium(35);
cocaCola.setCarbohydrate(27);
```
<br>
그러나 심각한 단점이 있다. 자바빈즈 패턴에서는 객체를 하나 만들려면 메서드를 여러 개 호출해야 하고, 객체가 완전히 생성되기 전까지는 일관성(consistency)이 무너진 상태에 놓이게 된다. 따라서 클래스를 불변으로 만들 수 없다.
- 불변식(invariant) : 프로그램이 실행되는 동안, 혹은 정해진 기간 동안 반드시 만족해야 하는 조건
<br>
<br>
<br>
#### 2-3 빌더 패턴 - 점층적 생성자 패턴과 자바빈즈 패턴의 장점만 취했다.
``` java
public class NutritionFact {
  private final int servingSize;
  private final int servings;    
  private final int calories;
  private final int fat;       
  private final int sodium;   
  private final int carbohydrate;  

  public static class Builder {
    // 필수 매개변수
    private final int servingSize;
    private final int servings;

    // 선택 매개변수 - 기본값으로 초기화 한다.
    private int calories      = 0;
    private int fat           = 0;
    private int sodium        = 0;
    private int carbohydrate  = 0;

    public Builder(int servingSize, int servings) {
      this.servingSize = servingSize;
      this.servings = servings;
    }

    public Builder setCalories(int val) {
      calories = val;
      return this;
   }
    public Builder setFat(int val) {
      fat = val;
      return this;
    }
    public Builder setSodium(int val) {
      sodium = val;
      return this;
    }
    public Builder setCarbohydrate(int val) {
      carbohydrate = val;
      return this;
    }

    public NutritionFact build() {
      return new NutritionFact(this);
    }
  }

    private NutritionFact(Builder build) {
      servingSize   = build.servingSize;
      servings      = build.servings;
      calories      = build.calories;    
      fat           = build.fat;       
      sodium        = build.sodium;    
      carbohydrate  = build.carbohydrate;
    }
}
```

<br>
이런 방식을 메서드 호출이 흐르듯 연결된다는 뜻으로 플루언트 API(fluent API) 혹은 메서드 연쇄(method chaining)라 한다.
<br>

```java
NutritionFact cocaCola = new NutritionFact.Builder(240, 8).calories(100).sodium(35).carbohydrate(27).build;
```

<br>
빌더 패턴은 (파이썬과 스칼라에 있는) 명명된 선택적 매개 변수(named optional parameters)를 흉내낸 것이다.  
빌더 패턴은 **계층적** 으로 설계된 클래스와 함께 쓰기에 좋다.
<br>
<br>

#### 2-4 계층적으로 설계된 클래스와 잘 어울리는 빌더 패턴

``` java
public abstract class Pizza {
  public enum Topping { HAM, MUSHROOM, ONION, PEPPER, SAUSAGE }
  final Set<Topping> toppings;

  abstract static class Builder<T extends Builder<T> {
    EnumSet<Topping> toppings = EnumSet.noneOf(Topping.class);
    public T addTopping(Topping topping) {
      toppings.add(Objects.requireNonNull(topping));
      return self();
    }

    abstract Pizza build();

    // 하위 클래스는 이 메서드를 재정의(overriding) 하여
    // "this" 를 반환하도록 해야한다.
    protected abstract T self();
  }

  Pizza(Builder<?> builder) {
    toppings = builder.toppings.clone();
  }
}
```

<br>
Pizza.Builder 클래스는 재귀적 타입 한정을 이용하는 제네릭 타입이다.  
self 타입이 없는 자바를 위한 우회 방법을 시뮬레이트한 셀프 타입(simulated self-type) 관용구라 한다.
<br>
<br>
<br>
#### 2-5 뉴욕피자 - 크기(size) 매개변수를 필수로 받는다.

``` java
public class NyPizza extends Pizza {
  public enum Size { SMALL, MEDIUM, LARGE }
  private final Size size;

  public static class Builder exteds Pizza.Builder<Builder> {
    private final Size size;

    public Builder(Size size) {
      this.size = Objects.requireNonNull(size);
    }

    @Override public NyPizza build() {
      return new NyPizza(this);
    }

    @Override protected Builder self() { return this; }
  }

  private NyPizza(Builder builder) {
    super(builder);
    size = builder.size;
  }
}
```

<br>
<br>
<br>

#### 2-6 칼초네 피자 - 안에 소스를 넣을지 선택(sauceInside)하는 매개 변수를 받는다.

``` java
public class Calzone extends Pizza {
  private final boolean sauceInside;

  public static class Builder exteds Pizza.Builder<Builder> {
    private boolean sauceInside = false;  // 기본값

    public Builder sauceInside() {
      sauceInside = true;
      return this;
    }

    @Override public Calzone build() {
      return new Calzone(this);
    }

    @Override protected Builder self() { return this; }
  }

  private Calzone(Builder builder) {
    super(builder);
    sauceInside = builder.sauceInside;
  }
}
```

<br>

각 하위 클래스의 빌더가 정의한 builder 메서드는 해당하는 구체 하위 클래스를 반환하도록 선언한다.  
하위 클래스의 메서드가 상위 클래스의 메서드가 정의한 반환 타입이 아닌, 그 하위 타입을 반환하는 기능을 공변 반환 타이핑(covariant return typing) 이라 한다.

<br>

``` java
NyPizza pizza = new NyPizza.Builder(SMALL).addTopping(SAUSAGE).addTopping(ONION).build();
Calzone calzone = new Calzone.Builder().addTopping(HAM).sauceInside().build();
```

<br>

빌더 하나로 여러 객체를 순회하면서 만들 수 있고, 빌더에 넘기는 매개변수에 따라 다른 객체를 만들 수도 있다.
<br>
<br>
<br>

#### 빌더 패턴의 단점
성능에 민감한 상황에서 객체를 만드려면, 그에 앞서 빌더부터 만들어야하는데 이것이 민감한 문제가 될 수 있다.
<br>
<br>
<br>
#### 핵심정리
> **생성자나 정적 팩터리가 처리해야 할 매개변수가 많다면 빌더 패턴을 선택하는 게 더 낫다.** 매개변수 중 다수가 필수가 아니거나 같은 타입이면 특히 더 그렇다. 빌더는 점층적 생성자보다 클라이언트 코드를 읽고 쓰기가 훨씬 간결하고, 자바빈즈보다 훨씬 안전하다.
