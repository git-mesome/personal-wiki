# Knight's Move

{% embed url="https://www.acmicpc.net/problem/7562" %}

### 문제해석 <a href="#undefined" id="undefined"></a>

* 체스판 위 나이트로 움직일 수 있는 칸이 있다.
* 나이트로 특정 칸으로 이동할 때 횟수

​

### 입력 <a href="#undefined-1" id="undefined-1"></a>

1. 1.테스트 케이스의 개수
2. 2.체스판의 한변의 길이 l -> 체스판의 크기 lxl
3. 3.나이트의 현재 위치
4. 4.나이트가 이동하려는 칸
5. 5.2-4 반

​**나이트의 이동 패턴**(0, 0) -> (1, 2), (2, 1), (2, -1), (1, -2), (-1, 2), (-2, 1), (-2, -1), (-1, -2)

```java
package bfs;

import java.io.*;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class nightMove7562 {
  static int[][] chess;
  static int length;
  static final int[] dx = {1, 1, 2, 2, -1, -1, -2, -2};
  static final int[] dy = {2, -2, 1, -1, 2, -2, 1, -1};

  public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    StringTokenizer st;
    Queue<PointXY> queue = new LinkedList<>();
    int testCase = Integer.parseInt(br.readLine());

    for (int i = 0; i < testCase; i++) {
      length = Integer.parseInt(br.readLine());
      chess = new int[length][length];

      st = new StringTokenizer(br.readLine()); // 현재 위치
      int x = Integer.parseInt(st.nextToken());
      int y = Integer.parseInt(st.nextToken());
      chess[x][y] = 1;
      queue.add(new PointXY(x, y));

      st = new StringTokenizer(br.readLine()); // 가고자하는 위치
      x = Integer.parseInt(st.nextToken());
      y = Integer.parseInt(st.nextToken());

      while (!queue.isEmpty()) {
        PointXY check = queue.poll();

        for (int j = 0; j < 8; j++) {
          int nx = check.x + dx[j];
          int ny = check.y + dy[j];

          if (nx >= 0 && ny >= 0 && nx < length && ny < length) {

            if(chess[nx][ny] == 0 ){
              chess[nx][ny] = chess[check.x][check.y] + 1;
              queue.add(new PointXY(nx,ny));
            }

          }

        }
      }
      bw.write(chess[x][y] - 1 + "\n");
    }
    bw.flush();
    bw.close();
    br.close();
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
