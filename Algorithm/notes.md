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



#  7. Reverse Integer

## 题目

Given a signed 32-bit integer `x`, return `x` *with its digits reversed*. If reversing `x` causes the value to go outside the signed 32-bit integer range `[-231, 231 - 1]`, then return `0`.

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**

**Example1:**

```
Input: x = 123
Output: 321
```



**Example2:**

```
Input: x = -123
Output: -321
```

## 题目大意

将数字倒过来，**但是假设环境中不能存储 64位的整数**。

## 思路

不能存储64位的整数就意味着不能开`long`、`long long`之类的，所以题目的难点在于怎么处理数字的边界问题，也就是程序中的任何一个变量都不能超过32位整数范围，得先进行预判。

本来想着用

```c++
if(res * 10 + x % 10 < 0 && !sign ||res * 10 + x % 10 > 0 && sign) return 0;
```

这个公式来处理越界的问题，但是`res * 10 + x % 10`这个已经越界了，所以没办法处理，只能考虑将`res`变小，而且不知道`int`的最大值可以用`INT_MAX`表示，最小值用`INT_MIN`表示。

## 代码

```c++
class Solution {
public:
    int reverse(int x) {
        int res = 0;
        while(x){
            int k = x % 10;
            if(res > INT_MAX / 10 || res == INT_MAX / 10 && k > 7) return 0;
            if(res < INT_MIN / 10 || res == INT_MIN / 10 && k < -8) return 0;
            res = res * 10 + k;
            x /= 10;
        }
        return res;
    }
};
```



# 8. String to Integer (atoi)

## 题目

Implement the `myAtoi(string s)` function, which converts a string to a 32-bit signed integer (similar to C/C++'s `atoi` function).

The algorithm for `myAtoi(string s)` is as follows:

1. Read in and ignore any leading whitespace.
2. Check if the next character (if not already at the end of the string) is `'-'` or `'+'`. Read this character in if it is either. This determines if the final  result is negative or positive respectively. Assume the result is  positive if neither is present.
3. Read in next the characters until the next non-digit character or  the end of the input is reached. The rest of the string is ignored.
4. Convert these digits into an integer (i.e. `"123" -> 123`, `"0032" -> 32`). If no digits were read, then the integer is `0`. Change the sign as necessary (from step 2).
5. If the integer is out of the 32-bit signed integer range `[-2^31, 2^31 - 1]`, then clamp the integer so that it remains in the range. Specifically, integers less than `-231` should be clamped to `-2^31`, and integers greater than `2^31 - 1` should be clamped to `2^31 - 1`.
6. Return the integer as the final result.

**Note:**

- Only the space character `' '` is considered a whitespace character.
- **Do not ignore** any characters other than the leading whitespace or the rest of the string after the digits.

 

**Example 1:**

```
Input: s = "42"
Output: 42
Explanation: The underlined characters are what is read in, the caret is the current reader position.
Step 1: "42" (no characters read because there is no leading whitespace)
         ^
Step 2: "42" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "42" ("42" is read in)
           ^
The parsed integer is 42.
Since 42 is in the range [-2^31, 2^31 - 1], the final result is 42.
```

**Example 2:**

```
Input: s = "   -42"
Output: -42
Explanation:
Step 1: "   -42" (leading whitespace is read and ignored)
            ^
Step 2: "   -42" ('-' is read, so the result should be negative)
             ^
Step 3: "   -42" ("42" is read in)
               ^
The parsed integer is -42.
Since -42 is in the range [-2^31, 2^31 - 1], the final result is -42.
```

**Example 3:**

```
Input: s = "4193 with words"
Output: 4193
Explanation:
Step 1: "4193 with words" (no characters read because there is no leading whitespace)
         ^
Step 2: "4193 with words" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "4193 with words" ("4193" is read in; reading stops because the next character is a non-digit)
             ^
The parsed integer is 4193.
Since 4193 is in the range [-2^31, 2^31 - 1], the final result is 4193.
```

## 题目大意

将字符串里的数字转换为32位整数，超出范围的需要截断到边界值。

## 思路

无非就是简单的字符串处理，按照步骤来就好，不过写的有点复杂，时间为77.17%。

```c++
class Solution {
public:
    int myAtoi(string s) {
        bool sign = false, first = true;
        int ans = 0;
        
        for(int i = 0; i < s.size(); i++){
            if(s[i] == ' '){
                if(first) continue;
                else break;
            }else if(s[i] == '+'){
                if(first) first = false;
                else break;
            }else if(s[i] == '-'){
                if(first){
                    sign = true;
                    first = false;
                }else break;
            }else if(isdigit(s[i])){
                if(first) first = false;
                int k = s[i] - '0';
                k = sign ? -k : k;
                if(ans > INT_MAX / 10 || ans == INT_MAX / 10 && k > 7) return INT_MAX;
                if(ans < INT_MIN / 10 || ans == INT_MIN / 10 && k < -8) return INT_MIN;
                ans = ans * 10 + k;
            }else break;
        }
        
        return ans;
        
    }
};
```

## 代码

看了官方的解答，果然速度快了，100%了（后来发现这个速度就是玄学）。

```c++
class Solution {
public:
    int myAtoi(string input) {
        int sign = 1; 
        int result = 0; 
        int index = 0;
        int n = input.size();
        
        // Discard all spaces from the beginning of the input string.
        while (index < n && input[index] == ' ') { 
            index++; 
        }
        
        // sign = +1, if it's positive number, otherwise sign = -1. 
        if (index < n && input[index] == '+') {
            sign = 1;
            index++;
        } else if (index < n && input[index] == '-') {
            sign = -1;
            index++;
        }
        
        // Traverse next digits of input and stop if it is not a digit. 
        // End of string is also non-digit character.
        while (index < n && isdigit(input[index])) {
            int digit = input[index] - '0';

            // Check overflow and underflow conditions. 
            if ((result > INT_MAX / 10) || (result == INT_MAX / 10 && digit > INT_MAX % 10)) { 
                // If integer overflowed return 2^31-1, otherwise if underflowed return -2^31.    
                return sign == 1 ? INT_MAX : INT_MIN;
            }
            
            // Append current digit to the result.
            result = 10 * result + digit;
            index++;
        }
        
        // We have formed a valid number without any overflow/underflow.
        // Return it after multiplying it with its sign.
        return sign * result;
    }
};
```







