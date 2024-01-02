Leetcode 2610(Daily-Challenge 2024/01/02) 
Probelem name:Convert an Array Into a 2D Array With Conditions

Author Simon Wang
Email: dodomicc@outlook.com

Problem:
You are given an integer array nums. You need to create a 2D array from nums satisfying the following conditions:
The 2D array should contain only the elements of the array nums.
Each row in the 2D array contains distinct integers.
The number of rows in the 2D array should be minimal.
Return the resulting array. If there are multiple answers, return any of them.
Note that the 2D array can have a different number of elements on each row.

Example 1:
Input: nums = [1,3,4,1,2,3,1]
Output: [[1,3,4,2],[1,3],[1]]
Explanation: We can create a 2D array that contains the following rows:
- 1,3,4,2
- 1,3
- 1
All elements of nums were used, and each row of the 2D array contains distinct integers, so it is a valid answer.
It can be shown that we cannot have less than 3 rows in a valid array.

Example 2:
Input: nums = [1,2,3,4]
Output: [[4,3,2,1]]
Explanation: All elements of the array are distinct, so we can keep all of them in the first row of the 2D array.
 
Constraints:
1 <= nums.length <= 200
1 <= nums[i] <= nums.length

Solution:
(I)Analysis:
In this problem, it can be found that as we need to sperate this array num into several sub lists, and the number of each sub lists should be different from each other, hence, it can be concluded that the number of sublists should equal to the maximum repeated number of an element in array nums. hence, we can desgin our aggorithm as below

(II)Algorithm design
for each number in array nums, assume that this is the i^th time that it appears in the array nums, and check the size of the sublists of the lists , if we the size of the sublists >=i, then we add it to the i^th sublist of our result directily, otherwise, just add a new sublist to the result first, then add this number to this sublist. 

(III)Code by Java
class Solution {
    public List<List<Integer>> findMatrix(int[] nums) {
        int[] freq=new int[200];
        int n=nums.length;
        List<List<Integer>> result=new ArrayList<>();
        int size=1;
        result.add(new ArrayList<>());
        freq[nums[0]-1]++;
        result.get(0).add(nums[0]);
         for(int i=1; i<n; i++){
            freq[nums[i]-1]++;
            if(size<freq[nums[i]-1]){
                size++;
                result.add(new ArrayList<>());
            }
            result.get(freq[nums[i]-1]-1).add(nums[i]);
        }
        return result;
    }
}

