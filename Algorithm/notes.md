# 24. Swap Nodes in Pairs

## 题目

Given a linked list, swap every two adjacent nodes and return its head.  You must solve the problem without modifying the values in the list's  nodes (i.e., only nodes themselves may be changed.)

**Example:**

```
Input: head = [1,2,3,4]
Output: [2,1,4,3]
```



## 题目大意

将两两相邻的节点相互交换

## 思路

一开始想的就是建立`pre`和`cur`指针，同时建立一个临时变量`a = cur->next`，使得`cur`指向`a->next`，`a`指向`cur`，`pre`又指向`a`，思路是对的，就是实现得有点复杂，导致时间是53.17%，空间是6.97%，代码如下：

```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* p = head;
        ListNode* pre = head;
        while(p && p->next){
            ListNode* a = p->next;
            p->next = a->next;
            a->next = p;
            if(p == head){
                head = a;
            }else{
                pre->next = a;
            }
            pre = p;
            p = p->next;
        }
        return head;
    }
};
```

## 代码

后来有幸看到几个大佬的做法，修改了一下。

代码一：

```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if(!head || !head->next) return head;
        ListNode* res = new ListNode();
        ListNode* pre = res;
        ListNode* cur = head;
        while(cur && cur->next){
            pre->next = cur->next;
            cur->next = pre->next->next;
            pre->next->next = cur;
            pre = cur;
            cur = cur->next;
        }
        return res->next;
    }
};
```

代码二：这是一种递归的做法，代码非常简洁，用时跟上面的差不多。

```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if(!head || !head->next) return head;
        ListNode* tmp = head->next;
        head->next = swapPairs(tmp->next);
        tmp->next = head;
        return tmp;
    }
};
```



