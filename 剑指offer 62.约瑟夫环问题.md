### 约瑟夫环问题

#### 题目描述

n个数字排成了圆圈，每次删除第m个数字，看最后剩下哪个数字。

#### 题目分析

当f(n, m)的答案为x，那么假设f(n-1, m)的答案为y则有关系,$$x=(m\%n+y\%n)\%n$$

因此有递归关系

~~~c++
class Solution {
public:
    int lastRemaining(int n, int m) {
        // if(n == 1)return 0;
        // return (m + lastRemaining(n-1, m)) % n;
        int x = 0;
        for(int i=2; i<=n ;i++){
            x = (m+x) % i;
        }

        return x;
    }
};
~~~

注释部分为递归代码。