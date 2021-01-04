---
layout: post
title: Algorithm | 순환
hide_title: true     
date: 01 january 2021
excerpt_separator: <!--more-->
---

## 순환(Recursion)
<!--more-->
자기 자신을 호출하는 함수, 재귀함수

#### Recursion이 무한 루프에 빠지지 않는 조건
Base case : 적어도 하나의 recursion에 빠지지 않는 경우가 존재애야한다.
Recursion case : recursion 을 반복하다보면 결국 base case로 수렴해야 한다.

#### 최대 공약수 : Euclid Method

#### 순환적 알고리즘 설계
암시적(implicit) 매개변수를 명시적(explicit) 매개변수로 바꾸어라.


#### 미로찾기
현재 위치에서 출구까지 가는 경로가 있으려면
1) 현재 위치가 출구이거나 혹은
2) 이웃한 셀들 중 하나에서 현재 위치를 지나지 않고 출구까지 가는 경로가 있거나

#### 미로찾기(Decision Problem)

~~~java
boolean findPath(x, y) 
	if (x, y) is the exit // 출구인 경우
		return true;
	else 
		for each neighbouring cell (x', y') of (x, y) do // 인접한 셀 4개에 대해서
			if (x', y') is on the pathway // 인접한 셀이 경로이면
				if findPath(x', y') // 출구가 있는 경로가 있는지 recursion으로 검사
					return trur;
		return false;
~~~

무한 루프에 빠지지 않기 위해 가본 위치와 가보지 않은 위치를 구분
~~~java
boolean findPath(x, y)
	if (x, y) is the exit
		return true;
	else
		mark (x, y) as a visited cell; // 방문된 위치라는 것을 표시
		for each neighbouring cell (x', y') of (x, y) do // 인접한 셀 4개에 대해서
			if (x', y') is on the pathway and not visited // 방문하지 않는 셀 조건 추가
				return true;
		return false;
~~~

~~~java
boolean findPath(x, y)
	if (x, y) is either on the wall or a visited cell // 방문된 위치라면 false return
		return false;
	else if (x, y) is the exit
		return true;
	else
		mark (x, y) as a visited cell; // 방문된 위치라는 것을 표시
		for each neighbouring cell (x', y') of (x, y) do // 인접한 셀 4개에 대해서
			if findPath (x', y')
				return true;
		return false;
~~~

#### class Maze

~~~ java 
public class Maze {
	private static int N = 8;
	private static int [][] maze = {
		{0, 0, 0, 0, 0, 0, 0, 1},
		{0, 1, 1, 0, 1, 1, 0, 1},
		{0, 0, 0, 1, 0, 0, 0, 1},
		{0, 1, 0, 0, 1, 1, 0, 0},
		{0, 1, 1, 1, 0, 0, 1, 1},
		{0, 1, 0, 0, 0, 1, 0, 1},
		{0, 0, 0, 1, 0, 0, 0, 1},
		{0, 1, 1, 1, 0, 1, 0, 0}
	};

	private static final int PATHWAY_COLOUR = 0;	// white
	private static final int WALL_COLOUR = 1; 		// blue
	private static final int BLOCKEN_COLOUR = 2;	// red visited이며 출구까지의 경로상에 있지 않음이 밝혀진 cell
	private static final int PATH_COLOUR = 3;		// green visited이며 아직 출구로 가는 경로가 될 가능성이 있는  cell


	public static boolean findMazePath(int x, int y) {
		if ( x<0 || y<0 || x>=N || y>=N) // 좌표가 유효한지 확인
			return false;
		else if ( maze[x][y] != PATHWAY_COLOUR) // visited
			return false;
		else if ( x == N-1 && y == N-1) { // 출구
			maze[x][y] = PATH_COLOUR; // 방문
			return true;
		}
		else {
			maze[x][y] = PATH_COLOUR; // visited
			if ( findMazePath(x-1, y) || findMazePath(x, y+1)
				|| findMazePath(x+1, y) findMazePath(x, y-1)) { // 네방향을 검사
				return true;
			}
			maze[x][y] = BLOCKEN_COLOUR;		// dead end
			return false;
		}
	}

	public static void main(String [] args) {
		printMaze();
		findMazePath(0,0);
		printMaze();
	}
}
~~~


#### Count Cells in a Blob
- Binary 이미지
- 각 픽셀은 background pixel 이거나 혹은 image pixel
- 서로 연결된 image pixel들의 집합을 blob이라고 부름
- 상하좌우 및 대각방향으로도 연결된 것으로 간주

- 입력
	n*n 크기의 2차원 그리드
	하나의 좌표 (x, y)
- 출력
	픽설(x, y)가 포함된 blob의 크기
	(x, y)가 어떤 blob에도 속하지 않는 경우에는 0

#### Count Cells in a Blob(Recursive Thinking)
현재 픽셀이 속한 blob의 크기를 카운트하려면
	현재 픽셀이 image color가 아니라면
		0을 반환한다
	현재 필셀이 image color라면
		먼저 현재 픽셀을 카운트한다(count=1)
		현재 픽셀이 중복 카운트되는 것을 방지하기 위해 다른 색으로 칠한다.
		현재 픽셀에 이웃한 모든 픽셀들에 대해서
			그 픽셀이 속한 blob의 크기를 카운트하여 카운터에 더해준다.
		카운터를 반환한다.

Algorithm for countCells(x, y)
if the pixel (x, y) is outside the grid
	the result is 0;
else if pixel(x, y) is not an image pixel or already counted
	the result is 0;
else
	set the colour of the pixel (x, y) to a red colour;
	the result is 1 plus the number of cells in each piece of 
		the blob that includes a nearest neighbour;

~~~ java
private static int BACKGROUNE_COLOR = 0;
private static int IMAGE_COLOR= 1;
private static int ALREADY_COUNTED = 2;

public int countCells(int x, int y) {
	int result;
	if (x<0 || x>=N || y<0 || y>=N) 
		return 0;
	else if(grid[x][y] != IMAGE_COLOR)
		return 0;
	else {
		grid[x][y] = ALREADY_COUNTED;
		return 1+ countCells(x-1, y+1) + countCells(x, y+1)
			+ countCells(x+1, y+1) + countCells(x-1, y)
			+ countCells(x+1, y) + countCells(x-1, y-1)
			+ countCells(x, y-1) + countCells(x+1, y-1);
	}
} 
~~~


#### N queens problem

#### 상태공간트리
상태공간트리란 찾는 해를 포함하는 트리
즉 해가 존재한다면 그것은 반드시 이 트리의 어떤 한 노드에 해당함
따라서 이 트리를 체계적으로 탐색하면 해를 구할 수 있음

#### Backtracking
상태공간 트리를 깊이 우선 방식으로 탐색하여 해를 찾는 알고리즘
상태공간 트리의 모든 노드를 탐색해야 하는 것은 아님


#### Design Recursion
~~~ java
int [] cols = new int [N+1]; 	// 매개변수 level은 현재 노드의 
// cols[1] : 1번 말이 놓인 열번호 
// ...
// colse[level] = level 말이 놓이 열변호

boolean queens(int level) { // 매개변수는 내가 현재 트리의 어떤 노드에 있는지를 지정해야 한다.
	if non-promising 			// 이 밑으로 내려갈 필요가 없다
		report failure and return;
	else if success 			// 내가 찾던 노드가 맞는가
		report answer and return;
	else 						// 자식 노드를 방문
		visit children recursively;
}
~~~

~~~ java
int [] cols = new int [N+1];
boolean queens (int level) {
	if (!promising(level)) 
		return flase;
	else if (level==N) 
		for(int i=1; i<=N; i+++) 
			System.out.println("(" + i + ", " + cols[i] + ")"); 
		return true;
	for(int i=1; i<N; i++) {
		cols[level+1] = i;
		if(queens(level+1))
			return true;
	}
	return false;
}

// PromisingTest 말들 간에는 충돌이 없음이 보장되어 있음 따라서 마지막에 놓이 이 말이 이전에 놓인 다른 말들과 충돌하는지 검사하는 것으로 충분
boolean promising(int level) {
	for(int i=1; i<level; i++) {
		if (cols[i] == cols[level]) // 같은 열에 놓였는지 검사
			return false;
		else if (level-i==Math.abs(cols[level]-cois[i])) // 같은 대각선에 놓였는지 검사
			return false;
	}
	return true;
}
~~~ 

### 멱집합(PowerSet)
임의의 집합.data의 모든 부분집합

{a, b, c, e, d, f}의 모든 부분집합을 나열하려면
	a를 제외한 {b, c, d, e, f}의 모든 부분 집합들을 나열하고
	{b, c, d, e, f}의 모든 부분집합에 {a}를 추가한 집합들을 나열한다.

.... 반복

~~~java
powerSet(S) 	// Mission : s의 멱집합을 출력하라
if s is an empty set
	print nothing;
else
	let t be the first element of s;
	find all subsets of s-{t} by calling powerSet(s-{t});
	print the subsets;
	print the subsets with adding t;
// 이렇게 하려면  poswerSet 함수는 여러 개의 잡합들을 return 해야한다. 어떻게?
~~~

~~~java
poswerSet(P, S)		// Misstion : S의 멱집합을 구한 후 각각에 집합 P를 합집합하여 출력하라
if S is an empty set
	print P;
else 
	let t be the first element of S;
	powerSet(P. S-{t}); 	// t 포함
	powerSet(PU{t}, S-{t}); // t 포함 안함 
	// 집합 S 는 k 번째 요소부터 끝까지
	// 집합 P는 0~k-1 원소 중에 일부

// Recursion 함수가 두 개의 집합을 매개변수로 받도록 설계해야 한다는 의미이다.
// 두 번째 집합의 모든 부분집합들에 첫번째 집합을 합집합하여 출력한다.

~~~

~~~java
// Mission : data[k], ... , data[n-1]의 멱집합을 구한 후 각각에 include[i]=true, i=0, ..., k-1인 원소를 추가하여 출력하라
// 처음 이 함수를 호출할 때는 powerSet(0)로 호출한다. 즉 P는 공집합이고 S는 전체 집합이다.
private static char data[] = {'a', 'b', 'c', 'd', 'e', 'f'};
private static int n=data.length;
private static boolean [] include = new boolean[n];

public static void powerSet(int k) { 	// 트리상에서 현재 나의 위치를 표현
	if (k==n) { 						// 만약 내 위치가 리프노드라면
		for(int i=0; i<n; i++) 
			if(include[i]) System.out.println(data[i] + " ");
		System.out.pirntln();
		return;
	}
	// data[k] 포함 안함
	include[k] = false;
	powerSet(k+1); 						// 왼쪽으로 내려갔다가

	// data[k] 포함
	include[k] = true;
	powerSet(k+1); 						// 오른쪽으로 내려감
}
~~~
