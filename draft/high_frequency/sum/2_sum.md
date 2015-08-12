
```java
public int[] twoSum(int[] numbers, int target) {
// naive method O(n^2)
    // if ( numbers.length == 0 || numbers == null ) {
    //     return null;
    // }
    
    // for ( int i = 0 ; i < numbers.length ; i++ ) {
    //     for ( int j = i+1 ; j < numbers.length ; j++ ) {
    //         if ( numbers[i] + numbers[j] == target ) {
    //             return new int[]{i+1, j+1};
    //         }
    //     }
    // }
    
    // return null;

    // HashMap O(n)
    
    HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
    
    // for ( int i = 0 ; i < numbers.length ; i++ ) {
    //     if ( map.containsKey(target-numbers[i]) ) {
    //         return new int[]{map.get(target-numbers[i]), i+1};
    //     } else {
    //         map.put(numbers[i], i+1);
    //     }
    // }
    
    // return null;

    // Two pointer   ** For sorted array
    HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
    for ( int i = 0 ; i < numbers.length ; i++ ) {
        map.put(numbers[i], i+1);
    }
    Arrays.sort(numbers);
    int start = 0;
    int end = numbers.length-1;
    
    while ( start < end ) {
        if ( numbers[start] + numbers[end] == target ) {
            break;
        } else if ( numbers[start] + numbers[end] > target ) {
            end--;
        } else if ( numbers[start] + numbers[end] < target ) {
            start++;
        }
    }
    
    if ( start < end ) {
        int[] ans = new int[]{map.get(numbers[start]), map.get(numbers[end])};
        Arrays.sort(ans);
        return ans;
    } else {
        return null;
    }
}
```