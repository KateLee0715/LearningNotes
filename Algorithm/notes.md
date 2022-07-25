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

# 29. Divide Two Integers

## 题目

Given two integers `dividend` and `divisor`, divide two integers **without** using multiplication, division, and mod operator.

The integer division should truncate toward zero, which means losing its fractional part. For example, `8.345` would be truncated to `8`, and `-2.7335` would be truncated to `-2`.

Return *the **quotient** after dividing* `dividend` *by* `divisor`.

**Note:** Assume we are dealing with an environment that could only store integers within the **32-bit** signed integer range: `[−2^31, 2^31 − 1]`. For this problem, if the quotient is **strictly greater than** `2^31 - 1`, then return `2^31 - 1`, and if the quotient is **strictly less than** `-2^31`, then return `-2^31`.

 

**Example 1:**

```
Input: dividend = 10, divisor = 3
Output: 3
Explanation: 10/3 = 3.33333.. which is truncated to 3.
```

**Example 2:**

```
Input: dividend = 7, divisor = -3
Output: -2
Explanation: 7/-3 = -2.33333.. which is truncated to -2.
```

## 题目大意

被除数除以除数，求商，但不能进行除法、乘法和求余运算，得到的结果取整数部分，而且整个环境只能存储32位有符号整数。

## 思路

一开始想着用减法，但是如果被除数太大，除数太小，就会TLE，所以我们要把除数变大，再用减法，把除数变大的方法就是用位左移，使得除数最接近被除数。

## 代码

```c++
class Solution {
public:
    int divide(int dividend, int divisor) {
        if(dividend == 0) return 0;
        
        if(divisor == INT_MIN) return dividend == INT_MIN ? 1 : 0;
        
        int neg = (dividend > 0) ^ (divisor > 0);
        
        // Here is different from the description above.
		// In practice, we force our dividend to be negative.
		// Because the range of negative values (2^31) is larger than the range of positive values (2^31 - 1).
		// If we force dividend to be positive, there may be integer overflow.
        if(dividend > 0) dividend = 0 - dividend;
        
		// Divisor should be positive.
		// Because we will apply bitwise shift to it.
		// And we have handled the case when divisor is INT_MIN.
        if(divisor < 0) divisor = 0 - divisor;
        
        int ans = 0;
        
        while(dividend <= -divisor){
            int tmp = divisor, step = 1;
            
            while(tmp < 1<<30 && -tmp >= dividend){
                tmp <<= 1;
                step <<= 1;
            }
            
            if(-tmp < dividend){
                tmp >>= 1;
                step >>= 1;
            }
            
            dividend += tmp;
            ans -= step;
        }
        
        if(neg) return ans;
        else return ans == INT_MIN ? INT_MAX : -ans;
    }
};
```

# 36. Valid Sudoku

## 题目

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note:**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

 

**Example 1:**

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

```
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

**Example 2:**

```
Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

## 题目大意

根据数独的规则判断一个数独是否成立。

## 思路

按照规则写判断函数建立几个数组去存储，避免重复判断。

## 代码

```c++
class Solution {
public:
    bool block[3][3] = {false};
    bool row[9] = {false};
    bool col[9] = {false};
    
    bool validBlock(vector<vector<char>>& board, int r, int c){
        int rr = r / 3, cc = c / 3;
        int cnt[10] = {0};
        for(int i = rr * 3; i < (rr + 1) * 3; i++){
            for(int j = cc * 3; j < (cc + 1) * 3; j++){
                if(board[i][j] == '.') continue;
                if(cnt[board[i][j] - '0']) return false;
                cnt[board[i][j] - '0']++;
            }
        }
        return true;
    }
    
    bool validRow(vector<vector<char>>& board, int r){
        int cnt[10] = {0};
        for(int i = 0; i < 9; i++){
            if(board[r][i] == '.') continue;
            if(cnt[board[r][i] - '0']) return false;
            cnt[board[r][i] - '0']++;
        }
        return true;
    }
    
    bool validCol(vector<vector<char>>& board, int c){
        int cnt[10] = {0};
        for(int i = 0; i < 9; i++){
            if(board[i][c] == '.') continue;
            if(cnt[board[i][c] - '0']) return false;
            cnt[board[i][c] - '0']++;
        }
        return true;
    }
    
    bool isValidSudoku(vector<vector<char>>& board) {
        for(int r = 0; r < 9; r++){
            for(int c = 0; c < 9; c++){
                if(board[r][c] == '.') continue;
                if(!block[r/3][c/3]){
                    bool flag = validBlock(board, r, c);
                    if(!flag) return false;
                    block[r/3][c/3] = true;
                }
                if(!row[r]){
                    bool flag = validRow(board, r);
                    if(!flag) return false;
                    row[r] = true;
                }
                if(!col[c]){
                    bool flag = validCol(board, c);
                    if(!flag) return false;
                    col[c] = true;
                }
            }
        }
        return true;
    }
};
```

# 38. Count and Say

## 题目

The **count-and-say** sequence is a sequence of digit strings defined by the recursive formula:

- `countAndSay(1) = "1"`
- `countAndSay(n)` is the way you would "say" the digit string from `countAndSay(n-1)`, which is then converted into a different digit string.

To determine how you "say" a digit string, split it into the **minimal** number of groups so that each group is a contiguous section all of the **same character.** Then for each group, say the number of characters, then say the  character. To convert the saying into a digit string, replace the counts with a number and concatenate every saying.

For example, the saying and conversion for digit string `"3322251"`:

![img](https://assets.leetcode.com/uploads/2020/10/23/countandsay.jpg)

Given a positive integer `n`, return *the* `nth` *term of the **count-and-say** sequence*.

 

**Example 1:**

```
Input: n = 1
Output: "1"
Explanation: This is the base case.
```

**Example 2:**

```
Input: n = 4
Output: "1211"
Explanation:
countAndSay(1) = "1"
countAndSay(2) = say "1" = one 1 = "11"
countAndSay(3) = say "11" = two 1's = "21"
countAndSay(4) = say "21" = one 2 + one 1 = "12" + "11" = "1211"
```

## 题目大意

像一种递归的形式，将n-1对应的字符串说出来。

## 思路

写一个递归，出口条件是当`n = 1`时，返回`"1"`；获取`n - 1`时的字符串，然后循环遍历将其说出来。

## 代码

```c++
class Solution {
public:
    string countAndSay(int n) {
        if(n == 1) return "1";
        string pre = countAndSay(n - 1);
        
        int cnt = 1, x = pre[0] - '0';
        string ans = "";
        
        for(int i = 1; i < pre.size(); i++){
            if(pre[i] != pre[i-1]){
                ans += cnt + '0';
                ans += x + '0';
                cnt = 1;
                x = pre[i] - '0';
            }else{
                cnt++;
            }
        }
        
        ans += cnt + '0';
        ans += x + '0';
        
        return ans;
    }
};
```

# 50. Pow(x, n)

## 题目

Implement [pow(x, n)](http://www.cplusplus.com/reference/valarray/pow/), which calculates `x` raised to the power `n` (i.e., `x^n`).

 

**Example 1:**

```
Input: x = 2.00000, n = 10
Output: 1024.00000
```

**Example 2:**

```
Input: x = 2.10000, n = 3
Output: 9.26100
```

**Example 3:**

```
Input: x = 2.00000, n = -2
Output: 0.25000
Explanation: 2^(-2) = 1/2^2 = 1/4 = 0.25
```

## 题目大意

求`x`的`n`次幂

## 思路

这个要是直接乘会TLE，所以我们用到了快速幂的方法（直接套模板），注意处理边界问题。

## 代码

```c++
class Solution {
public:
    double myPow(double x, int n) {
        double res = 1.0;
        bool neg = false;
        if(n == INT_MIN){
            x *= x;
            n = 1 << 30;
            neg = true;
        }else if(n < 0){
            n = 0 - n;
            neg = true;
        }
        while(n){
            if(n & 1){
                res *= x;
            }
            x *= x;
            n >>= 1;
        }
        return neg ? 1.0 / res : res;
    }
};
```

# 503. Next Greater Element II

## 题目

Given a circular integer array `nums` (i.e., the next element of `nums[nums.length - 1]` is `nums[0]`), return *the **next greater number** for every element in* `nums`.

The **next greater number** of a number `x`  is the first greater number to its traversing-order next in the array,  which means you could search circularly to find its next greater number. If it doesn't exist, return `-1` for this number.

 

**Example 1:**

```
Input: nums = [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number. 
The second 1's next greater number needs to search circularly, which is also 2.
```

**Example 2:**

```
Input: nums = [1,2,3,4,3]
Output: [2,3,4,-1,4]
```

## 题目大意

求每个元素下一个比它更大的元素。

## 思路

一开始想着用队列和栈实现，顺序遍历，队列顺序存着从小到大的数，栈顺序存着从大到小的数：

```c++
class Solution {
public:
    int ans[10005];
    int q[10005];
    int stk[10005];
    int hh = 0, tt = -1, top = -1;
    vector<int> nextGreaterElements(vector<int>& nums) {
        vector<int> res;
        q[++tt] = 0;
        stk[++top] = 0;
        for(int i = 1; i < nums.size(); i++){
            while(top != -1 && nums[i] > nums[stk[top]]){
                int k = stk[top--];
                ans[k] = i;
            }
            stk[++top] = i;
            if(nums[i] > nums[q[tt]]){
                q[++tt] = i;
            }
        }
        
        while(top != -1){
            int k = stk[top--];
            while(hh <= tt && nums[q[hh]] <= nums[k]) hh++;
            if(hh > tt){
                ans[k] = -1;
            }else{
                ans[k] = q[hh];
            }
        }
        
        for(int i = 0; i < nums.size(); i++){
            if(ans[i] != -1){
                res.push_back(nums[ans[i]]);
            }else{
                res.push_back(-1);
            }
        }
        
        return res;
    }
};
```

结果还不错，不过有些复杂

## 代码

看了官方解答，代码简洁了不少

```c++
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        stack<int> s;
        int n = nums.size();
        vector<int> res(n, -1);
        
        for(int i = 2 * n - 1; i >= 0; i--){
            while(!s.empty() && nums[i%n] >= s.top()) s.pop();
            if(i < n && !s.empty() && nums[i] < s.top()) res[i] = s.top();
            s.push(nums[i%n]);
        }
        
        return res;
    }
};
```

# 54. Spiral Matrix

## 题目

Given an `m x n` `matrix`, return *all elements of the* `matrix` *in spiral order*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg)

```
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

## 题目大意

将矩阵中的元素按蛇形顺序打印出来

## 思路

一开始想着一圈一圈由外向里地打印，可能判断条件写得不够好，导致用时长：

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        vector<int> res;
        int cnt = 0;
        
        do{
            for(int i = cnt; i < n + cnt; i++){
                res.push_back(matrix[cnt][i]);
            }
            
            for(int i = cnt + 1; i < m + cnt; i++){
                res.push_back(matrix[i][n+cnt-1]);
            }
            
            for(int i = cnt + n - 2; m >= 2 && i >= cnt; i--){
                res.push_back(matrix[m+cnt-1][i]);
            }
            
            for(int i = m + cnt - 2; n >= 2 && i >= cnt + 1; i--){
                res.push_back(matrix[i][cnt]);
            }
            
            m -= 2;
            n -= 2;
            cnt++;
        }while(m > 0 && n > 0);
        
        return res;
    }
};
```

## 代码

看了一个大佬的代码，感觉比我写的清晰多了，通俗易懂多了，有条理多了，复刻如下：

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        int st_row = 0, ed_row = m - 1, st_col = 0, ed_col = n - 1;
        int cnt = 0, tol = m * n;
        vector<int> res;
        
        while(cnt < tol){
            for(int i = st_col; cnt < tol && i <= ed_col; i++){
                res.push_back(matrix[st_row][i]);
                cnt++;
            }
            st_row++;
            
            for(int i = st_row; cnt < tol && i <= ed_row; i++){
                res.push_back(matrix[i][ed_col]);
                cnt++;
            }
            ed_col--;
            
            for(int i = ed_col; cnt < tol && i >= st_col; i--){
                res.push_back(matrix[ed_row][i]);
                cnt++;
            }
            ed_row--;
            
            for(int i = ed_row; cnt < tol && i >= st_row; i--){
                res.push_back(matrix[i][st_col]);
                cnt++;
            }
            st_col++;
        }
        
        return res;
    }
};
```

# 73. Set Matrix Zeroes

## 题目

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.

You must do it [in place](https://en.wikipedia.org/wiki/In-place_algorithm).

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

```
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg)

```
Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
```

## 题目大意

一个位置有0，那么这个0所在的行和列全部置为0

## 思路

一开始想的是遍历，到0了就把行列变为0，并标记一下该行/该列已经变为0，同时为了区分原先是0还是后面变为0做了标记，但是时间和空间不理想。后来看了某位大佬的做法，是遍历的时候先不置为0，看到0就把0的坐标放入vector中，最后再遍历一次把他们所在的行和列置为0。

```c++
class Solution {
public:
    bool flag[205][205];
    bool row[205];
    bool col[205];
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(matrix[i][j]) continue;
                if(flag[i][j]) continue;
                if(!row[i]){
                    for(int k = 0; k < n; k++){
                        if(!matrix[i][k]) continue;
                        matrix[i][k] = 0;
                        flag[i][k] = true;
                    }
                    row[i] = true;
                }
                if(!col[j]){
                    for(int k = 0; k < m; k++){
                        if(!matrix[k][j]) continue;
                        matrix[k][j] = 0;
                        flag[k][j] = true;
                    }
                    col[j] = true;
                }
            }
        }
    }
};
```

## 代码

```c++
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        vector<pair<int, int>> v;
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(!matrix[i][j]) v.push_back(make_pair(i, j));
            }
        }
        
        for(int k = 0; k < v.size(); k++){
            int c = 0, r = 0;
            while(c < n){
                matrix[v[k].first][c] = 0;
                c++;
            }
            
            while(r < m){
                matrix[r][v[k].second] = 0;
                r++;
            }
        }
    }
};
```

# 116. Populating Next Right Pointers in Each Node

## 题目

You are given a **perfect binary tree** where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2019/02/14/116_sample.png)

```
Input: root = [1,2,3,4,5,6,7]
Output: [1,#,2,3,#,4,5,6,7,#]
Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```

**Example 2:**

```
Input: root = []
Output: []
```

## 题目大意

用`next`指针指向节点右边第一个节点，如果没有指向`null`

## 思路

用bfs遍历每一层，如果那一层还有剩节点那就指向队头的节点，如果没有就指向null

## 代码

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

class Solution {
public:
    Node* connect(Node* root) {
        if(root == nullptr) return nullptr;
        queue<Node*> q;
        q.push(root);
        while(q.size()){
            int cnt = q.size();
            while(cnt){
                Node* tmp = q.front();
                q.pop();
                cnt--;
                if(cnt){
                    tmp->next = q.front();
                }
                if(tmp->left) q.push(tmp->left);
                if(tmp->right) q.push(tmp->right);
            }
            
        }
        return root;
    }
};
```

# 122. Best Time to Buy and Sell Stock II

## 题目

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

On each day, you may decide to buy and/or sell the stock. You can only hold **at most one** share of the stock at any time. However, you can buy it then immediately sell it on the **same day**.

Find and return *the **maximum** profit you can achieve*.

 

**Example 1:**

```
Input: prices = [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.
```

**Example 2:**

```
Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Total profit is 4.
```

**Example 3:**

```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: There is no way to make a positive profit, so we never buy the stock to achieve the maximum profit of 0.
```

## 题目大意

买卖股票，每天最多只能持有一股，每天都能买卖无数次，求能赚到利润的最大值

## 思路

其实就是一个贪心问题，只要股票明天升，那就今天买明天卖

## 代码

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int ans = 0;
        for(int i = 0; i < prices.size() - 1; i++){
            if(prices[i+1] > prices[i]) ans += prices[i+1] - prices[i];
        }
        return ans;
    }
};
```

# 131. Palindrome Partitioning

## 题目

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

 

**Example 1:**

```
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
```

**Example 2:**

```
Input: s = "a"
Output: [["a"]]
```

## 题目大意

给定一个字符串，将其分割成每个字符串都是回文的所有组合

## 思路

判断回文用动态规划，中间那段字符串是回文且两端字母相同就是回文，否则不是；列举所有组合用深搜。

## 代码

```c++
class Solution {
public:
    bool pal[20][20];
    void init(string s){
        int n = s.size();
        for(int i = 0; i < n; i++){
            pal[i][i] = true;
            pal[i][i+1] = true;
        }
        for(int len = 2; len <= n; len++){
            for(int i = 0; i <= n - len; i++){
                if(pal[i+1][i+len-1] && s[i] == s[i+len-1]) pal[i][i+len] = true;
                else pal[i][i+len] = false;
            }
        }
    }
    void dfs(vector<vector<string>>& res, int st, string s, vector<string>& cur){
        if(st == s.size()){
            res.push_back(cur);
            return;
        }
        for(int ed = st+1; ed <= s.size(); ed++){
            if(pal[st][ed]){
                cur.push_back(s.substr(st, ed-st));
                dfs(res, ed, s, cur);
                cur.pop_back();
            }
        }
    }
    vector<vector<string>> partition(string s) {
        init(s);
        vector<vector<string>> res;
        vector<string> cur;
        dfs(res, 0, s, cur);
        return res;
    }
};
```

# 134. Gas Station

## 题目

There are `n` gas stations along a circular route, where the amount of gas at the `ith` station is `gas[i]`.

You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from the `ith` station to its next `(i + 1)th` station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays `gas` and `cost`, return *the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return* `-1`. If there exists a solution, it is **guaranteed** to be **unique**

 

**Example 1:**

```
Input: gas = [1,2,3,4,5], cost = [3,4,5,1,2]
Output: 3
Explanation:
Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 4. Your tank = 4 - 1 + 5 = 8
Travel to station 0. Your tank = 8 - 2 + 1 = 7
Travel to station 1. Your tank = 7 - 3 + 2 = 6
Travel to station 2. Your tank = 6 - 4 + 3 = 5
Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.
Therefore, return 3 as the starting index.
```

**Example 2:**

```
Input: gas = [2,3,4], cost = [3,4,3]
Output: -1
Explanation:
You can't start at station 0 or 1, as there is not enough gas to travel to the next station.
Let's start at station 2 and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 0. Your tank = 4 - 3 + 2 = 3
Travel to station 1. Your tank = 3 - 3 + 3 = 3
You cannot travel back to station 2, as it requires 4 unit of gas but you only have 3.
Therefore, you can't travel around the circuit once no matter where you start.
```

## 题目大意

从哪个点出发才能送气送一圈，到下一个点会消耗气，到达后可充气

## 思路

用双指针，如果当前拥有的气为负数，则要从下一个点重新开始；绕一圈都为正数则为答案。

## 代码

```c++
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int n = gas.size();
        int i = 0, j = i, ans = 0;
        while(i < n && j < 2 * n && j - i < n){
            while(i < n && gas[i] - cost[i] < 0) i++;
            if(i < n){
                j = i;
                while(j < 2 * n && j - i < n){
                    ans += gas[j%n] - cost[j%n];
                    if(ans < 0){
                        i = j + 1;
                        ans = 0;
                        break;
                    }else j++;
                }
                if(j - i == n) return i;
            }
        }
        return -1;
    }
};
```

# 150. Evaluate Reverse Polish Notation

## 题目

Evaluate the value of an arithmetic expression in [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Valid operators are `+`, `-`, `*`, and `/`. Each operand may be an integer or another expression.

**Note** that division between two integers should truncate toward zero.

It is guaranteed that the given RPN expression is always valid. That  means the expression would always evaluate to a result, and there will  not be any division by zero operation.

 

**Example 1:**

```
Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```

**Example 2:**

```
Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```

**Example 3:**

```
Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

## 题目大意

计算一个后缀表达式的值

## 思路

用栈的方式，建立一个数字栈，一遍历到运算符，就把栈顶的两个数字拿出来运算，再压入栈中，最后输出栈顶的结果。

## 代码

```c++
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        int n = tokens.size();
        stack<int> s;
        for(int i = 0; i < n; i++){
            if(tokens[i] == "+" || tokens[i] == "-" || tokens[i] == "*" || tokens[i] == "/"){
                char op = tokens[i][0];
                int num2 = s.top();
                s.pop();
                int num1 = s.top();
                s.pop();
                if(op == '+'){
                    s.push(num1 + num2);
                }else if(op == '-'){
                    s.push(num1 - num2);
                }else if(op == '*'){
                    s.push(num1 * num2);
                }else{
                    s.push(num1 / num2);
                }
            }else{
                int x = stoi(tokens[i]);
                s.push(x);
            }
        }
        
        return s.top();
    }
};
```

# 162. Find Peak Element

## 题目

A peak element is an element that is strictly greater than its neighbors.

Given an integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You may imagine that `nums[-1] = nums[n] = -∞`.

You must write an algorithm that runs in `O(log n)` time.

 

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

**Example 2:**

```
Input: nums = [1,2,1,3,5,6,4]
Output: 5
Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.
```

## 题目大意

寻找局部最大值，并返回它的索引

## 思路

利用二分查找法，如果mid右边的比mid大，那就在右边找，否则就在左边找

## 代码

```c++
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int n = nums.size();
        int l = 0, r = n - 1;
        while(l < r){
            int mid = (l + r) / 2;
            if(nums[mid+1] > nums[mid]) l = mid + 1;
            else r = mid;
        }
        return l;
    }
};
```

# 166. Fraction to Recurring Decimal

## 题目

Given two integers representing the `numerator` and `denominator` of a fraction, return *the fraction in string format*.

If the fractional part is repeating, enclose the repeating part in parentheses.

If multiple answers are possible, return **any of them**.

It is **guaranteed** that the length of the answer string is less than `104` for all the given inputs.

 

**Example 1:**

```
Input: numerator = 1, denominator = 2
Output: "0.5"
```

**Example 2:**

```
Input: numerator = 2, denominator = 1
Output: "2"
```

**Example 3:**

```
Input: numerator = 4, denominator = 333
Output: "0.(012)"
```

## 题目大意

给定除数和被除数，求出商并用字符串表示，如果小数部分有循环的话就要用括号括起来。

## 思路

能够除得尽都很好处理，当有循环的时候，会出现余数相同的时候，这时候就在余数相同的位置插上括号。

## 代码

```c++
class Solution {
public:
    unordered_map<long, int> mp;
    string fractionToDecimal(int numerator, int denominator) {
        if(!numerator) return "0";
        string ans = "";
        if(numerator < 0 ^ denominator < 0) ans += "-";
        long num = labs(numerator);
        long den = labs(denominator);
        long f = num / den;
        long mod = num % den;
        ans += to_string(f);
        if(!mod) return ans;
        
        ans += ".";
        while(mod){
            if(mp.count(mod)){
                int idx = mp[mod];
                ans.insert(idx, "(");
                ans += ")";
                break;
            }else{
                mp[mod] = ans.size();
                mod *= 10;
                f = mod / den;
                mod %= den;
                ans += to_string(f);
            }
        }
        return ans;
    }
};
```

# 172. Factorial Trailing Zeroes

## 题目

Given an integer `n`, return *the number of trailing zeroes in* `n!`.

Note that `n! = n * (n - 1) * (n - 2) * ... * 3 * 2 * 1`.

 

**Example 1:**

```
Input: n = 3
Output: 0
Explanation: 3! = 6, no trailing zero.
```

**Example 2:**

```
Input: n = 5
Output: 1
Explanation: 5! = 120, one trailing zero.
```

**Example 3:**

```
Input: n = 0
Output: 0
```

## 题目大意

统计n的阶乘末尾有多少个0

## 思路

只有2和5相乘才会在末尾产生0，所以只需要统计2和5的数量，取最小值就是最终的答案。

## 代码

```c++
class Solution {
public:
    int trailingZeroes(int n) {
        int cnt2 = 0, cnt5 = 0;
        int div2 = 2, div5 = 5;
        while(div2 <= n){
            cnt2 += n / div2;
            div2 *= 2;
        }
        while(div5 <= n){
            cnt5 += n / div5;
            div5 *= 5;
        }
        int ans = min(cnt5, cnt2);
        return ans;
    }
};
```

# 179. Largest Number

## 题目

Given a list of non-negative integers `nums`, arrange them such that they form the largest number and return it.

Since the result may be very large, so you need to return a string instead of an integer.

 

**Example 1:**

```
Input: nums = [10,2]
Output: "210"
```

**Example 2:**

```
Input: nums = [3,30,34,5,9]
Output: "9534330"
```

## 题目大意

给定一些数，将它们拼接成最大的一个数

## 思路

定义一个排序函数，当a和b拼接起来比b和a拼接起来大时，a排在b的前面。

## 代码

```c++
class Solution {
public:
    static bool cmp(string a, string b){
        return a + b > b + a;
    }
    
    string largestNumber(vector<int>& nums) {
        vector<string> str;
        string ans = "";
        int n = nums.size();
        for(int i = 0; i < n; i++){
            str.push_back(to_string(nums[i]));
        }
        sort(str.begin(), str.end(), cmp);
        
        if(str[0] == "0") return "0";
        
        for(int i = 0; i < n; i++){
            ans += str[i];
        }
        
        return ans;
    }
};
```

# 204. Count Primes

## 题目

Given an integer `n`, return *the number of prime numbers that are strictly less than* `n`.

 

**Example 1:**

```
Input: n = 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```

**Example 2:**

```
Input: n = 0
Output: 0
```

**Example 3:**

```
Input: n = 1
Output: 0
```

## 题目大意

求n的前面有多少个素数。

## 思路

模板题，排除掉0、1和合数后剩下的就是素数。

## 代码

```c++
class Solution {
public:
    int primes[5000005];
    bool st[5000005];
    int countPrimes(int n) {
        if(n == 0 || n == 1) return 0;
        int cnt = 0;
        
        for(int i = 2; i < n; i++){
            if(!st[i]){
                primes[cnt++] = i;
            }
            for(int j = 0; primes[j] * i < n; j++){
                st[primes[j] * i] = true;
                if(i % primes[j] == 0) break;
            }
        }
        
        return cnt;
    }
};
```

# 227. Basic Calculator II

## 题目

Given a string `s` which represents an expression, *evaluate this expression and return its value*. 

The integer division should truncate toward zero.

You may assume that the given expression is always valid. All intermediate results will be in the range of `[-231, 231 - 1]`.

**Note:** You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

 

**Example 1:**

```
Input: s = "3+2*2"
Output: 7
```

**Example 2:**

```
Input: s = " 3/2 "
Output: 1
```

**Example 3:**

```
Input: s = " 3+5 / 2 "
Output: 5
```

## 题目大意

给定一个式子，计算它的值。

## 思路

一开始直接建立一个数字栈和一个符号栈来进行计算，发现既费时又费空间，后来看了解答，因为只有加减乘除四种符号，所以可以不建栈，遇到乘除可以直接计算，遇到加减结果可以加上加减号前面的那个数，减去一个数可以看做加上一个负数。

## 代码

```c++
class Solution {
public:
    int calculate(string s) {
        int n = s.size();
        int cur = 0, last = 0, res = 0;
        char sign = '+';
        for(int i = 0; i < n; i++){
            // if(s[i] == ' ') continue;
            char ops = s[i];
            if(isdigit(ops)){
                cur = cur * 10 + (ops - '0');
            }
            if(!isdigit(ops) && s[i] != ' ' || i == n - 1){
                if(sign == '+' || sign == '-'){
                    res += last;
                    last = sign == '+'? cur : -cur;
                }else if(sign == '/'){
                    last /= cur;
                }else if(sign == '*'){
                    last *= cur;
                }
                cur = 0;
                sign = ops;
            }
        }
        res += last;
        return res;
    }
};
```

栈的解法：

```c++
class Solution {
public:
    int cal(char op, int num1, int num2){
        if(op == '+'){
            return num1 + num2;
        }else if(op == '-'){
            return num1 - num2;
        }else if(op == '*'){
            return num1 * num2;
        }else{
            return num1 / num2;
        }
    }
    
    int calculate(string s) {
        int n = s.size();
        string num = "";
        stack<int> nums;
        stack<char> ops;
        for(int i = 0; i < n; i++){
            if(s[i] == ' ') continue;
            if(!isdigit(s[i])){
                nums.push(stoi(num));
                num = "";
                if(s[i] == '+' || s[i] == '-'){
                    while(!ops.empty()){
                        char op = ops.top();
                        ops.pop();
                        int num2 = nums.top();
                        nums.pop();
                        int num1 = nums.top();
                        nums.pop();
                        int res = cal(op, num1, num2);
                        nums.push(res);
                    }
                    ops.push(s[i]);
                }else{
                    while(!ops.empty() && (ops.top() == '*' || ops.top() == '/')){
                            char op = ops.top();
                            ops.pop();
                            int num2 = nums.top();
                            nums.pop();
                            int num1 = nums.top();
                            nums.pop();
                            int res = cal(op, num1, num2);
                            nums.push(res);
                    }
                    ops.push(s[i]);
                }
            }else{
                num += s[i];
            }
        }
        nums.push(stoi(num));
        while(!ops.empty()){
            char op = ops.top();
            ops.pop();
            int num2 = nums.top();
            nums.pop();
            int num1 = nums.top();
            nums.pop();
            int res = cal(op, num1, num2);
            nums.push(res);
        }
        return nums.top();
    }
};
```

# 289. Game of Life

## 题目

According to [Wikipedia's article](https://en.wikipedia.org/wiki/Conway's_Game_of_Life): "The **Game of Life**, also known simply as **Life**, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

The board is made up of an `m x n` grid of cells, where each cell has an initial state: **live** (represented by a `1`) or **dead** (represented by a `0`). Each cell interacts with its [eight neighbors](https://en.wikipedia.org/wiki/Moore_neighborhood) (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

1. Any live cell with fewer than two live neighbors dies as if caused by under-population.
2. Any live cell with two or three live neighbors lives on to the next generation.
3. Any live cell with more than three live neighbors dies, as if by over-population.
4. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.

The next state is created by applying the above rules  simultaneously to every cell in the current state, where births and  deaths occur simultaneously. Given the current state of the `m x n` grid `board`, return *the next state*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/12/26/grid1.jpg)

```
Input: board = [[0,1,0],[0,0,1],[1,1,1],[0,0,0]]
Output: [[0,0,0],[1,0,1],[0,1,1],[0,1,0]]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/12/26/grid2.jpg)

```
Input: board = [[1,1],[1,0]]
Output: [[1,1],[1,1]]
```

## 题目大意

一个格子附近的8个格子都是它的邻居，一个为1的格子只有附近有2个或3个为1的格子才能保持为1，否则为0；一个为0的格子只有附近有3个为1的格子才能为1，否则保持为0。

## 思路

每遍历一个格子都要遍历它的邻居，判断这个格子是否需要改变，如果需要改变就加2，对2求余就能知道这个格子原来的状态。最后输出格子的最终状态，大于等于2的就用3去减，来实现状态的更改，小于2的就不用变。

## 代码

```c++
class Solution {
public:
    bool change(vector<vector<int>>& board, int x, int y){
        int cnt = 0;
        int m = board.size(), n = board[0].size();
        for(int i = -1; i <= 1; i++){
            if(x + i < 0 || x + i >= m) continue;
            for(int j = -1; j <= 1; j++){
                if(i == 0 && j == 0) continue;
                else if(y + j < 0 || y + j >= n) continue;
                cnt += board[x+i][y+j] % 2;
            }
        }
        
        if(board[x][y] && (cnt < 2 || cnt > 3)) return true;
        else if(!board[x][y] && cnt == 3) return true;
        else return false;
    }
    
    void gameOfLife(vector<vector<int>>& board) {
        int m = board.size(), n = board[0].size();
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(change(board, i, j)){
                    board[i][j] += 2;
                }
            }
        }
        
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                board[i][j] = board[i][j] >= 2? 3 - board[i][j] : board[i][j];
            }
        }
    }
};
```

# 300. Longest Increasing Subsequence

## 题目

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

A **subsequence** is a sequence that can be derived from an array by deleting some or no elements without changing the order of  the remaining elements. For example, `[3,6,2,7]` is a subsequence of the array `[0,3,1,6,2,2,7]`.

 

**Example 1:**

```
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
```

## 题目大意

求最长严格上升子序列

## 思路

采用二分查找+贪心的方法，遍历数组构建一个严格上升的序列，如果当前元素大于序列的最后一位，则将该元素添加到序列最后；否则用二分查找找到大于等于该元素的最小元素的位置，将其放入，因为该数越小意味着能找到比它大的数的概率越大，其后面能接的数就越多。

## 代码

```c++
class Solution {
public:
    int search(int dp[], int pos, int num){
        int l = 0, r = pos;
        while(l < r){
            int mid = (l + r) / 2;
            if(num <= dp[mid]) r = mid;
            else l = mid + 1;
        }
        
        return l;
    }
    
    int lengthOfLIS(vector<int>& nums) {
        int pos = 0;
        int dp[2505] = {0};
        dp[pos] = nums[0];
        int n = nums.size();
        for(int i = 1; i < n; i++){
            if(nums[i] > dp[pos]){
                dp[++pos] = nums[i];
            }else{
                int tmp = search(dp, pos, nums[i]);
                dp[tmp] = nums[i];
            }
        }
        return pos + 1;
    }
};
```

# 322. Coin Change

## 题目

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return *the fewest number of coins that you need to make up that amount*. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

 

**Example 1:**

```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```

**Example 2:**

```
Input: coins = [2], amount = 3
Output: -1
```

**Example 3:**

```
Input: coins = [1], amount = 0
Output: 0
```

## 题目大意

给定一些面额的硬币，每种面额都有无数个硬币，给定一个金额，求组成这个金额所用的最少硬币数，如果无法组成这个金额，则返回-1。

## 思路

先判断这些面额能否组成这个金额，如果金额除不尽这些面额的最大公因数，则一定不能组成（好像有这个定理）；然后就是完全背包问题，最后还要再判断一下能不能组成（最后返回的值是否等于最大值）。

## 代码

```c++
class Solution {
public:
    int gcd(int a, int b){
        return b == 0? a : gcd(b, a % b);
    }
    
    int coinChange(vector<int>& coins, int amount) {
        int n = coins.size();
        int tmp = coins[0];
        for(int i = 1; i < n; i++){
            tmp = gcd(tmp, coins[i]);
        }
        if(amount % tmp) return -1;
        vector<int> dp(amount+1, 10005);
        dp[0] = 0;
        for(int i = 0; i < n; i++){
            for(int j = coins[i]; j <= amount; j++){
                dp[j] = min(dp[j], dp[j - coins[i]] + 1);
            }
        }
        if(dp[amount] == 10005) return -1;
        return dp[amount];
    }
};
```

# 324. Wiggle Sort II

## 题目

Given an integer array `nums`, reorder it such that `nums[0] < nums[1] > nums[2] < nums[3]...`.

You may assume the input array always has a valid answer.

 

**Example 1:**

```
Input: nums = [1,5,1,1,6,4]
Output: [1,6,1,5,1,4]
Explanation: [1,4,1,5,1,6] is also accepted.
```

**Example 2:**

```
Input: nums = [1,3,2,2,3,1]
Output: [2,3,1,3,1,2]
```

## 题目大意

给定一个整数数组，将其重新排序，使得偶数位上的数比两边的小，奇数位上的数比两边的大。

## 思路

**解法一**：将数组从小到大排序，前半部分放在偶数位，后半部分放在奇数位（P.S. 无论前半部分还是后半部分都要从后往前遍历）

**解法二**：将中间大的数放在中间，在这个数前面的比它小，在这个数后面的比它大，偶数位的指针从后往前遍历，奇数位的指针从前往后遍历，还有一个当前指针遍历整个数组。反正奇数位上的数要比中间数大，偶数位上的数要比中间数小。

## 代码

**解法一**：

```c++
class Solution {
public:
    void wiggleSort(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n = nums.size();
        vector<int> tmp(n, 0);
        int half = (n - 1) / 2;
        for(int k = 0, i = half, j = n-1; k < n && (i >= 0 || j > half); k+=2, i--, j--){
            tmp[k] = nums[i];
            if(k + 1 < n){
                tmp[k+1] = nums[j];
            }
        }
        
        nums = tmp;
    }
};
```

**解法二**：

```c++
class Solution {
public:
    void wiggleSort(vector<int>& nums) {
        int len = nums.size();
        nth_element(nums.begin(), nums.begin() + len/2, nums.end());
        int mid = *(nums.begin() + len/2);
        int small = len % 2? len - 1: len - 2;
        int large = 1;
        int cur = 0;
        
        while(cur < len){
            if(nums[cur] < mid && (cur < small || (cur > small && cur % 2))){
                swap(nums[cur], nums[small]);
                small -= 2;
            }else if(nums[cur] > mid && (cur > large || (cur < large && !(cur % 2)))){
                swap(nums[cur], nums[large]);
                large += 2;
            }else cur++;
        }
    }
};
```

# 328. Odd Even Linked List

## 题目

Given the `head` of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return *the reordered list*.

The **first** node is considered **odd**, and the **second** node is **even**, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in `O(1)` extra space complexity and `O(n)` time complexity.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/10/oddeven-linked-list.jpg)

```
Input: head = [1,2,3,4,5]
Output: [1,3,5,2,4]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/03/10/oddeven2-linked-list.jpg)

```
Input: head = [2,1,3,5,6,4,7]
Output: [2,3,6,7,1,5,4]
```

## 题目大意

把奇数项排在前面，把偶数项排在后面

## 思路

cur代表当前节点，odd代表奇数项，even代表偶数项。把odd放在cur的后面，更新odd，even，cur

## 代码

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        if(head == nullptr || head->next == nullptr || head->next->next == nullptr){
            return head;
        }
        
        ListNode* cur = head, *even = head->next, *odd = head->next->next;
        
        while(odd){
            even->next = odd->next;
            odd->next = cur->next;
            cur->next = odd;
            even = even->next;
            if(even){
                odd = even->next;
            }else odd = nullptr;
            cur = cur->next;
        }
        
        return head;
    }
};
```

# 334. Increasing Triplet Subsequence

## 题目

Given an integer array `nums`, return `true` *if there exists a triple of indices* `(i, j, k)` *such that* `i < j < k` *and* `nums[i] < nums[j] < nums[k]`. If no such indices exists, return `false`.

 

**Example 1:**

```
Input: nums = [1,2,3,4,5]
Output: true
Explanation: Any triplet where i < j < k is valid.
```

**Example 2:**

```
Input: nums = [5,4,3,2,1]
Output: false
Explanation: No triplet exists.
```

**Example 3:**

```
Input: nums = [2,1,5,0,4,6]
Output: true
Explanation: The triplet (3, 4, 5) is valid because nums[3] == 0 < nums[4] == 4 < nums[5] == 6.
```

## 题目大意

给定一个整数数列，如果存在三个索引`(i, j, k)`满足`i < j < k` 且 `nums[i] < nums[j] < nums[k]`，则返回true，否则返回false。

## 思路

i代表第一个数，j代表第二个数，i < j，遍历数组中的每一个数，如果当前的数小于等于i，替代i；否则（此时已大于i）如果当前的数小于等于j，替代j；否则（此时已大于j）就返回true。

## 代码

```c++
class Solution {
public:
    bool increasingTriplet(vector<int>& nums) {
        int i = INT_MAX, j = INT_MAX, n = nums.size();
        for(int k = 0; k < n; k++){
            if(nums[k] <= i) i = nums[k];
            else if(nums[k] <= j) j = nums[k];
            else return true;
        }
        return false;
    }
};
```

# 341. Flatten Nested List Iterator

## 题目

You are given a nested list of integers `nestedList`. Each element is either an integer or a list whose elements may also be  integers or other lists. Implement an iterator to flatten it.

Implement the `NestedIterator` class:

- `NestedIterator(List<NestedInteger> nestedList)` Initializes the iterator with the nested list `nestedList`.
- `int next()` Returns the next integer in the nested list.
- `boolean hasNext()` Returns `true` if there are still some integers in the nested list and `false` otherwise.

Your code will be tested with the following pseudocode:

```
initialize iterator with nestedList
res = []
while iterator.hasNext()
    append iterator.next() to the end of res
return res
```

If `res` matches the expected flattened list, then your code will be judged as correct.

 

**Example 1:**

```
Input: nestedList = [[1,1],2,[1,1]]
Output: [1,1,2,1,1]
Explanation: By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,1,2,1,1].
```

**Example 2:**

```
Input: nestedList = [1,[4,[6]]]
Output: [1,4,6]
Explanation: By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,4,6].
```

## 题目大意

实现一个类，要求如上。

## 思路

使用递归的思想实现，遍历当前list，如果当前元素是int，加入到结果list中，如果是list，则进入到这个list中遍历，返回遍历的结果（这个list），将这个list插入到当前的结果list中。

用idx标记当前元素（next（）），用cnt标记元素的个数，看遍历完没有。

## 代码

```c++
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Return true if this NestedInteger holds a single integer, rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds, if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Return the nested list that this NestedInteger holds, if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */

class NestedIterator {
private:
    vector<int> res;
    int idx = 0, cnt = 0;
    
    vector<int> flatten(vector<NestedInteger> &nested){
        int n = nested.size();
        vector<int> ans, tmp;
        for(int i = 0; i < n; i++){
            if(nested[i].isInteger()){
                ans.push_back(nested[i].getInteger());
            }else{
                tmp = flatten(nested[i].getList());
                ans.insert(ans.end(), tmp.begin(), tmp.end());
            }
        }
        return ans;
    }
    
public:
    NestedIterator(vector<NestedInteger> &nestedList) {
        res = flatten(nestedList);
        cnt = res.size();
    }
    
    int next() {
        return res[idx++];
    }
    
    bool hasNext() {
        return idx < cnt;
    }
};

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i(nestedList);
 * while (i.hasNext()) cout << i.next();
 */
```

# 347. Top K Frequent Elements

## 题目

Given an integer array `nums` and an integer `k`, return *the* `k` *most frequent elements*. You may return the answer in **any order**.

 

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**

```
Input: nums = [1], k = 1
Output: [1]
```

## 题目大意

找出k个在数组中出现得最频繁的数

## 思路

用unordered_map将每个数出现的次数记录下来，再将他们存进priority_queue中，取出前k个。

## 代码

```c++
class Solution {
public:
    unordered_map<int, int> cnt;
    priority_queue<pair<int, int>> heap;
    
    vector<int> topKFrequent(vector<int>& nums, int k) {
        vector<int> ans;
        int n = nums.size();
        for(int i = 0; i < n; i++){
            cnt[nums[i]]++;
        }
        for(auto a : cnt){
            heap.push({a.second, a.first});
        }
        for(int i = 0; i < k; i++){
            ans.push_back(heap.top().second);
            heap.pop();
        }
        return ans;
    }
};
```

# 371. Sum of Two Integers

## 题目

Given two integers `a` and `b`, return *the sum of the two integers without using the operators* `+` *and* `-`.

 

**Example 1:**

```
Input: a = 1, b = 2
Output: 3
```

**Example 2:**

```
Input: a = 2, b = 3
Output: 5
```

## 题目大意

不用+和-，求两数之和。

## 思路

用^，将数简单地加起来（不考虑进位）；用&再<<1（要保证是正数），算出进位。一直循环，直到b为0。

## 代码

```c++
class Solution {
public:
    int getSum(int a, int b) {
        
        while(b){
            int c = a ^ b;
            int d = (unsigned int)(a & b) << 1;
            a = c;
            b = d;
        }
        
        return a;
    }
};
```

# 378. Kth Smallest Element in a Sorted Matrix

## 题目

Given an `n x n` `matrix` where each of the rows and columns is sorted in ascending order, return *the* `kth` *smallest element in the matrix*.

Note that it is the `kth` smallest element **in the sorted order**, not the `kth` **distinct** element.

You must find a solution with a memory complexity better than `O(n2)`.

 

**Example 1:**

```
Input: matrix = [[1,5,9],[10,11,13],[12,13,15]], k = 8
Output: 13
Explanation: The elements in the matrix are [1,5,9,10,11,12,13,13,15], and the 8th smallest number is 13
```

**Example 2:**

```
Input: matrix = [[-5]], k = 1
Output: -5
```

## 题目大意

给定一个矩阵，矩阵的行和列都是升序排序的，求矩阵中第k小的元素。

## 思路

全程使用二分查找法。

## 代码

```c++
class Solution {
public:
    int search(vector<int>& mat, int l, int r, int num){
        while(l < r){
            int mid = (l + r) / 2;
            if(num >= mat[mid]) l = mid + 1;
            else r = mid;
        }
        
        if(mat[l] <= num) l++;
        return l;
    }
    
    int kthSmallest(vector<vector<int>>& matrix, int k) {
        int n = matrix.size();
        int l = matrix[0][0], r = matrix[n-1][n-1];
        while(l <= r){
            int cnt = 0;
            int mid = (l + r) / 2;
            for(int i = 0; i < n; i++){
                cnt += upper_bound(matrix[i].begin(), matrix[i].end(), mid) - matrix[i].begin();
                // cnt += search(matrix[i], 0, n - 1, mid);
            }
            
            if(cnt < k) l = mid + 1;
            else r = mid - 1;
        }
        
        
        return l;
    }
};
```

# 380. Insert Delete GetRandom O(1)

## 题目

Implement the `RandomizedSet` class:

- `RandomizedSet()` Initializes the `RandomizedSet` object.
- `bool insert(int val)` Inserts an item `val` into the set if not present. Returns `true` if the item was not present, `false` otherwise.
- `bool remove(int val)` Removes an item `val` from the set if present. Returns `true` if the item was present, `false` otherwise.
- `int getRandom()` Returns a random element from the  current set of elements (it's guaranteed that at least one element  exists when this method is called). Each element must have the **same probability** of being returned.

You must implement the functions of the class such that each function works in **average** `O(1)` time complexity.

 

**Example 1:**

```
Input
["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]
[[], [1], [2], [2], [], [1], [2], []]
Output
[null, true, false, true, 2, true, false, 2]

Explanation
RandomizedSet randomizedSet = new RandomizedSet();
randomizedSet.insert(1); // Inserts 1 to the set. Returns true as 1 was inserted successfully.
randomizedSet.remove(2); // Returns false as 2 does not exist in the set.
randomizedSet.insert(2); // Inserts 2 to the set, returns true. Set now contains [1,2].
randomizedSet.getRandom(); // getRandom() should return either 1 or 2 randomly.
randomizedSet.remove(1); // Removes 1 from the set, returns true. Set now contains [2].
randomizedSet.insert(2); // 2 was already in the set, so return false.
randomizedSet.getRandom(); // Since 2 is the only number in the set, getRandom() will always return 2.
```

## 题目大意

定义一个随机集合，可以增加任一不存在元素，删除任一存在元素，且随机获取集合中的一个数，平均时间复杂度均为O(1)。

## 思路

定义一个unordered_map（相当于哈希表），一个vector，可以用前者判断该元素是否已存在，记录每个值的索引。

## 代码

```c++
class RandomizedSet {
private:
    unordered_map<int, int> mp;
    vector<int> nums;
    
public:
    RandomizedSet() {
        
    }
    
    bool insert(int val) {
        if(mp.count(val)) return false;
        else{
            nums.push_back(val);
            mp[val] = nums.size() - 1;
            return true;
        }
    }
    
    bool remove(int val) {
        if(!mp.count(val)) return false;
        else{
            int idx = mp[val];
            swap(nums[idx], nums[nums.size()-1]);
            mp[nums[idx]] = idx;
            nums.pop_back();
            mp.erase(mp.find(val));
            return true;
        }
    }
    
    int getRandom() {
        return nums[rand() % nums.size()];
    }
};

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet* obj = new RandomizedSet();
 * bool param_1 = obj->insert(val);
 * bool param_2 = obj->remove(val);
 * int param_3 = obj->getRandom();
 */
```

# 384. Shuffle an Array

## 题目

Given an integer array `nums`, design an algorithm to randomly shuffle the array. All permutations of the array should be **equally likely** as a result of the shuffling.

Implement the `Solution` class:

- `Solution(int[] nums)` Initializes the object with the integer array `nums`.
- `int[] reset()` Resets the array to its original configuration and returns it.
- `int[] shuffle()` Returns a random shuffling of the array.

 

**Example 1:**

```
Input
["Solution", "shuffle", "reset", "shuffle"]
[[[1, 2, 3]], [], [], []]
Output
[null, [3, 1, 2], [1, 2, 3], [1, 3, 2]]

Explanation
Solution solution = new Solution([1, 2, 3]);
solution.shuffle();    // Shuffle the array [1,2,3] and return its result.
                       // Any permutation of [1,2,3] must be equally likely to be returned.
                       // Example: return [3, 1, 2]
solution.reset();      // Resets the array back to its original configuration [1,2,3]. Return [1, 2, 3]
solution.shuffle();    // Returns the random shuffling of array [1,2,3]. Example: return [1, 3, 2]
```

## 题目大意

完成一个类，给定一个整数数组，完成打乱、重置的功能，且打乱的每个排列组合的出现都要是等可能性的。

## 思路

重置将原始的保存下来即可，打乱采用Fisher-Yates算法（随机排列）。

## 代码

```c++
class Solution {
private:
    vector<int> origin;
    vector<int> shf;
    
public:
    Solution(vector<int>& nums) {
        origin = nums;
        shf = nums;
    }
    
    vector<int> reset() {
        return origin;
    }
    
    vector<int> shuffle() {
        int n = shf.size();
        for(int i = n - 1; i > 0; i--){
            swap(shf[i], shf[rand() % (i+1)]);
        }
        return shf;
    }
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(nums);
 * vector<int> param_1 = obj->reset();
 * vector<int> param_2 = obj->shuffle();
 */
```

# 395. Longest Substring with At Least K Repeating Characters

## 题目

Given a string `s` and an integer `k`, return *the length of the longest substring of* `s` *such that the frequency of each character in this substring is greater than or equal to* `k`.

 

**Example 1:**

```
Input: s = "aaabb", k = 3
Output: 3
Explanation: The longest substring is "aaa", as 'a' is repeated 3 times.
```

**Example 2:**

```
Input: s = "ababbc", k = 2
Output: 5
Explanation: The longest substring is "ababb", as 'a' is repeated 2 times and 'b' is repeated 3 times.
```

## 题目大意

求一个字符串中每个字母出现的次数大于等于k的最长子串。

## 思路

**Intuition**

There is another intuitive method to solve the problem by using the  Sliding Window Approach. The sliding window slides over the string `s` and validates each character. Based on certain conditions, the sliding window either expands or shrinks.

A substring is valid if each character has at least `k`  frequency. The main idea is to find all the valid substrings with a  different number of unique characters and track the maximum length.  Let's look at the algorithm in detail.

**Algorithm**

1. Find the number of unique characters in the string `s` and store the count in variable `maxUnique`. For `s` = `aabcbacad`, the unique characters are `a,b,c,d` and `maxUnique = 4`.
2. Iterate over the string `s` with the value of `currUnique` ranging from `1` to `maxUnique`. In each iteration, `currUnique`  is the maximum number of unique characters that must be present in the sliding window.
3. The sliding window starts at index `windowStart` and ends at index `windowEnd` and slides over string `s` until `windowEnd` reaches the end of string `s`. At any given point, we shrink or expand the window to ensure that the number of unique characters is not greater than `currUnique`.

- If the number of unique character in the sliding window is less than or equal to `currUnique`, expand the window from the right by adding a character to the end of the window given by `windowEnd`
- Otherwise, shrink the window from the left by removing a character from the start of the window given by `windowStart`.

1. Keep track of the number of unique characters in the current sliding window having at least `k` frequency given by `countAtLeastK`. Update the result if all the characters in the window have at least `k` frequency.

## 代码

```c++
class Solution {
public:
    int longestSubstring(string s, int k) {
        int ans = 0, n = s.size();
        int maxUni = getMaxUnique(s);
        int cnt[30] = {0};
        
        for(int uni = 1; uni <= maxUni; uni++){
            int st = 0, ed = 0, cntK = 0, cur = 0;
            memset(cnt, 0, sizeof(cnt));
            while(ed < n){
                if(cur <= uni){
                    int idx = s[ed] - 'a';
                    if(!cnt[idx]){
                        cur++;
                    }
                    cnt[idx]++;
                    if(cnt[idx] == k) cntK++;
                    ed++;
                }else{
                    int idx = s[st] - 'a';
                    if(cnt[idx] == 1){
                        cur--;
                    }
                    if(cnt[idx] == k) cntK--;
                    cnt[idx]--;
                    st++;
                }
                
                if(cur == uni && cur == cntK){
                    ans = max(ans, ed - st);
                }
            }
        }
        return ans;
    }
    
    int getMaxUnique(string s){
        int cnt[30] = {0};
        int n = s.size(), ans = 0;
        for(int i = 0; i < n; i++){
            if(!cnt[s[i] - 'a']){
                ans++;
                cnt[s[i] - 'a'] = 1;
            }
        }
        return ans;
    }
};
```

# 454. 4Sum II

## 题目

Given four integer arrays `nums1`, `nums2`, `nums3`, and `nums4` all of length `n`, return the number of tuples `(i, j, k, l)` such that:

- `0 <= i, j, k, l < n`
- `nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`

 

**Example 1:**

```
Input: nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
Output: 2
Explanation:
The two tuples are:
1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0
```

**Example 2:**

```
Input: nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
Output: 1
```

## 题目大意

给定四个数组`nums1`, `nums2`, `nums3`, 和 `nums4`，找出元组 `(i, j, k, l)` 的个数，使得：

- `0 <= i, j, k, l < n`
- `nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`

## 思路

先嵌套遍历前两个数组，计算两个元素的和的个数；再嵌套遍历后两个数组，如果 `- nums3[k] - nums4[l]`这个数存在，则说明`nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`成立，将 `- nums3[k] - nums4[l]`这个数的数量加入答案中。

## 代码

```c++
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        unordered_map<int, int> mp;
        int ans = 0, n = nums1.size();
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                mp[nums1[i]+nums2[j]]++;
            }
        }
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                if(mp.count(-nums3[i]-nums4[j])){
                    ans += mp[-nums3[i]-nums4[j]];
                }
            }
        }
        
        return ans;
    }
};
```

