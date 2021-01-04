---
layout: post
title: Algorithm | 정렬
hide_title: true     
date: 03 january 2021
excerpt_separator: <!--more-->
---

# 정렬
<!--more-->
#### Select Sort
가장 큰 값을 찾아 뒤로 보낸다
|순서|결과|
|----|----|
|inttial array  | 29 10 14 **37** 13|
|after 1st swap | **29** 10 14 13 *37*|
|after 2nd swap | 13 10 **14** *29 37*|
|after 3rd swap | **13** 10 *14 29 37*|
|after 4th swap | 10 *13 14 29 37*|

~~~java
 selectionSort(A[], n) { // 배열  A[1...n]을 정렬한다
   for last <- n downto 2 {                   ------ (1)
     A[1...last] 중 가장 큰 수 A[k]를 찾는다;  -------(2)

     // A[k]와 A[last]의 값을 교환
     A[k] <-> A[last];                        -------(3)
   }
 }
~~~

실행시간 :
(1)의 for 루프는 n-1번 반복
(2)에서 가장 큰 수를 찾기 위한 비교 횟수 : n-1, n-2, ..., 2, 1
(3)의 교환은 상수시간 작업

시간복잡도 $$T(n)=(n-1)+(n-2)+...+2+1 = O(n^{2})$$


#### Bubble Sort

|pass1|pass2|
|-----|-----|
|**29 10** 14 37 13|**10 13** 29 13 *37*
|10 **29 14** 37 13|10 **14 29** 13 *37*
|10 14 **29 37** 13|10 14 **29 13** *37*
|10 14 29 **37 13**|10 14 13 29 *37*
|10 14 29 13 *37*|

실행시간 : (n-1)+(n-2)+...+2+1 = O(n^2^)

~~~java
 bubbleSort(A[], n) { // 배열  A[1...n]을 정렬한다
   for last <- n downto 2 {                   ------ (1)
     for i <- 1 last-1                        -------(2)

     // 교환
     if (A[i]>A[i+1]) then a[i] <-> a[i+1];   -------(3)
   }
 }
~~~

수행시간 :
(1)의 for 루프는 n-1번 반복
(2)의 for 루프는 각각  n-1, n-2, ..., 2, 1번 반복
(3)의 교환은 상수시간 작업

시간복잡도$$T(n)=(n-1)+(n-2)+...+2+1 = O(n^{2})$$
-> 최약, 최선, 평균 동일

#### Insert Sort
|정렬|Insert|before
|----|----|---|
|*15* **12** 13 10 14 11|12|15|
|*12 **15*** 13 10 14 11|
|*12 15* **13** 10 14 11|13|15|
|*12 13 **15*** 10 14 11|
|*12 13 15* **10** 14 11|10|12|
|*10 12 13 **15*** 14 11|
|*10 12 13 15* **14** 11|14|15|
|*10 12 13 14 **15*** 11|
|*10 12 13 14 15* **11**|11|12|
|*10 11 12 13 14 **15***|

~~~java
 insetSort(A[], n) { // 배열  A[1...n]을 정렬한다
   for i <- 2 to n {                          -----(1)
     A[1...i]의 적당한 자리에 A[i]를 삽입한다.  -----(2)
   }
 }
~~~

수행시간 :
(!)의 for 루프는 n-1번 반복
(2)의 삽입은 최악의 경우 i-1 비교

**최악**의 경우:
$$T(n)=(n-1)+(n-2)+...+2+1 = O(n^{2})$$

#### 합병정렬(Merge Sort)
- 분할 : 해결하고자 하는 문제를 작은 크기의 **동일한** 문제들로 분할
- 정복 : 각각의 작은 문제를 **순환적**으로 해결
- 합병 : 작은 문제의 해를 합하여(merge) 원래 문제에 대한 해를 구함
divide -> recursively sort -> merge

~~~java
mergeSort(A[], p, r) { // A[p...r]을 정렬한다
  if (p<r) then {
    q <- (p+q)/2;         -----(1) p, q의 중간 지점 계산
    mergeSort(A, p, q);   -----(2) 전반부 정렬
    mergeSort(A, q+1, r); -----(3) 후반부 정렬
    merge(A, p, q, r);    -----(4) 합병
  }
}

merge(A[], p, q, r) {
  정렬되어 있는 두 배여 A[p...q]와 A[q+1...r]을 합하여
  정렬된 하나의 배열 A[p...r]을 만든다.
}
~~~


~~~java
void merge(int data[], int p, int q, int r) {
  int i=p, j=q+1, k=p;
  int tmp[data.length()]; // 추가 배열

  while(i<=q && j<=r) { // 한쪽이 끝날 때까지 반복
    if (data[i] <= data[j])
      tmp[k++]=data[i++];
    else
      tmp[k++]=data[j++];
  }
  // 둘 중 하나가 끝나면
  while(i<=q)
    tmp[k++]=data[i++];
  while(j<=r)
    tmp[k++]=data[k++];

  // 추가 배열에 있는 것을 원래 배열에 옮겨줌
  for(int i=p; i<=r; i++)
    data[i]=tmp[i];
  }
~~~
O(n)

시간복잡도
\[
     T(n) = \begin{cases}
        0 & \text{if $n=1$} \\
       T(n/2)+T(n/2)+n & \text{otherwise} \\
     \end{cases}
\]
$$O(nlogn)$$

#### Quick sort
- 분할정복법
  분할 : 배열을 다움과 같은 조건이 만족되도록 두 부분으로 나눈다. (pivot 선정)
          elements in lower parts <= elements in upper parts
  정복 : 각 부분을 순환적으로 정렬한다.
  합병 : nothing to do

  1) 정렬할 배열이 주어짐. 마지막 수를 기준(pivot)으로 삼는다
  31 8 48 73 11 3 20 29 65 **15**
  2) 기중보다 작은 수는 기준의 왼쪽에 나머지는 기준의 오른쪽에 오도록 재배치(분할) 한다.
  8 11 3 **15** 31 48 20 29 65 73
  3) 기준의 왼쪽과 오른쪽을 각각 **순환적으로** 정렬한다(정렬 완료)
  *3 8 11* 15 *20 29 31 48 65 73*


~~~java
quickSort(A[], p, r) { // A[p...r]을 정렬한다.
  if (p<r) then {
    q = partition(A, p, r); // 분할 return : pivot의 위치
    quickSort(A, p, q-1); // 왼쪽 부분배열 정렬
    quickSort(A, q+1, r); // 오른쪽 부분배열 정렬
  }
}

partition(A[],p, r]) {
  배열 A[p...r]의 원소들을 A[r]을 기준으로 양쪽으로 재배치하고
  A[r]이 자리한 위치를 return 한다.

  // i= pivot보다 작은 값들 중 마지막값
  // j= 지금 검사하려는 값
  x <- A[r]; // pivot
  i<-p-1;
  for j<-p to r-1
  if A[j] <= x then
    i<-i+1;
    exchange A[i] and A[j];
  exchange A[i+1] and A[r];
  return i+1;
}
~~~
- 항상 한쪽은 0개, 다른 쪽은 n-1개로 분할되는 경우 (최악)
$
T(n) = T(0) + T(n-1) + \Theta(n)\\
= T(n-1) + \Theta(n)\\
= T(n-2) + T(n-1) + \Theta(n-1) + \Theta(n)\\
...\\
= \Theta(1) + \Theta(2) + \Theta(n-1) + \Theta(n)\\
= \Theta(n^2)
$

- 이미 정렬된 입력 데이터(마지막 원소를 pivot으로 선택하는 경우) (최악)
- 항상 절반으로 분할 되는 경우(최선)
$
T(n) = 2T(n/2) + \Theta(n)\\
=\Theta(nlogn)
$

- 항상 한쪽이 적어도 1/9 이상이 되도록 분할 된다면?
$
O(nlogn)
$
<br>
##### 평균시간복잡도
- "평균" 혹은 "기대값"이란?
$$
A(n) = \sum_{input instance I of size n}^{}p(I)T(I)
$$
p(I) : I가 입력으로 들어올 확률
T(I) : I를 정렬하는데 걸리는 시간
그러나, p(I)를 모름
p(I)에 관한 정절한 가정을 한 후 분석
예. 모든 입력 인스턴스가 동일한 확률을 가진다면 $p(I) = 1/n!$

rank of vivot | probability | result of partition | running time|
--------------|-------------|---------------------|-------------|
1             |1/n          |0:n-1                |A(0) + A(n-1)|
2             |1/n          |1:n-2                |A(1) + A(n-2)|
...           |             |...                  |             |
n             |1/n          |n-1:0                |A(n-1) + A(0)|
n             |1/n          |n-1:0                |A(n-1) + A(0)|

$$
A(n) = {2 \over N }\sum_{i=0}^{n-1}A(i)+\theta(n)=\Theta(nlog_2n)
$$

##### Pivot의 선책
- 첫번째 값이나 마지막 값을 피못으로 선택
  이미 정렬된 데이터 혹은 거꾸로 정렬된 데이터가 최악의 경우
    현실의 데이터는 랜덤하지 않으므로 (거꾸로) 정렬된 데이터가 입력으로 들어올 가능성을 매우 높음
    따라서 좋은 방법이라고 할 수 없음
- "Median of Three"
  첫번째 값과 마지막 값, 그리고 가운데 값 중에서 중간값(median)을 피못으로 선택
  최악의 경우 시간복잡도가 달라지지느 않음
- Randomized quickSort
  피봇을 랜덤하게 선택
  no worst case instance, but worst case execution
  평균 시간 복잡도(ONlogN)

#### Heap Sort
- 최악의 경우 시간 복잡도 $O(nlog_2n)$
- Sort in place - 추가 배열 불필요
- 이진힙 자료구조 사용

##### Full vs Complete Binary Trees
- full Binary tree : 모든 레벨에 노드들이 꽉 차있는 형태
- Complete Binary Trees : 마지막 레벨을 제외하면 완전히 꽉 차있고, 마지막 레벨에는 가장 오른쪽부터 연속된 몇 개의 노드가 비어있을 수 있음

##### Heap의 정의
(1) Complete Binary Tree 이면서
(2) Heap property를 만족
**max heap property(부모는 자식보다 크거나 같다)** vs min heap property(부모는 자식보다 작거나 같다)

##### Heap의 표현
- 힙은 일차원 배열로 표현 가능 : A[1..n]
  루트노드 A[1]
  A[i]의 부모 = A[i/2]
  A[i]의 왼쪽 자식 = A[2i]
  A[i]의 오른쪽 자식 = A[2i+1]

##### 기본 연산 : MAX-HEAPIFY
- 전체를 힙으로 만들어라
  트리의 전체 모양은 Complete Binary Tree
  유일하게 루트만이 heap property를 만족 안함
  왼쪽/오른쪽 부트리(subtree)가 그 자체로 heap
- 두 자식들 중 더 큰 쪽이 나보다 크면 exchange

##### MAX=HEAPIFY : recursive viersion
~~~java
// 노드 i를 루트로 하는 서브트리를 heapify한다
MAX-HEAPIFY(A, i) { // A: 힙
  if there is no child of A[i] // 자식이 없다면 종료
    return;
  k <- index of the biggest child of i; // 더 큰 자식 k
  if A[i] >= A[k] // 부모가 더 크다면 종료
    return;
  exchange A[i] and A[k]; // 교환
  MAX-HEAPIFY(A, k); // recursion
  // root노드에 대한 heapify는 MAX-HEAPIFY(1)을 호출하면  
}
~~~

##### MAX=HEAPIFY : iterative viersion
~~~java
// 노드 i를 루트로 하는 서브트리를 heapify한다
MAX-HEAPIFY(A, i) { // A: 힙
  while A[i] has a child do // 자식을 가진 동안에만 반복
    k <- index of the biggest child of i;
    if A[i] >= A[k]
      return;
    exchange A[i] and A[k];
    i=k;
  end.
}
~~~

##### 정렬할 배열을 힙으로 만들기
~~~java
BULD-MAx-HEAP(A)
heap-size[A] <- legnth[A]
for i <- length[A]/2 downto 1
  do MAX-HEAPIFY(A, i)
~~~
시간복잡도 : $O(n)$n

#### Heap sort
1. 주어진 데이터로 힙을 만든다.
2. 힙에서 최대값(루트)을 가장 마지막 값과 바꾼다.
3. 힙의 크기가 1 줄어든 것으로 간주한다. 즉, 가장 마지막 값은 힙의 일부가 아닌 것으로 간주한다.
4. 루트노드에 대해서 HEAPIFY(1)한다.
5. 2~4번을 반복한다.

~~~java
HEAPSORT(A)
BUILD-MAX-HEAP(A)                   : O(n)
for i<- i heap_size downto 2 do     : n-1 times    // i : 현재 마지막 노드
  exchange A[1] <-> A[i]            : O(1)
  heap_size <- heap_size - 1        : O(1)
  MAP_HEAPIFY(A, 1)                 : O(log_2n)
~~~
수행시간 : $O(nlog_2n)


#### 힙의 응용 : 우선순위 큐
- 최대 우선순위 큐(maximum priority queue)는 다음의 두 가지 연산을 지원하는 자료구조
  INSERT(x) : 새로운 원소를 삽입
  EXTRACT_MAX() : 최대값을 삭제하고 반환
- 최소 우선순위 큐(minimum priority queue)는 EXTRACT_MAX 대신 EXTRACT_MIN을 지원하는 자료구조
- MAX HAEP을 이용하여 최대 우선순위 큐를 구현

~~~java
MAX-HEAP-INSERT(A, key) { // A: heap
  heap_size = heap_size+1;
  A[heap_size] = key;
  i = heap_size; // 문제아노드
  while (i>1 and A[PARENT(i)] < A[i]) { // 루트가 아니고, 부모의값<문제값인 동안
    exchange A[i] and A[PARENT(i)];
    i < PARENT(i);

  }
}
~~~
시간복잡도 $O(log_2n)$
<br>
~~~java
HEAT-EXTRACT_MAX(A)
  if heap_size[A] < 1
    then error "heap underflow" // 예외처리
  max <- A[1]
  A[1] <- A[heap-size[A]]
  heap-size[A] <- heap-size[A] - 1
  MAX-HEAPIFY(A, 1)
  return max
~~~
시간복잡도 $O(log_2n)$


#### 정렬의 Lower Bound
- Comparison sort
  데이터들간의 **상대적 크기관계**만을 이용해서 정렬하는 알고리즘
  따라서 데이터들간의 크기 관계가 정의되어 있으면 어떤 데이터에든 적용가능 (문자열, 알파벳, 사용자 정의 객체 등)
  버블소트, 삽입정렬, 합병정렬, 퀵정렬, 힙정렬 등
- Non-Comparison sort
  정렬할 데이터에 대한 **사전지식**을 이용 - 적용에 제한
  Bucket sort
  Radix sort

##### 정렬문제의 하한
- 하한 (Lower Bound)
  입력된 데이터를 한번씩 다 보기위해서 최소 $\Theta(n)$의 시간 복잡도 필요
  합병정렬과 힙정렬 알고리즘들의 시갑 복잡도는 $\Theta(nlog_2n)$
  **어떤 Comparison sort 알고리즘도 $\Theta(nlog_2n)$보다 나을 수 없다**


##### Decision Tree
- 3개의 값을 정렬하는 삽입정렬알고리즘에 대한 Decision Tree
- Leaf노드의 개수는 n!  -> 모든 순열에 해당하므로
- 최악의 경우 시간복잡도는 트리의 높이
- 트리의 높이는
height $\geq log_2n! = \Theta(nlog_2n)$

#### Sorting in linear time
- Counting Sort
  n개의 정수를 정렬하라. 단 모든 정수는 0에서 k사이의 정수이다.
  예: n명의 학생들의 시험점수를 정렬하라. 단 모든 점수는 100이하 양의 정수이다.

~~~java
int A[n]; // 정렬할 데이터
int C[k] = {0,};
for(int i=1; i<n; i++)
  C[A[i]]++;
for(int s=1, i=0; i<=k; i++) {
  for(int j=0; j<C[i]; j++) {
    A[s++] = ㅑ ;
  }
}
~~~
=> Is is okay? No~~ 대부분의 경우 정렬할 key값들은 레코드의 일부분이기 때문

~~~java
COUNTING-SORT(A, B, k) {
  // 0으로 초기화
  for i <- 0 to k
    do C[i] <- 0

  // data countnig
  for j <- 1 to length[A]
    do C[A[j]] <- C[A[j]] + 1
  => C[i] now cont ains the number of elements equal to i.

  // 누적합 구하기 C[i-1] : 이전의 누적함
  for i <- 1 to k
    do C[i] <- C[i] + C[i-1]
  => C[i] now contains the number of elements less than or equal to i.

  // 저장할 위치 찾아서 저장
  for j <- length[A] downto 1
    do B[C[A[j]]] <- A[j]
       C[A[j]] <- C[A[j]] - 1
}
~~~

##### 시간복잡도
- $\Theta(n+k)$, 또는 $\Theta(n)$ if k=o(n) -> 선형시간
- k가 클 경우 비실용적
- Stable 정렬 알고리즘
  "입력에 동일한 값이 있을 때 입력에 먼저 나오는 값이 출력에서도 먼저 나온다"
  **Counting정렬은 Stable하다**

#### Sorting in linear time: Radix Sort
- n개의 d자리 정수들
- 가장 **낮은** 자리수부터 정렬

~~~java
RADIX-SORT(A, d)
for i <- 1 to default:
    do use a stable sort to sort array A on digit i
~~~
시간복잡도 O(d(n+k))

#### 정렬 알고리즘
|Sort Algorithm | T(n)|
|---------------|-----|
|Bubble Sort| $\theta(n^2)$|
|Insertion Sort |  $\theta(n^2)$|
|Selection Sort| $\theta(n^2)$|
|Quick Sort| worst  $\theta(n^2)$ and average  $\theta(nlog_2n)$|
|Merge Sort | $\theta(nlog_2n)$|
|Heap Sort|$\theta(nlog_2n)$|
|Counting Sort|$\theta(n+k)$|
|Radix Sort | $\theta(d(n+k))$

#### JAVA에서의 정렬
##### 기본타입 데이터의 정렬
- Arrays 클래스가 primitive 타입 데이터를 위한 정렬 메서드를 제공
~~~java
int [] data = new int [capacity];
// data[0]에서 data[capacity-1]까지 데이터가 꽉 차있는 경우에는 다음과 같이 정렬한다.
Arrays.sort(data);
// 배열이 꽉차있지 않고 data[0]에서 data[size-1]까지
// size개의 데이터만 있다면 다음과 같이 한다.
Arrays.sort(data, 0, size);
~~~
- int 이외의 다른 primitive타입 데이터 (double, char 등)에 대해서도 제공

<br>
##### 객체의 정렬 : 문자열
~~~java
String [] fruits = new String [] {"pineapple", "apple", "orange", "banana"};
Arrays.sort(fruits);
for(String name : fruits)
  System.out.println(name);
~~~

<br>
##### ArrayList 정렬 : 문자열
~~~java
List<String> fruits = new ArrayList<String>();
fruits.add("pineapple");
fruits.add("apple");
fruits.add("orange");
fruits.add("banana");

Collections.sort(fruits);

for(String name: fruits) {
  System.out.println(name);
}
~~~

<br>
##### 객체의 정렬 : 사용자 정의 객체
~~~java
public class Fruit implements Comparable<Fruit>{
  public String name;
  public int quantity;
  public Fruit(String name, int quantity) {
    this.name = name;
    this.quantity = quantity;
  }

  // 방법1-1. Comparable Interface -이름 순으로 정렬
  public int compareTo(Fruit other) {
    return name.compareTo(other.name);
  }

  // 방법1-2. Comparable Interface -재고 수량으로 정렬
  public int compareTo(Fruit other) {
    return quantity - other.quantity;
  }

}

// somewhere in your program
Fruit [] fruits = new Fruit[4];
fruits[0] = new Frut("pineapple", 70);
fruits[1] = new Frut("apple", 100);
fruits[2] = new Frut("orange", 80);
fruits[3] = new Frut("bananan", 90);

Arrays.sort(fruits);
~~~
<br>
##### 객체의 정렬 : 사용자 정의 객체 - 두 가지 이상의 기준
~~~java
public class Fruit{
  public String name;
  public int quantity;
  public Fruit(String name, int quantity) {
    this.name = name;
    this.quantity = quantity;
  }

// Comparator 인터페이스를 extends하여 compare메서드를 overring하는
// 새로운 이름 없는 클래스를 정의한 후 그 클래스의 객체를 하나 생성한다.
  public static Comparator<Fruit> nameComparator = new Comparator<Fruit>() {
    public int compare(Fruit fruit1, Fruit fruit2) {
      return fruit1.name.compareTo(fruit2.name);
    }
  }

  public static Comparator<Fruit> quanComparator = new Comparator<Fruit>() {
    public int compare(Fruit fruit1, Fruit fruit2) {        
      return fruit1.quantity - fruit2.quantity;
    }
  }
}

// somewhere in your program
Fruit [] fruits = new Fruit[4];
fruits[0] = new Frut("pineapple", 70);
fruits[1] = new Frut("apple", 100);
fruits[2] = new Frut("orange", 80);
fruits[3] = new Frut("bananan", 90);

Arrays.sort(fruits, Fruit.nameComparator);
//or
Arrays.sort(fruits, Fruit.quanComparator);
~~~
<br>
<br>
출처 : https://www.inflearn.com/course/알고리즘-강좌/dashboard 인프런 영리한 프로그래밍을 위한 알고리즘 강좌
