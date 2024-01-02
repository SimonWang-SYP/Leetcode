Leetcode 455(Daily-Challenge 2024/01/01)
Probelem name:
Assign Cookies

Author Simon Wang
Email: dodomicc@outlook.com

Problem:
Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie.
Each child i has a greed factor g[i], which is the minimum size of a cookie that the child will be content with; and each cookie j has a size s[j]. If s[j] >= g[i], we can assign the cookie j to the child i, and the child i will be content. Your goal is to maximize the number of your content children and output the maximum number.

Example 1:
Input: g = [1,2,3], s = [1,1]
Output: 1
Explanation: You have 3 children and 2 cookies. The greed factors of 3 children are 1, 2, 3. 
And even though you have 2 cookies, since their size is both 1, you could only make the child whose greed factor is 1 content.
You need to output 1.

Example 2:
Input: g = [1,2], s = [1,2,3]
Output: 2
Explanation: You have 2 children and 3 cookies. The greed factors of 2 children are 1, 2. 
You have 3 cookies and their sizes are big enough to gratify all of the children, 
You need to output 2.
 
Constraints:
1 <= g.length <= 3 * 104
0 <= s.length <= 3 * 104
1 <= g[i], s[j] <= 231 - 1

Solution:
(I)Mathematicial notation 
(I-I)Basic assumption: 
We can assume that the arrays of g and s in problem are both in increasing order as the answer or the process for analysis this problem do nothing with the original order of g or s. 

(I-II)Notation:
In this problem, assume that if k children can be content after giving cookies, then this problem can be set as the mathematical form below. 
(1)  0<=i_1<i_2<...<i_k<g.length 
(2)  0<=j_1,j_2,...,j_k<s.length
(3)  for all 1<=t<=k : s[j_t]>=g[i_t]

(II)Theorem and its proof
theorem: 
assume that there are k children can be content after giving cookies, then we can find suitable i_1,...,i_k, j_1,j_2,...,j_k such that
(4) for all 1<=t<=k : i_t=t-1
(5) 0<=j_1<j_2<...<j_k<s.length
(6) for all 1<=t<=k : s[j_t]>=g[i_t]
proof: 
our goal is to change from the form (1)(2) into (4)(5) and at the same time keep the relation in (6)
step1
By the inequality for all 1<=t<=k:g[t-1]<=g[i_t]<=s[j_t], hence, the i_1<i_2<...<i_k can be changed into 0,1,...,k-1, thus we have finised change from (1) to (4)
step 2;
if u<v and j_u>j_v, we can split the situation into two cases, 
case 1: if s[j_u]=s[j_v], then we can interchange j_u and j_v, after changing, it still satisfy(4),(2) and (3).
case 2: if s[j_u]>s[j_v], then we have that s[j_u]>s[j_v]>=g[v-1] and s[j_v]>=g[v-1]>=g[u-1], hence, in this senerio, we can still interchange j_u and j_v 
now we can change {j_1,j_2,...,j_k} from from (2) into form (5) by keeping several interchange as indicated in case 1 and case 2. 
after the step 1 and step 2, we have changed {i_1,i_2,...,i_k} and {j_1,j_2,...,j_k} into a more standard form (4)(5)(6) from (1)(2)(3)

(III)Designing algorithm by theorem
Apply this theorem into designing our algorithm. in the first step, we can sort the array g and array s because that the order of array g and s has no influence on the final result. now we dive into the second step, in this step, we begin from the minimum number of the g and find the minimum of s to match it, and then we do this for the second minimum of g, the acciracy of this method can be guaranteed by the theorem just proved.

(IV)Code by Java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        int gNum=g.length;
        int sNum=s.length;
        int gIndex=0;
        int sIndex=0;
        int count=0;
        while(gIndex<gNum){
            while(sIndex<sNum && s[sIndex]<g[gIndex]){
                sIndex++;
            }
            if(sIndex<sNum){
                count++;
                sIndex++;
                gIndex++;
            }else{
                break;
            }
        }
        return count;
    }
}
