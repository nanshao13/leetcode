#### [19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

像这种一次遍历找第N个数的类似的题目，就可以用快慢指针来做。

快指针先走N步，然后快慢指针一起走，当快指针为空的时候，慢指针就指向的是目标了。

```cpp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode *dummyHead = new ListNode;
        dummyHead->next = head;
        ListNode *slow = dummyHead;
        ListNode *fast = dummyHead;
        while (n--) {
            fast = fast->next;
        }
        fast = fast->next;
        while (fast) {
            slow = slow->next;
            fast = fast->next;
        }
        ListNode *tmp = slow->next;
        slow->next = slow->next->next;
        delete tmp;
        ListNode *res = dummyHead->next;
        delete dummyHead;
        return res;
    }
};
```

