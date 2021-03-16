# [백준 9470] Strahler 순서

- 위상정렬을 통해 해결할 수 있습니다.
- 순위는 따로 최대값을 저장하는 배열을 만든 후에 2개이상있을때만 확인해서 ++해주면 해결됩니다.



- 소스코드

```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.*;

class study9 {
	static StringTokenizer st;
	static int k, m, p;
	static ArrayList<ArrayList<Integer>> list;
	static int[] link;
	static int[] rank;
	static int[] cntLink;
	static BufferedWriter bw;
	static Queue<Integer> que;
	public static void main(String[] args) throws NumberFormatException, IOException {
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		bw = new BufferedWriter(new OutputStreamWriter(System.out));
		
		int t = Integer.parseInt(br.readLine());
		
		for (int i = 0; i < t; i++) {
			st = new StringTokenizer(br.readLine());
			k = Integer.parseInt(st.nextToken());
			m = Integer.parseInt(st.nextToken());
			p = Integer.parseInt(st.nextToken());
			
			list = new ArrayList<>();
			link = new int[m+1];
			rank = new int[m+1];
			cntLink = new int[m+1];
			
			for (int j = 0; j <= m; j++) {
				list.add(new ArrayList<>());
			}
			
			for (int j = 0; j < p; j++) {
				st = new StringTokenizer(br.readLine());
				int v1 = Integer.parseInt(st.nextToken());
				int v2 = Integer.parseInt(st.nextToken());
				list.get(v1).add(v2);
				link[v2]++;
			}
			// 입력 끝
			topologicalSort();
			
			bw.write(k+" "+rank[m]);
			bw.newLine();
		}
		bw.flush();
		bw.close();
	}
	static void topologicalSort() throws IOException {
		
		que = new LinkedList<>();
		for (int i = 1; i < link.length; i++) {
			if(link[i]==0) {
				que.add(i);
				rank[i] = 1;
			}
		}
		
		for (int i = 0; i < m; i++) {
			
			int num = que.poll();
			for (int j = 0; j < list.get(num).size(); j++) {
				
				int v = list.get(num).get(j);
				link[v]--;
				
	
				if(rank[v]<=rank[num]) {
					if(rank[v]==rank[num]) {
						cntLink[v]++;
					}else {
						cntLink[v] = 1;
					}
					rank[v] = rank[num];
				}
			
				
				if(link[v]==0) {
					que.add(v);
					if(cntLink[v]>1) {
						rank[v]++;
					}
				}
			}
			
		}
		
	}

}
```

