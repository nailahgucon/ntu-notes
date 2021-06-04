---
title: Data Structures and Algorithms - Stack & Queue
pageTitle: reverse()
---

## reverse()

<span class="tags"><a href="#">Stack & Queue</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write a C function <span class="functions">reverse()</span> to reverse a queue using a stack. Note that the <span class="functions">reverse()</span> function only uses <span class="functions">push()</span> and <span class="functions">pop()</span> when adding or removing integers from the stack and only uses <span class="functions">enqueue()</span> and <span class="functions">dequeue()</span> when adding or removing integers from the queue.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void reverse(Queue *q);</span>
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
1: Insert an integer into the queue;<br>
2: Reverse the queue;<br>
0: Quit;<br>
<br>
Please input your choice(1/2/0): 1<br>
Input an integer that you want insert into the queue: 1<br>
The queue is: 1<br>
<br>
Please input your choice(1/2/0): 1<br>
Input an integer that you want insert into the queue: 2<br>
The queue is: 1 2<br>
<br>
Please input your choice(1/2/0): 1<br>
Input an integer that you want insert into the queue: 3<br>
The queue is: 1 2 3<br>
<br>
Please input your choice(1/2/0): 1<br>
Input an integer that you want insert into the queue: 4<br>
The queue is: 1 2 3 4<br>
<br>
Please input your choice(1/2/0): 2<br>
The resulting queue after reversing its elements is: 4 3 2 1
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

////////////////////////////////// stack    ///////////////////////////////////////////////////////

typedef struct stack{
	LinkedList ll;
} Stack;

//////////////////////////////////// queue ////////////////////////////////////////////////////////

typedef struct _queue{
	LinkedList ll;
} Queue;

///////////////////////////////////////////////////////////////////////////////////////////////////

void reverse(Queue *q);

///////////////////////////////////////////////////////////////////////////////////////////////////

void push(Stack *s, int item);
int pop(Stack *s);
int peek(Stack *s);
int isEmptyStack(Stack *s);

void enqueue(Queue *q, int item);
int dequeue(Queue *q);
int isEmptyQueue(Queue *s);

///////////////////////////////////////////////////////////////////////////////////////////////////
void printList(LinkedList *ll);
ListNode * findNode(LinkedList *ll, int index);
int insertNode(LinkedList *ll, int index, int value);
int removeNode(LinkedList *ll, int index);
void removeAllItems(LinkedList *ll);

///////////////////////////////////////////////////////////////////////////////////////////////////


int main()
{
    int c, value;

    Queue q;

    //initialize the queue
	q.ll.head =NULL;
	q.ll.size =0;
	q.ll.tail=NULL;

    c =1;

    printf("1: Insert an integer into the queue;\n");
    printf("2: Reverse the queue;\n");
    printf("0: Quit;\n");

    while (c != 0)
	{
		printf("Please input your choice(1/2/0): ");
		scanf("%d", &c);

		switch (c)
		{
		case 1:
			printf("Input an integer that you want insert into the queue: ");
			scanf("%d", &value);
			enqueue(&q, value);
			printf("The queue is: ");
			printList(&(q.ll));
			break;
		case 2:
			reverse(&q); // You need to code this function
			printf("The resulting queue after reversing its elements is: ");
			printList(&(q.ll));
			removeAllItems(&(q.ll));
			break;
		case 0:
			removeAllItems(&(q.ll));
			break;
		default:
			printf("Choice unknown;\n");
			break;
		}
	}

    return 0;
}

///////////////////////////////////////////////////////////////////////////////////////////////////

void reverse(Queue *q)
{
    // add your code here
	Stack stk;
	
	stk.ll.head = NULL;
	stk.ll.tail = NULL;
	stk.ll.size = 0;

	while(!isEmptyQueue(q)){
    	push(&stk, dequeue(q));
	}

	while(!isEmptyStack(&stk)){
    	enqueue(q, pop(&stk));
	}
}

///////////////////////////////////////////////////////////////////////////////////////////////////

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

void enqueue(Queue *q, int item){
   insertNode(&(q->ll), q->ll.size, item);
}

int dequeue(Queue *q){
   int item;
   item = ((q->ll).head)->item;
   removeNode(&(q->ll), 0);
   return item;
}

int isEmptyQueue(Queue *q){
   if ((q->ll).size == 0)
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

