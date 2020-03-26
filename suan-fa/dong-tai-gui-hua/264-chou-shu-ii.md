# 264 丑数II

```java
class Solution {
    // static List<Integer> list = new ArrayList<>(1700);
    static int[] nums = new int[1690];
    static boolean yes = false;
    // public int nthUglyNumber2(int n) {
    //     if (list.size() == 0) {
    //         for (long a = 1; a <= Integer.MAX_VALUE; a *= 2) {
    //             for (long b = a; b <= Integer.MAX_VALUE; b *= 3) {
    //                 for (long c = b; c <= Integer.MAX_VALUE; c *= 5) {
    //                     list.add((int)c);
    //                 }
    //             }
    //         }
    //         Collections.sort(list);
    //     }
    //     return list.get(n - 1);
    // }

    public int nthUglyNumber(int n) {
        if (yes) {
            return nums[n - 1];
        }
        int i2 = 0;
        int i3 = 0;
        int i5 = 0;
        
        nums[0] = 1;
        for (int i = 1; i < 1690; i++) {
            int next2 = nums[i2] * 2;
            int next3 = nums[i3] * 3;
            int next5 = nums[i5] * 5;
            int next = Math.min(Math.min(next2, next3), next5);
            nums[i] = next;
            if (next == next2 ) i2 ++;
            if (next == next3 ) i3 ++;
            if (next == next5 ) i5 ++;
        }
        yes = true;
        return nums[n-1];
    }
}
```

