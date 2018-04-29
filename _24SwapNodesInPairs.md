### 两两交换链表中的节点<h1>
### 描述<h2>
> 给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。
### 示例:<h3>
```
给定 1->2->3->4, 你应该返回 2->1->4->3.
```
### 说明:<h4>
- 你的算法只能使用常数的额外空间。
- 你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。
### 分析<h5>
> 单向链表，用两个指针来交换，用一个指针定位上次的位置
### 代码<h6>
```C++
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
    ListNode* swapPairs(ListNode* head) {
        typedef ListNode* ls;
        if(head==NULL)return NULL;
        if(head->next==NULL)return head;
        ls temp=NULL;
        ls p1,p2;
        p1=head;
        p2=p1->next;
        head=p2;
        while(true)
        {
            if(p1->next==NULL)break;
            if(p2==NULL)break;
            if(temp)temp->next=p2;
            p1->next=p2->next;
            p2->next=p1;
            temp=p1;
            if(p1->next)
            p1=p1->next;
            else break;

            p2=p1->next;
        }
        return head;
    }
};
```
