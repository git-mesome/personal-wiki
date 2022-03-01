# Maze Exploration

{% embed url="https://www.acmicpc.net/problem/2178" %}

### 문제 접근

미로 , **최단 경로** 사용 → BFS를 사용하자

1. 인접 노드가 1이면 Queue에 추가하자.

1-1 . 인접 노드 구하기 → 상하좌우를 알아야 한다.

![](<../../../.gitbook/assets/image (3).png>)

*   code

    ```java
    int [] dx = {1, 0, -1, 0};
    int [] dy = {0, 1, 0, -1};
    ```

2\. 이동할 수 있는 곳이면 해당 좌표에 +1 반복해주어 도착지점까지 이동한 횟수를 알아내자.

* code

```java
while (!queue.isEmpty()) { // 주변에 1이 없을 때까지
        PointXY check = queue.poll();

        if (check.x == width - 1 && check.y == height - 1) {
          break;
        }
        //상, 하, 좌, 우 탐색 반복문
        for (int i = 0; i < dx.length; i++) {
          int nx = check.x + dx[i];
          int ny = check.y + dy[i];

          //0보다 크고 행,열보다 작을때 진입
          if (nx >= 0 && ny >= 0 && nx < width && ny < height) {

            if (maze[nx][ny] == 1) {
              maze[nx][ny] = maze[check.x][check.y] + 1;
              queue.add(new PointXY(nx, ny));
            }
          }
        }
      }
```

* 입력 값과 이동 횟수&#x20;

![](<../../../.gitbook/assets/image (2).png>)

1일 때 진입 가능하므로 현재 위치의 maze 배열 값이 1이면 기준 좌표 값에서 1을 더하여 현재 배열 값을 더한다. 방문한 경로는 2이상이 되므로 조건문 if (maze\[nx]\[ny] == 1) 을 만족시키지 않기 때문에 재방문하지 않는다. 즉, 0과 2이상의 배열값은 <mark style="color:red;">갈 수 없는 경로</mark>가 되는 것이다.

### 전체 코드

```java
package bfs;

import java.io.*;
import java.util.LinkedList;
import java.util.Queue;

public class Main {
    static int[][] maze;
    static int[] dx = {-1, 0, 0, 1};
    static int[] dy = {0, 1, -1, 0};
    static int width;
    static int height;
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    public static void main(String[] args) throws IOException {
      String[] input = br.readLine().split(" ");
      height = Integer.parseInt(input[0]);
      width = Integer.parseInt(input[1]);
      maze = new int[width][height];

      for (int h = 0; h < height; h++) {
        String inputLine = br.readLine();
        for (int w = 0; w < width; w++) {
          maze[w][h] = inputLine.charAt(w) - '0';
        }
      }
      bfs(0, 0);
      bw.flush();
      bw.close();
      br.close();
    }

    static void bfs(int x, int y) throws IOException {
      //BFS 위한 큐 객체
      Queue<PointXY> queue = new LinkedList<>();
      //초기 0.0좌표 삽입
      queue.add(new PointXY(x, y));

      while (!queue.isEmpty()) { // 주변에 1이 없을 때까지
        PointXY check = queue.poll();

        if (check.x == width - 1 && check.y == height - 1) {
          break;
        }
        //상, 하, 좌, 우 탐색 반복문
        for (int i = 0; i < dx.length; i++) {
          int nx = check.x + dx[i];
          int ny = check.y + dy[i];

          //0보다 크고 행,열보다 작을때 진입
          if (nx >= 0 && ny >= 0 && nx <width && ny < height) {

            if (maze[nx][ny] == 1) {
              maze[nx][ny] = maze[check.x][check.y] + 1;
              queue.add(new PointXY(nx, ny));
            }
          }
        }
      }
      bw.write(maze[width-1][height-1] + "");
    }

    static class PointXY {
      int x;
      int y;

      PointXY(int x, int y) {
        this.x = x;
        this.y = y;
      }
    }
}
```
