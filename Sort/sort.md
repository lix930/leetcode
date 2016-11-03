选择排序：

```java
public static void insertSort(int[] nums) {
		int temp;
		int i, j;
		for(i = 1; i < nums.length; i++){
			temp = nums[i];
			j = i - 1;
			while(j >= 0 && temp < nums[j]){
				nums[j + 1] = nums[j];
				j--;
			}
			nums[j + 1] = temp;
		}	
	}
```

