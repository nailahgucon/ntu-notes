---
title: Data Structures and Algorithms - Stack & Queue
pageTitle: isStackPairwiseConsecutive()
---

## isStackPairwiseConsecutive()

<span class="tags"><a href="#">Stack & Queue</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write a C function write a function <span class="functions">isStackPairwiseConsecutive()</span> that checks whether numbers in the stack are pairwise consecutive or not. Note that the <span class="functions">isStackPairwiseConsecutive()</span> function only uses <span class="functions">push()</span> and <span class="functions">pop()</span> when adding or removing integers from the stack.
<br><br>

**The function prototype is given as follows:**

<span class="functions">int isStackPairwiseConsecutive(Stack *s);</span>
<br><br>
**Some examples:**

Test case 1<br>
_The stack is: 16 15 11 10 5 4_<br>
_The stack is pairwise consecutive_<br>
<br>
Test case 2<br>
_The stack is: 4 5 10 11 15 16_<br>
_The stack is pairwise consecutive_<br>
<br>
Test case 3<br>
_The stack is: 4 5 11 10 15 16_ <br>
_The stack is pairwise consecutive_<br>
<br>
Test case 4<br>
_The stack is: empty_<br>
_The stack is not pairwise consecutive_<br>
<br>
Test case 5<br>
_The stack is: 16 17 11 13 5 4_<br>
_The stack is not pairwise consecutive_<br>
<br>
Test case 6<br>
_The stack is: 16 15 11 10 5_<br>
_The stack is not pairwise consecutive_ <br>
<br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
			1: Insert an integer into the stack:<br>
			2: Check the stack is pairwise consecutive:<br>
			0: Quit:<br>
			<br>
			Please input your choice(1/2/0): 1<br>
			Input an integer that you want insert into the stack: 4<br>
			The stack is: 4<br>
			Please input your choice(1/2/0): 1<br>
			Input an integer that you want insert into the stack: 5<br>
			The stack is: 5 4<br>
			Please input your choice(1/2/0): 1<br>
			Input an integer that you want insert into the stack: 10<br>
			The stack is: 10 5 4<br>
			Please input your choice(1/2/0): 1<br>
			Input an integer that you want insert into the stack: 11<br>
			The stack is: 11 10 5 4<br>
			Please input your choice(1/2/0): 1<br>
			Input an integer that you want insert into the stack: 15<br>
			The stack is: 15 11 10 5 4<br>
			Please input your choice(1/2/0): 1<br>
			Input an integer that you want insert into the stack: 16<br>
			The stack is: 16 15 11 10 5 4<br>
			<br>
			Please input your choice(1/2/0): 2<br>
			The stack is pairwise consecutive.
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
#include <limits.h>
#define MIN_INT -1000

typedef struct _listnode{
   int item;
   struct _listnode *next;
} ListNode;

typedef struct _linkedlist{
   int size;
   ListNode *head;
   ListNode *tail;
} LinkedList;

////////////////////////////////// stack //////////////////////////////////////////

typedef struct stack{
	LinkedList ll;
} Stack;

////////////////////////// function prototypes ////////////////////////////////////

// You should not change the prototypes of these functions
int isStackPairwiseConsecutive(Stack *s);

void push(Stack *s, int item);
int pop(Stack *s);
int peek(Stack *s);
int isEmptyStack(Stack *s);

// You may use the following functions or you may write your own
void printList(LinkedList *ll);
ListNode * findNode(LinkedList *ll, int index);
int insertNode(LinkedList *ll, int index, int value);
int removeNode(LinkedList *ll, int index);
void removeAllItems(LinkedList *ll);

//////////////////////////////////////////////////////////////////////////////////////

int main()
{
    int c, value;

    Stack s;

    s.ll.head=NULL;
	s.ll.size =0;
	s.ll.tail =NULL;

    c =1;

    printf("1: Insert an integer into the stack:\n");
    printf("2: Check the stack is pairwise consecutive:\n");
    printf("0: Quit:\n");

    while (c != 0)
	{
		printf("Please input your choice(1/2/0): ");
		scanf("%d", &c);

		switch (c)
		{
		case 1:
			printf("Input an integer that you want insert into the stack: ");
			scanf("%d", &value);
			push(&s, value);
			printf("The stack is: ");
            printList(&(s.ll));
			break;
		case 2:
            if(isStackPairwiseConsecutive(&s))
            {
                printf("The stack is pairwise consecutive.\n");
            }
            else{
                printf("The stack is not pairwise consecutive.\n");
            }
            removeAllItems(&(s.ll));
            break;
		case 0:
			removeAllItems(&(s.ll));
			break;
		default:
			printf("Choice unknown;\n");
			break;
		}
	}

    return 0;
}

/////////////////////////////////////////////////////////////////////////////////

int isStackPairwiseConsecutive(Stack *s)
{
  	// add your code here 
  	if(s->ll.size == 0 || s->ll.size % 2 != 0) {
        return 0;
	}

    while(!isEmptyStack(s)){
    	//check difference in the pairs; use abs value
        if(abs(pop(s) - pop(s)) != 1){
            return 0;
		}
    }

    return 1;
}

//////////////////////////////////////////////////////////////////////////////////

void push(Stack *s, int item){
   insertNode(&(s->ll), 0, item);
}

int pop(Stack *s){
   int item;
   if(!isEmptyStack(s)){
    item = ((s->ll).head)->item;
    removeNode(&(s->ll), 0);
    return item;
   }
    return INT_MIN;
}

int peek(Stack *s){
   return ((s->ll).head)->item;
}

int isEmptyStack(Stack *s){
   if ((s->ll).size == 0)
      return 1;
   return 0;
}

//////////////////////////////////////////////////////////////////////////////////

void printList(LinkedList *ll){

	ListNode *cur;
	if (ll == NULL)
		return;
	cur = ll->head;

	if (cur == NULL)
		printf("Empty");
	while (cur != NULL)
	{
		printf("%d ", cur->item);
		cur = cur->next;
	}
	printf("\n");
}

ListNode * findNode(LinkedList *ll, int index){

	ListNode *temp;

	if (ll == NULL || index < 0 || index >= ll->size)
		return NULL;

	temp = ll->head;

	if (temp == NULL || index < 0)
		return NULL;

	while (index > 0){
		temp = temp->next;
		if (temp == NULL)
			return NULL;
		index--;
	}

	return temp;
}

int insertNode(LinkedList *ll, int index, int value){

	ListNode *pre, *cur;

	if (ll == NULL || index < 0 || index > ll->size + 1)
		return -1;

	// If empty list or inserting first node, need to update head pointer
	if (ll->head == NULL || index == 0){
		cur = ll->head;
		ll->head = malloc(sizeof(ListNode));
		ll->head->item = value;
		ll->head->next = cur;
		ll->size++;
		return 0;
	}


	// Find the nodes before and at the target position
	// Create a new node and reconnect the links
	if ((pre = findNode(ll, index - 1)) != NULL){
		cur = pre->next;
		pre->next = malloc(sizeof(ListNode));
		pre->next->item = value;
		pre->next->next = cur;
		ll->size++;
		return 0;
	}

	return -1;
}


int removeNode(LinkedList *ll, int index){

	ListNode *pre, *cur;

	// Highest index we can remove is size-1
	if (ll == NULL || index < 0 || index >= ll->size)
		return -1;

	// If removing first node, need to update head pointer
	if (index == 0){
		cur = ll->head->next;
		free(ll->head);
		ll->head = cur;
		ll->size--;

		return 0;
	}

	// Find the nodes before and after the target position
	// Free the target node and reconnect the links
	if ((pre = findNode(ll, index - 1)) != NULL){

		if (pre->next == NULL)
			return -1;

		cur = pre->next;
		pre->next = cur->next;
		free(cur);
		ll->size--;
		return 0;
	}

	return -1;
}

void removeAllItems(LinkedList *ll)
{
	ListNode *cur = ll->head;
	ListNode *tmp;

	while (cur != NULL){
		tmp = cur->next;
		free(cur);
		cur = tmp;
	}
	ll->head = NULL;
	ll->size = 0;
}

```

