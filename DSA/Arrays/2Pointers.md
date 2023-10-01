# Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.
Note that you must do this in-place without making a copy of the array.

Example 1:

Input: nums = [0,1,0,3,12]

Output: [1,3,12,0,0]

```
class Solution {
    public void moveZeroes(int[] nums) {

        //Brute Force Solution
        // using extra arraylist to store all non zero elements
        // fill all non zero elements at front
        // add zeros to remaining positions

        //Optimised
        //using 2Pointers
        int i=0; 
        int n = nums.length;
        if(n<=1) return;
        while(i<n && nums[i]!=0) i++;
        int j = i+1;
        while(j<n){
            if(nums[j]!=0){
                nums[i] = nums[j];
                nums[j] = 0;
                i++;
            }
            j++;
        }
    }
}
```
