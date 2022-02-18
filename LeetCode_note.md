# LeetCode_note

## 前言：基于Leetcode总结/萌新刷题

### 数据结构：

#### ·链表

86.分隔链表：给你一个链表的头节点 head 和一个特定值 x ，请你对链表进行分隔，使得所有 小于 x 的节点都出现在 大于或等于 x 的节点之前。你应当 保留 两个分区中每个节点的初始相对位置。示例1：

```
输入：head = [1,4,3,2,5,2], x = 3
输出：[1,2,2,4,3,5]
```

```c
struct ListNode* partition(struct ListNode* head, int x)
{
    struct ListNode*small=malloc(sizeof(struct ListNode));
    small->next=NULL;//保存小于X的节点
    struct ListNode*big=malloc(sizeof(struct ListNode));
    big->next=NULL;//保存大于X的节点
    struct ListNode*first=NULL;//大于X链表头节点
    struct ListNode*last=NULL;//小于X链表头节点
    struct ListNode*px=head;
    while(px)
    {
        if(px->val<x)
        {
            if(first==NULL)
            {
                small->val=px->val;
                first=small;
                px=px->next;
            }
            else
            {
                small->next=px;
                small=px;
                px=px->next;
                small->next=NULL;
            }
        }
        else
        {
            if(last==NULL)
            {
                big->val=px->val;
                last=big;
                px=px->next;
            }
            else
            {
                big->next=px;
                big=px;
                px=px->next;
                big->next=NULL;
            }
        
        }

        
    }
    if(first==NULL)
    {
        return last;
    }
    else if(last==NULL)
    {
        return first;
    }
    else
    {
        small->next=last;
        return first;
    }
}
```



