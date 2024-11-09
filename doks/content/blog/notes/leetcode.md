## [两数相加](https://leetcode.cn/problems/add-two-numbers/description/)
O(n)
从头至尾，逐位相加，如果进位，就向前加1。
```cpp
class Solution {

public:

    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {

        ListNode* l3 = new ListNode(0);

        ListNode* head = l3;

        ListNode* last = new ListNode(0);

        int up = 0;

        int v1, v2;

        for (;l1 !=nullptr || l2 != nullptr;) {

            if (l1 == nullptr) {

                v1 = 0;

            }else {

                v1 = l1->val;

                l1=l1->next;

            }

            if (l2 == nullptr) {

                v2 = 0;

            }else {

                v2 = l2->val;

                l2=l2->next;

            }

            int temp = v1 + v2 + up;

            if (temp >= 10) {

                up = 1;

                l3->next = new ListNode(temp - 10);

                l3 = l3 -> next;

                last = l3;

            }else {

                up = 0;

                l3->next = new ListNode(temp);

                l3 = l3 -> next;

                last = l3;

            }

        }

        if (up != 0) {

            last->next = new ListNode(up);

        }

        if (head->next != nullptr) {

            head = head -> next;

        }

        return head;

    }

};
```
题解中，更精简的代码，使用 问好表达式，同时各种情况都融合到while中：
```cpp
class Solution {

public:

    // 更精简

    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {

        ListNode* head = new ListNode(0);

        ListNode* first = head;

        int carry = 0;

        int v1,v2;

        while (l1 || l2 || carry) {

            v1 = l1 ? l1->val : 0;

            v2 = l2 ? l2->val : 0;

            l1 = l1 ? l1->next : nullptr;

            l2 = l2 ? l2->next : nullptr;

            carry = v1 + v2 + carry;

            int val = carry%10;

            carry = carry >= 10 ? 1 : 0;

            head -> next = new ListNode(val);

            head = head -> next;

        }

        return first->next;

    }

};
```
## [无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)
### 利用kmp的思想
每次搜索停止的时候，不需要重新开始查找。
```cpp
class Solution {

public:

    int lengthOfLongestSubstring(string s) {

        if (s == "") {

            return 0;

        }

        int max = 1;

        int end = 0;

        for (int i=0;i<s.size();i++) {

            int size = end - i;

            for (int j=end;j<s.size();j++) {  

                if (i != j && !(s.substr(i,j-i).find(s[j]) == string::npos)) {

                    end = j;

                    break;

                }

                size += 1;

            }

            max = max > size ? max : size;

        }

        return max;

    }

};
```
