# [백준 15591] MooTube(Silver)

- 이 문제의 핵심은 정점이 N개 일 때 N-1개의 쌍을 가지고 있고 모든 정점이 연결되어있다는 의미는 그래프가 **스패닝 트리**임을 알 수 있습니다.
- 그래서 만약에 K보다 작은 정점이 나오게 되면은 다른 정점으로 가는 것을 멈춰주면 됩니다.
- 또한 그래프는 인접리스트로 구현하였습니다.
- BFS 시간복잡도(인접리스트) : O(V(정점)+E(간선))
- 전체 시간 복잡도 : O(5000+5000) * 5000(질문 수)



- 소스코드

```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.*;

class Main {
	static StringTokenizer st;
	static int n, m, count;
	static ArrayList<ArrayList<node>> list;
	static boolean[] visit;
	public static void main(String[] args) throws NumberFormatException, IOException {
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		st = new StringTokenizer(br.readLine());
		n = Integer.parseInt(st.nextToken());
		m = Integer.parseInt(st.nextToken());
		list = new ArrayList<>();
		for (int i = 0; i <= n; i++) {
			list.add(new ArrayList<>());
		}
		
		for (int i = 0; i < n-1; i++) {
			st = new StringTokenizer(br.readLine());
			int x = Integer.parseInt(st.nextToken());
			int y = Integer.parseInt(st.nextToken());
			int v = Integer.parseInt(st.nextToken());
			list.get(x).add(new node(y,v));
			list.get(y).add(new node(x,v));
		}
		
		for (int i = 0; i < m; i++) {
			st = new StringTokenizer(br.readLine());
			int k = Integer.parseInt(st.nextToken());
			int num = Integer.parseInt(st.nextToken());
			
			count = 0;
			bfs(k, num);
			System.out.println(count);
		}
	}
	static void bfs(int k, int num) {
		Queue<Integer> que = new LinkedList<>();
		que.add(num);
		visit = new boolean[n+1];
		visit[num] = true;
		
		while(!que.isEmpty()) {
			int idx = que.poll();
			
			for (int i = 0; i < list.get(idx).size(); i++) {
				int end = list.get(idx).get(i).idx;
				if(!visit[end] && list.get(idx).get(i).v >= k) {
					visit[end] = true;
					que.add(end);
					count++;
				}
			}
		}
	}
}
class node {
	int idx;
	int v;
	
	public node(int idx, int v) {
		super();
		this.idx = idx;
		this.v = v;
	}
}
```

