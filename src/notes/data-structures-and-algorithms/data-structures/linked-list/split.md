---
title: Data Structures and Algorithms - Linked List - Assignments
pageTitle: split()
---

## split()

<span class="tags"><a href="#">Linked List</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a function <span class="functions">split()</span> that copies the contents of a linked list into two other linked lists.
<br><br>

**The function prototype is given as follows:**

<span class="functions">split(ListNode *head, ListNode **ptrEvenList, ListNode **ptrOddList);</span>
<br><br>
The function copies nodes with even indices (0, 2, 4, etc) to evenList and nodes with odd indices(1, 3, 5, etc) to oddList. The original linked list should not be modified.
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
    	    Current list: 1 3 5 2 4 6 19 16 7 <br>
            Even list: 1 5 4 19 7 <br>
            Odd list: 3 2 6 16
			</p>
		</div>
		<div class="modal-footer">
			<button id="closeModalBtn">Close</button>
		</div>
	</div>
</div>
<br>

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct _listnode{
	int num;
	struct _listnode *next;
} ListNode;


void printList(ListNode *cur);
ListNode * findNode(ListNode *cur, int index);
int insertNode(ListNode **ptrHead, int index, int item);
void deleteList(ListNode **ptrHead);

int split(ListNode *cur,ListNode **ptrEvenList,ListNode **ptrOddList);

int main()
{
    ListNode *head=NULL;
    ListNode *oddHead = NULL;
    ListNode *evenHead = NULL;

    int size =0;
    int item;

    printf("Enter a list of numbers, terminated by any non-digit character: \n");
    while(scanf("%d",&item))
        if(insertNode(&head,size, item)) size++;
    scanf("%*s");

    printf("\nBefore split() is called:\n ");
    printf("The original list: ");
    printList(head);

    split(head, &evenHead, &oddHead);

    printf("\nAfter split() was called:\n");
    printf("The original list: ");
    printList(head);
	printf("The even list: ");
	printList(evenHead);
	printf("The odd list: ");
	printList(oddHead);

	if(head!=NULL)
       deleteList(&head);
    if(oddHead!=NULL)
       deleteList(&oddHead);
    if(evenHead!=NULL)
       deleteList(&evenHead);
    return 0;
}

void printList(ListNode *cur){
    while (cur != NULL){
        printf("%d ", cur->num);
        cur = cur->next;
    }
    printf("\n");
}

ListNode *findNode(ListNode* cur, int index)
{
   if (cur==NULL || index<0)
      return NULL;
   while(index>0){
      cur=cur->next;
      if (cur==NULL)
         return NULL;
      index--;
   }
   return cur;
}

int insertNode(ListNode **ptrHead, int index, int value){
	ListNode *pre, *cur;
	// If empty list or inserting first node, need to update head pointer
	if (*ptrHead == NULL || index == 0){
		cur = *ptrHead;
		*ptrHead = malloc(sizeof(ListNode));
		(*ptrHead)->num = value;
		(*ptrHead)->next = cur;
		return 0;
	}
	// Find the nodes before and at the target position
	// Create a new node and reconnect the links
	if ((pre = findNode(*ptrHead, index-1)) != NULL){
		cur = pre->next;
		pre->next = malloc(sizeof(ListNode));
		pre->next->num = value;
		pre->next->next = cur;
		return 0;
	}
	return -1;
}

void deleteList(ListNode **ptrHead){
    ListNode *cur = *ptrHead;
    ListNode *temp;
    while (cur!= NULL) {
		temp=cur->next;
		free(cur);
		cur=temp;
	}
	*ptrHead=NULL;
}

int split(ListNode *head, ListNode **ptrEvenList, ListNode **ptrOddList)
{
	int even = 1, evenSize = 0, oddSize = 0;
	ListNode *cur=head;

	if (cur == NULL)
		return -1;
	while (cur!= NULL){
		if (even==1){
			insertNode(ptrEvenList, evenSize, cur->num);
			evenSize++;
		}
		else{
			insertNode(ptrOddList, oddSize, cur->num);
			oddSize++;
		}
	cur = cur ->next;
	even = -even;
	}
	return 0;
}

```

