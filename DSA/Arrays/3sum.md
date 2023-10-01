## Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

(Notice that the solution set must not contain duplicate triplets.)

<img width="574" alt="Screenshot 2023-10-01 at 12 52 24 PM" src="https://github.com/HrushiBorhade/Google-Interview-Preparation/assets/89704093/8ddf4b82-7a33-4033-b355-9175c7e09972">

```
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        //Brute Force is to check for all possible Triplets
        //In order to remove duplicate triplates we sort the triplet & store in set.
        Set<List<Integer>> set = new HashSet<>();
        int n = nums.length;

        for(int i =0 ; i<n ; i++){
            for(int j= i+1 ; j<n ; j++){
                for(int k = j+1 ; k<n ; k++){
                    if(nums[i]+nums[j]+nums[k]==0){
                        Integer[] a = new Integer[]{nums[i],nums[j],nums[k]};
                        List<Integer> temp = Arrays.asList(a);
                        Collections.sort(temp);
                        set.add(temp);
                    }

                }
            }
        }
        List<List<Integer>> ans = new ArrayList<>(set);
        return ans;
    }

}

```

```
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        //Better Solution

        // in order to reduce time complexity from O(n^3) -> O(n^2)
        // we use hashset to store the element so nums[k] = 0 - (nums[i]+nums[j])
        // if it is present in our set we sort triplet and add it in our unique triplet set
        Set<List<Integer>> set = new HashSet<>();
        int n = nums.length;
        for(int i=0 ; i<n ; i++){
            HashSet<Integer> s = new HashSet<>();
            for(int j = i+1; j<n ; j++){
                int val = 0 - (nums[i]+nums[j]);
                if(s.contains(val)){
                    Integer[] a = new Integer[]{nums[i],nums[j],val};
                        List<Integer> temp = Arrays.asList(a);
                        Collections.sort(temp);
                        set.add(temp);
                }
                s.add(nums[j]);
            }
        }
         List<List<Integer>> ans = new ArrayList<>(set);
        return ans;
    }
}
```

```
//Optimised Solution
        //Sort the array
        //itterate frm for(i=0 -> n)
        // we use two pointers j = i+1 and k = n-1
        // as array is sorted we have three cases <0 , >0 ==0
        // we perform operations according to the conditionn
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums);
        int n = nums.length;
        for(int i=0 ; i<n ; i++){
            if(i>0 && nums[i]==nums[i-1]) continue;
            int j = i+1;
            int k = n-1;
            while(j<k){
                int sum= nums[i] + nums[j] + nums[k];
                if(sum<0){
                    j++;
                }else if(sum>0){
                    k--;
                }else{
                    Integer[] a = new Integer[]{nums[i],nums[j],nums[k]};
                    List<Integer> temp = Arrays.asList(a);
                    ans.add(temp);
                    j++;
                    k--;
                    while(j<k && nums[j]==nums[j-1]) j++;
                    while(j<k && nums[k]==nums[k+1]) k--;
                }
            }
        }
        return ans;
```
