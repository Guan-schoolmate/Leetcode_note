**86.分隔链表**给你一个链表的头节点 head 和一个特定值 x ，请你对链表进行分隔，使得所有 小于 x 的节点都出现在 大于或等于 x 的节点之前。你应当 保留 两个分区中每个节点的初始相对位置。示例1：

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

**19.删除链表的倒数第 N 个结点。** 给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。示例1：

```c
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```

```c
typedef struct ListNode ListNode;
struct ListNode* removeNthFromEnd(struct ListNode* head, int n)
{
    int t=0; 
	if(head==NULL)
	{
		return ;
	}
    if(head->next==NULL)
    {
        return head->next;
    }
	ListNode*p=head;
	ListNode*px=head;
	ListNode*pr=NULL;
	while(p)
	{
        if(n>0)
        {
            p=p->next;
            n--;
        }
        else
        {
            p=p->next;
            pr=px;
            px=px->next;
        }
		
	}
    if(pr==NULL)
    {
    head=px->next;
    px->next=NULL;
	free(px); 
    }
    else
    {
    pr->next=px->next;
	px->next=NULL;
	free(px);
    }
	return head;
}
//采用双指针 一个先走K步，之后同步走，当第一个到达末尾时，第二个所指即为到数第K个节点。
```

**21.合并两个有序链表。** 将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。示例1：

```c
输入：l1 = [1,2,4], l2 = [1,3,4]
输出：[1,1,2,3,4,4]
```

```c
struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2)
{
	struct ListNode* head=l1;
	struct ListNode* px=l1;//找插入位置
	struct ListNode* pr=NULL;//找插入位置前一个
	struct ListNode* pk=l2;//待插入的节点
	struct ListNode* ps=NULL;//待插入节点的下一个

	//三种情况1.头插2.中间插3.尾插
    if(l1==NULL)
    {
        return l2;
    }
    if(l2==NULL)
    {
        return l1;
    }
	//第一先找插入位置
	while(pk)
	{
		ps=pk;
		pk=pk->next;
        ps->next=NULL;
        pr=NULL;
        px=head;
		while(px)
		{
			if(px->val>ps->val)
			{
				break;
			}
			pr=px;
			px=px->next;
		}
		//找到插入位置了
		if(px)
		{
			if(px==head)
			{
				ps->next=head;
				head=ps;
			}
			else 
			{
                if(pr!=NULL)
                {
                    ps->next=px;
                    pr->next=ps;
                }
			}

		}
		else
		{
			pr->next=ps;
		}
	}
return head;
}
```

**24. 两两交换链表中的节点。** 给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。示例1：

```
输入：head = [1,2,3,4]
输出：[2,1,4,3]
```

```c
struct ListNode* swapPairs(struct ListNode* head)
{
	struct ListNode* ps=NULL;//指向pr前面
	struct ListNode* pr=NULL;//指向px前面
	struct ListNode* px=head;//链接指针
	struct ListNode* link=NULL;//链接指针
	int flag1=0;
	int flag2=0;
    if(head==NULL)
    {
        return NULL;
    }
	if(head->next==NULL)
	{
		return head;
	}
	pr=px;
	px=px->next;
	while(px)
	{
		if(flag1==0)
		{
			ps=pr;
			pr=px;
			px=px->next;
			pr->next=ps;
			ps->next=NULL;
			head=pr;
			link=ps;
			flag1=1;
		}
		if(px&&px->next==NULL)
		{
			link->next=px;
            px=px->next;;

		}
		else if(px&&px->next)
		{
			pr=px;
			px=px->next;
			ps=pr;
			pr=px;
			px=px->next;
			pr->next=ps;
			ps->next=NULL;
			link->next=pr;
			link=ps;
		}
	}
	return head;
}
```

