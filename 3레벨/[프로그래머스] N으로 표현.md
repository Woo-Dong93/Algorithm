# [프로그래머스] N으로 표현

- DP를 활용한 문제 입니다.
- 숫자 5를 가지고 DP를 활용해보겠습니다.
  - 1번 사용 : 5
  - 2번 사용 : 55(붙여쓰기) / 5+5, 5-5, 5*5, 5/5
  - 3번사용 : 555(붙여쓰기) / (5+55, 5+5+5, 5+5-5, 5+5\*5, 5+5/5) = 더하기 연산...
  - 이것을 바탕으로 N번을 사용
    - 연달아 붙인 수 
    - 1번 SET과 N-1 SET을 사칙연산으로 조합한 수
    - 2번 SET과 N-2 SET을 사칙연산으로 조합한 수
    - 즉 i+j==k 일 때 4칙연산을 모든 경우의 수로 탐색하면 됩니다.



- 불필요한 값 제거
  - N의 최소 개수로 number을 만드는 것이기 때문에 0이 들어 있다면 그냥 개수만 들어가는 것이니 제외시켜야 합니다. ( 0이 나오는 경우는 뺄셈과 나눗셈 )
  - 마이너스(-) 연산을 통해 나온 음수 값은 위의 규칙에 따라서 무저 같은 절대 값을 가진 양수값을 가지게 됩니다. 그래서 이 수들은 +,- 연산을 하게 되면 중복된 값이 들어가므로 -숫자들은 들어갈 필요가 없습니다.
    - -3, 3 => n+(3) , n-(3) == n+(-3) , n-(-3)

- 소스코드

```java
import java.util.*;

class Solution {
    public int solution(int N, int number) {
        int answer = -1;
        
		//숫자 8개를 사용해서 만들 수 있는 수들의 집합을 저장하는 배열
        ArrayList<HashSet<Integer>> list = new ArrayList<HashSet<Integer>>();
        for (int i = 0; i < 8; i++) {
        	list.add(new HashSet<Integer>());
		}
        list.get(0).add(N);
        if(list.get(0).contains(number)) return 1;
        
        for (int k = 1; k < 8; k++) {
        	
        	int num = N;
        	for (int i = 0; i < k; i++) {
				num = num*10+N;
			}
        	list.get(k).add(num);
			
        	for (int i = 0; i < k; i++) {
        		for (int j = 0; j < k; j++) {
        			if(i+j+1==k) {
        				
        				//완전 탐색
        				for (int a : list.get(i)) {
							for (int b : list.get(j)) {
								list.get(k).add(a+b);
								list.get(k).add(a*b);
								if(a-b>0)list.get(k).add(a-b);
								if(a/b>0)list.get(k).add(a/b);
							}
						}	
        			}
        		}
        	}
        	
        	if(list.get(k).contains(number)) return k+1;
		}
       
        
        return answer;
    }
}
```

