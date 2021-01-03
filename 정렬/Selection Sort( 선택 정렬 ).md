# Selection Sort( 선택 정렬 )

- 해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘 입니다.
- 해당 자리를 선택하고 그 자리에 오는 값을 찾는 것입니다. ( 제자리 정렬 )
- 자신을 제외하고 조건에 맞는 index 1개를 찾아 마지막에 교환해주면 됩니다.

- 시간 복잡도 : O(n^2)
- 공간 복잡도 : O(n), 주어진 배열 안에서 교환을 통해 정렬이 수행됩니다.
- 장점
  - Bubble sort와 마찬가지로 알고리즘이 단순합니다.
  - 정렬을 위한 비교 횟수는 많지만 Bubble Sort에 비해 실제로 교환하는 횟수는 적기 때문에 교환이 발생하는 자료상태에서는 비교젹 효율적입니다.
  - Bubble Sort와 마찬가지로 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않습니다. ( 제자리 정렬 )
- 단점
  - 시간복잡도가 O(n^2)으로, 비효율적입니다.
  - **불안정 정렬(Unstable Sort)** 입니다.
    - 정렬 후에 순서 유지를 보장할 수 없습니다.
    - 값이 같은 레코드가 있는 경우 상대적 위치가 변경될 수 있습니다.
    - ex) Array - <B> <b> <a> <c> ( a < b < c )



- 소스코드

```java
class Study {
	public static void main(String[] args) {
		int[] arr = {5, 10, 16, 1, 300, 34, 60};
		
		for (int i = 0; i < arr.length-1; i++) {
			int min = arr[i];
			int index = i;
			for (int j = i+1; j < arr.length; j++) {
				if(arr[index]>arr[j]) {
					index = j;
				}
			}
			int temp = arr[i];
			arr[i] = arr[index];
			arr[index] = temp;
		}
		
		System.out.println(Arrays.toString(arr));

	}
}
```

