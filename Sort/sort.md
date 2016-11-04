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

冒泡排序：

```java
public static void bubbleSort(int[] nums) {
  	for(int i = 1; i < nums.length; i++) {
      	for(int j = 0; j < nums.length - 1; j++) {
          	if(nums[i] < nums[j]) {
              	int temp = nums[j];
              	nums[j] = nums[i];
              	nums[i] = temp;
          	}
      	}
  	}
}
```

