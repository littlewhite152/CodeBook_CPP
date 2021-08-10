## **原题目介绍**

![image-20210809212310983](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210809212310983.png)

## 题目理解 & 解题思路

题目理解：将链表的元素反向存储到一个数组中

解题思路：链表要从头访问元素，可以正向存在一个数组中，然后将数组的元素反向存储

##  自己的解法实现

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        vector<int> v;
        ListNode *i = head;
        while(i){
            v.push_back(i->val);
            i = i->next;
        }
        for(int i = 0; i < v.size() / 2; i ++){
            swap(v[i], v[v.size() - 1 - i]);
        }
        return v;
    }
};
//执行用时：4 ms, 在所有 C++ 提交中击败了86.75%的用户
//内存消耗：8.4 MB, 在所有 C++ 提交中击败了89.07%的用户
```

执行结果：

通过

执行用时：4 ms, 在所有 C++ 提交中击败了86.75%的用户

内存消耗：8.4 MB, 在所有 C++ 提交中击败了89.07%的用户

## 网上比较优秀的解法

#### 解法一:

利用**递归**，先递推至链表末端；回溯时，依次将节点值加入列表，即可实现链表值的倒序输出。

递归解析：

1. 终止条件： 当 head == None 时，代表越过了链表尾节点，则返回空列表；
2. 递推工作： 访问下一节点 head.next ；
3. 回溯阶段：
   - Python： 返回 当前 list + 当前节点值 [head.val] ；
   - Java / C++： 将当前节点值 head.val 加入列表 tmp ；

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> v;
    void fun(ListNode* p){
        if(!p)
            return;
        else{
            fun(p->next);
            v.push_back(p->val);
        }        
    }
    vector<int> reversePrint(ListNode* head) {
        fun(head);
        return v;
    }
};
//执行用时：4 ms, 在所有 C++ 提交中击败了86.75%的用户
//内存消耗：9 MB, 在所有 C++ 提交中击败了12.59%的用户
```



#### 解法二:

**辅助栈法**：链表只能**从前至后**访问每个节点，而题目要求**倒序输出**各节点值，这种**先入后出**的需求可以借助**栈**来实现。

算法流程：

1. 入栈： 遍历链表，将各节点值 push 入栈。
2. 出栈： 将各节点值 pop 出栈，存储于数组并返回。

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        stack<int> stk;
        while(head != nullptr) {
            stk.push(head->val);
            head = head->next;
        }
        vector<int> res;
        while(!stk.empty()) {
            res.push_back(stk.top());
            stk.pop();
        }
        return res;
    }
};
//执行用时：8 ms, 在所有 C++ 提交中击败了34.81%的用户
//内存消耗：8.5 MB, 在所有 C++ 提交中击败了53.56%的用户
```

## 对自己解法的改进



 

## 相关知识总结和思考

相关知识：递归，栈

深入思考：递归的思想可以实现反向输出