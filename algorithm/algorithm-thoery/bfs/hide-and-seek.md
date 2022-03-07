# Hide And Seek

{% embed url="https://www.acmicpc.net/problem/1697" %}

### 문제 접근

수빈이가 동생을 찾을 수 있는 가장 빠른 시간을 구하는 문제 → 최단 거리 → **BFS**

수빈의 위치 X → 1초 후 X-1, X+1, X\*2 이동

* 0초일 때 X위치
* 1초일 때 X-1, X+1, X\*2 위치

### **※ 문제의 힌트**

수빈이가 5-10-9-18-17 순으로 가면 4초만에 동생을 찾을 수 있다.

**0초**

* 0초 일때 인덱스에 1을 저장한다.(왔던 경로를 표시하기 위함)
* 수빈이의 현재 위치 5

![](<../../../.gitbook/assets/image (3).png>)

**1초**

* 이동 시간이 1초일 때 위치 값

![](<../../../.gitbook/assets/image (7).png>)

**2초**

* 이동 시간이 2초일 때 위치 값
* 현재 위치인 4,6,10에서 이동한 위치
* 방문한 곳은 작성하지 않는다.

![](<../../../.gitbook/assets/image (5).png>)

**3초**

* 이동 시간이 3초일 때 위치 값
* 현재 위치인 3,7,8,9,11,12,20



**4초**

* 이동 시간이 4초일 때 위치 값
* 현재 위치인 2, 13, 14, 16, 17, 18, 22, 24

~~이해를 돕기위함이므로 30까지만 했습니다.~~

![](<../../../.gitbook/assets/image (4).png>)

동생 위치(17)에 값이 5가 저장되어있다. 시작한 경로 값이 1이므로 1을 빼주고 4를 출력한다.

### 전체 코드

```java
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

public class HideAndSeek1697 {

  static int N;
  static int K;
  static int[] point = new int[100001];

  public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    N = sc.nextInt();
    K = sc.nextInt();

	 	//동생과 수빈의 위치가 같을 경우
    if (N == K) {
      System.out.println(0);
    } else {
      bfs(N);
    }
  }

  static void bfs(int num) {

    Queue<Integer> queue = new LinkedList<>();
    queue.add(num);
		//처음 위치값 1
    point[num] = 1;

    while (!queue.isEmpty()) {
      int next = queue.poll();

      int x1 = next + 1;
      int x2 = next - 1;
      int x3 = next * 2;

			//좌표안에 있고 안 간 경로라면
      if (x1 <= 100000 && point[x1] == 0) {
				//현재 위치값 + 1
        point[x1] = point[next] + 1;
        queue.add(x1);
      }

      if (x2 >= 0 && point[x2] == 0) {
        point[x2] = point[next] + 1;
        queue.add(x2);
      }

      if (x3 <= 100000 && point[x3] == 0) {
        point[x3] = point[next] + 1;
        queue.add(x3);
      }

    }
		//처음 위치가 1이므로 1을 빼준다.
    System.out.println(point[K] - 1);
  }

}
```
