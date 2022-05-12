#### 题目要求

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

#### 题目分析

要求min,push,pop的时间复杂度都是1,因为是栈结构,push和pop的复杂度本来就是O(1),考虑创建辅助栈,通过同步原始栈记录栈中最小元素实现min的复杂度也是O(1)。

~~~c++
class MinStack {
private:
    stack<int> s1, s2;
public:
    /** initialize your data structure here. */
    MinStack() {
        s2.push(INT_MAX);
    }
    
    void push(int x) {
        s1.push(x);
        s2.push(std::min(s2.top(), x));
    }
    
    void pop() {
        s1.pop();
        s2.pop();
    }
    
    int top() {
        return s1.top();
    }
    
    int min() {
        return s2.top();
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->min();
 */
~~~

