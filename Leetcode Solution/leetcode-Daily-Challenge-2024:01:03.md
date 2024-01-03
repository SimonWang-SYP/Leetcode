Leetcode 2125(Daily-Challenge 2024/01/03) 
Number of Laser Beams in a Bank

Author Simon Wang
Email: dodomicc@outlook.com

Problem:
Anti-theft security devices are activated inside a bank. You are given a 0-indexed binary string array bank representing the floor plan of the bank, which is an m x n 2D matrix. bank[i] represents the ith row, consisting of '0's and '1's. '0' means the cell is empty, while'1' means the cell has a security device.
There is one laser beam between any two security devices if both conditions are met:
The two devices are located on two different rows: r1 and r2, where r1 < r2.
For each row i where r1 < i < r2, there are no security devices in the ith row.
Laser beams are independent, i.e., one beam does not interfere nor join with another.
Return the total number of laser beams in the bank.

Example 1:
Input: bank = ["011001","000000","010100","001000"]
Output: 8
Explanation: Between each of the following device pairs, there is one beam. In total, there are 8 beams:
 * bank[0][1] -- bank[2][1]
 * bank[0][1] -- bank[2][3]
 * bank[0][2] -- bank[2][1]
 * bank[0][2] -- bank[2][3]
 * bank[0][5] -- bank[2][1]
 * bank[0][5] -- bank[2][3]
 * bank[2][1] -- bank[3][2]
 * bank[2][3] -- bank[3][2]
Note that there is no beam between any device on the 0th row with any on the 3rd row.
This is because the 2nd row contains security devices, which breaks the second condition.

Example 2:
Input: bank = ["000","111","000"]
Output: 0
Explanation: There does not exist two devices located on two different rows.
 

Constraints:
m == bank.length
n == bank[i].length
1 <= m, n <= 500
bank[i][j] is either '0' or '1'.

Solution:
(I)Analysis:
This problem is very trival，it can be seen that if there is an laser beams, then there are at least two rows have security divice, hence, an algorithm has been designed as below: 

(II)Algorithm design
By maintaining an array called device number to count the number of devices on each row, then, it can be assumed that i_1, 
i_2,...,i_k is not zero, the number of laser beams in a bank is that i_1*i_2+
...+i_(k-1)*i_k.

(III)Code by Java
class Solution {
    public int numberOfBeams(String[] bank) {
        int m=bank.length;
        int n=bank[0].length();
        int[] deviceNum=new int[m];
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                if(bank[i].charAt(j)=='1') deviceNum[i]++;
            }
        }
        int oldNum=0,newNum=0;
        int i=0;
        while(i<m && deviceNum[i]==0){
            i++;
        }
        int result=0;
        if(i<m){
            oldNum=deviceNum[i];
            for(int j=i+1; j<m; j++){
                if(deviceNum[j]!=0){
                    newNum=deviceNum[j];
                    result+=oldNum*newNum;
                    oldNum=newNum;
                }
            }
        }
        return result;
    }
}

