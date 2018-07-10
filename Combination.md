> **Source:** [Combination_GeeksForGeeks](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)
## __With Repetition__ 

> Elements will be considered different even it their values are same.
> Eg: {1, 2, 3, 1, 1} here each ```1``` will be considered different entity even if there values are same.

```java
class Main{
    
    static void combination(int arr[], int data[], int start, int end, int index, int r) {
        if (index == r)
        {
            System.out.println();
            for (int j=0; j<r; j++)
                System.out.print(data[j]+" ");
            return;
        }
        for (int i=start; i<=end && end-i+1 >= r-index; i++) {
            data[index] = arr[i];
            combination(arr, data, i+1, end, index+1, r);
        }
    }
    static void print(int arr[], int n, int r){
        int data[]=new int[r];
        combination(arr, data, 0, n-1, 0, r);
    }
    
    public static void main (String[] args) {
        int arr[] = {1, 2, 3, 1, 1};
        int r = 3;
        int n = arr.length;
        print(arr, n, r);
    }
}
```
> **Output:**
```
1 2 3 
1 2 1 
1 2 1 
1 3 1 
1 3 1 
1 1 1 
2 3 1 
2 3 1 
2 1 1 
3 1 1 
```
## __Without Repetition__ 

> Elements will be considered same even it their values are same.
> Eg: {1, 2, 3, 1, 1} here each ```1``` will be considered same entity even if there values are same.

```java

```

