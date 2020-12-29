# [프로그래머스] N-Queen

- 하나의 1차원 배열을 이용해 칼럼 index를 저장합니다.
- 같은 열에 있는지 판단해주고 또한 같은 대각선에 있는지 판단합니다.
- 같은 대각선은 y1-y2의 절대값과 x1-x2의 절재값이 동일하면 같은 대각선에 존재하는 것입니다.



- 소스코드

```java
class Solution {
    static int answer;
	static int[] col;
    public int solution(int n) {
        for (int i = 0; i < n; i++) {
			col = new int[n];
			col[0] = i;
			dfs(1, n);
		}
        return answer;
    }
    static void dfs(int row, int n) {
		if(row==n) {
			answer++;
			return;
		}
		
		for (int i = 0; i < n; i++) {
			col[row] = i;
			if(isPossible(i, row, n)) {
				dfs(row+1, n);
			}
		}
	}
	static boolean isPossible(int index, int row, int n) {
		
		for (int i = 0; i < row; i++) {
			
			if(col[i]==index) return false;
			
			if(Math.abs(i-row) == Math.abs(col[i]-index)) return false;
		}

		return true;
	}
}
```

