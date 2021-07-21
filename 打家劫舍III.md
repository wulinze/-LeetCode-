### 题目描述

打家劫舍是一个系列题，都是用DP做的前两个比较简单，主要说一下第三个。

在上次打劫完一条街道之后和一圈房屋后，小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为“根”。 除了“根”之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果两个直接相连的房子在同一天晚上被打劫，房屋将自动报警。

计算在不触动警报的情况下，小偷一晚能够盗取的最高金额。

**示例1：**

~~~
输入: [3,2,3,null,3,null,1]

     3
    / \
   2   3
    \   \ 
     3   1

输出: 7 
解释: 小偷一晚能够盗取的最高金额 = 3 + 3 + 1 = 7.
~~~

**示例2：**

~~~
输入: [3,4,5,1,3,null,1]

     3
    / \
   4   5
  / \   \ 
 1   3   1

输出: 9
解释: 小偷一晚能够盗取的最高金额 = 4 + 5 = 9.
~~~

### 题目分析

有了前面两个题的经验，可以很容易知道这是一个DP的问题。那么问题就在于如何书写状态转移方程。首先因为生产状态转移方程需要知道之前的状态，因此选择通过叶子节点向上转移。

转移方程如下
$$
f[node] = node->val+g[node->left]+g[node->right]
$$

$$
g[node]=max(f[node->left],g[node->left])+max(f[node->right],g[node->right])
$$



~~~c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    unordered_map<TreeNode*, int> f1, f2;
    void dfs(TreeNode* root){
        if(!root)return;
        dfs(root->left);
        dfs(root->right);
        f1[root] = root->val + f2[root->left] + f2[root->right];
        f2[root] = max(f1[root->left], f2[root->left]) + max(f1[root->right], f2[root->right]);
    }
    int rob(TreeNode* root) {
        dfs(root);
        return max(f1[root], f2[root]);
    }
};
~~~

