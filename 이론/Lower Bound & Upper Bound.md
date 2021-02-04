# Lower Bound & Upper Bound

- 이진탐색을 활용한 알고리즘입니다.
- 원하는 값을 못 찾았을 때 -1 등을 반환하는 이진탐색과는 달리 **Lower Bound & Upper Bound**는 원하는 값을 초과하는 첫번째 위치, 원하는 값 이상의 첫번째 위치를 반환합니다.
- 정렬된 배열에서 찾고자 하는 key가 있을 때
  - Upper Bound : 원하는 **key**를 초과한 값이 처음 나오는 위치를 찾는 과정
  - Lower Bound : 원하는 **key** 이상이 처음 나오는 위치를 찾는 과정

```java
// { 1, 3, 3, 5, 7 }
key = 3; // Upper Bound = 3(인덱스), Lower Bound = 1(인덱스) 
key = 2; // Upper Bound = 1(인덱스), Lower Bound = 1(인덱스)
```



### 1. Upper Bound 구현

- key보다 큰 첫번째 위치를 찾는 것이기 때문에 `if(arr[mid] <= key) front = mid + 1`을 해야 합니다.
  - key값을 찾았어도 front값을 증가시켜 줍니다.

```java
static int upperBound(int arr[], int front, int rear, int key) {
    int mid = 0;
    while(front<rear) {
        mid = (front+rear)/2;
        if(arr[mid] <= key) front = mid+1;

        // 기존 이진탐색은 mid-1이지만 mid를 포함해야 최종 결가값이 언제나 rear에 위치하게 됩니다.
        else rear = mid;
    }
    return rear;
}
```



### 2. Lower Bound 구현

- key보다 크거나 같은 첫번째 위치를 찾는 것이기 때문에  `if(arr[mid] < key) front = mid + 1` 을 해야 합니다.
  - 키 값을 찾았을 때도 포함해서 front를 변경하는 것이 아닌 키 값보다 작을 땜나 front을 변경합니다.

```java
static int lowerBound(int arr[], int front, int rear, int key) {
    int mid = 0;
    while(front<rear) {
        mid = (front+rear)/2;
        // 키값보다 작을 때 front를 변경
        if(arr[mid]<key) front = mid + 1;
        else rear = mid;
    }

    return rear;
}
```



### 3. 소스코드

```java
class Solution 

	public static void main(String[] args) throws NumberFormatException, IOException {
		int arr[] = { 1, 3, 3, 5, 7 };
		int key = 3;
		System.out.println(upperBound(arr, 0, arr.length, key));
		System.out.println(rowerBound(arr, 0, arr.length, key));
	}
	// front : 처음 index, rear : 마지막 index, key : 기준이 될 key
	static int upperBound(int arr[], int front, int rear, int key) {
		int mid = 0;
		while(front<rear) {
			mid = (front+rear)/2;
			if(arr[mid] <= key) front = mid+1;
			
			// 기존 이진탐색은 mid-1이지만 mid를 포함해야 최종 결가값이 언제나 rear에 위치하게 됩니다.
			else rear = mid;
		}
		return rear;
	}
	static int lwerBound(int arr[], int front, int rear, int key) {
		int mid = 0;
		while(front<rear) {
			mid = (front+rear)/2;
			// 키값보다 작을 때 front를 변경
			if(arr[mid]<key) front = mid + 1;
			else rear = mid;
		}
		
		return rear;
	}
}
```



### 4. 카카오 기출

- https://programmers.co.kr/learn/courses/30/lessons/72412

```java
import java.util.*;

class Solution {
    static HashMap<String, ArrayList<Integer>> map;
    public int[] solution(String[] info, String[] query) {
        int index = 0;
		int[] answer = new int[query.length];
		
		//1. 모든 info에 대해 16가지 경우의 수로 만듭니다.
		map = new HashMap<>();
		for (int i = 0; i < info.length; i++) {
			String[] temp = info[i].split(" ");
			comb(0, temp, "");
		}
		
		//2. 미리 모든 map을 탐색하면서 정렬해줍니다.
		Iterator<String> itr = map.keySet().iterator();
		while(itr.hasNext()) {
			Collections.sort(map.get(itr.next()));
		}
		
		//3. query를 이용해 key값으로 배열을 불론 후 스코어를 이분탐색으로 위치를 찾아냅니다.
		for (int i = 0; i < query.length; i++) {
			
			String[] temp = query[i].split(" ");
			String key= temp[0]+temp[2]+temp[4]+temp[6];
			int score = Integer.parseInt(temp[7]);
			
			if(map.containsKey(key)) {
				ArrayList<Integer> list = map.get(key);
				int result = rowerBound(list, 0, list.size(), score);
				answer[index] = result;
				
			}else {
				answer[index] = 0;
			}
			index++;
		}
		
        return answer;
    }
	static void comb(int index, String[] temp, String str) {
		
		if(index>=4) {

			int score = Integer.parseInt(temp[4]);
			if(map.containsKey(str)) {
				map.get(str).add(score);
			}else {
				map.put(str, new ArrayList<Integer>());
				map.get(str).add(score);
			}
			return;
		}
		
		comb(index+1, temp, str+temp[index]);
		comb(index+1, temp, str+"-");
	}
	static int rowerBound(ArrayList<Integer> list, int front, int rear, int key) {
		int mid = 0;
		
        while(front<rear) {
            mid = (front+rear)/2;
            if(list.get(mid)<key) front = mid +1;
            else rear = mid;
        }

        return list.size()-rear;

	}
}
```

