---
title: Data Structures and Algorithms - Stack & Queue
pageTitle: createQueueFromLinkedList()
---

## createQueueFromLinkedList()

<span class="tags"><a href="#">Stack & Queue</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write a C function <span class="functions">createQueueFromLinkedList()</span> to create a queue (linked-list-based) by enqueuing all integers which are stored in the linked list. The first node of the linked list is enqueued first, and then the second node, and so on. Remember to empty the queue at the beginning, if the queue is not empty.
<br><br>
After the queue is built, write another C function <span class="functions">removeOddValues()</span> to remove all odd integers from the queue. Note that you should only use <span class="functions">enqueue()</span> or <span class="functions">dequeue()</span> when you add or remove integers from queues.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void createQueueFromLinkedList(LinkedList *ll , Queue *q);</span><br>
<span class="functions">void removeOddValues(Queue *q);</span>
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
            The resulting linked list is: 1 2 3 4 5<br>
            <br>
            Please input your choice(1/2/3/0): 2<br>
            The resulting queue is: 1 2 3 4 5<br>
            <br>
            Please input your choice(1/2/3/0): 3<br>
            The resulting queue after removing odd integers is: 2 4
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

typedef struct _listnode
{
	int item;
	struct _listnode *next;
} ListNode;	// You should not change the definition of ListNode

typedef struct _linkedlist
{
	int size;
	ListNode *head;
} LinkedList;	// You should not change the definition of LinkedList


typedef struct _queue
{
	LinkedList ll;
} Queue;  // You should not change the definition of Queue

///////////////////////// function prototypes ////////////////////////////////////

// You should not change the prototypes of these functions
void createQueueFromLinkedList(LinkedList *ll, Queue *q);
void removeOddValues(Queue *q);
void enqueue(Queue *q, int item);
int dequeue(Queue *q);
int isEmptyQueue(Queue *q);
void removeAllItemsFromQueue(Queue *q);


// You may use the following functions or you may write your own
void printList(LinkedList *ll);
void removeAllItems(LinkedList *ll);
ListNode * findNode(LinkedList *ll, int index);
int insertNode(LinkedList *ll, int index, int value);
int removeNode(LinkedList *ll, int index);

//////////////////////////// main() //////////////////////////////////////////////

int main()
{
	int c, i;
	LinkedList ll;
	Queue q;

	c = 1;

	// Initialize the linked list as an empty linked list
	ll.head = NULL;
	ll.size = 0;

	// Initialize the Queue as an empty queue
	q.ll.head = NULL;
	q.ll.size = 0;


	printf("1: Insert an integer into the linked list:\n");
	printf("2: Create the queue from the linked list:\n");
	printf("3: Remove odd numbers from the queue:\n");
	printf("0: Quit:\n");


	while (c != 0)
	{
		printf("Please input your choice(1/2/3/0): ");
		scanf("%d", &c);

		switch (c)
		{
		case 1:
			printf("Input an integer that you want insert into the List: ");
			scanf("%d", &i);
			insertNode(&ll, ll.size, i);
			printf("The resulting linked list is: ");
			printList(&ll);
			break;
		case 2:
			createQueueFromLinkedList(&ll, &q); // You need to code this function
			printf("The resulting queue is: ");
			printList(&(q.ll));
			break;
		case 3:
			removeOddValues(&q); // You need to code this function
			printf("The resulting queue after removing odd integers is: ");
			printList(&(q.ll));
			removeAllItemsFromQueue(&q);
			removeAllItems(&ll);
			break;
		case 0:
			removeAllItemsFromQueue(&q);
			removeAllItems(&ll);
			break;
		default:
			printf("Choice unknown;\n");
			break;
		}

	}

	return 0;
}


//////////////////////////////////////////////////////////////////////////////////

void createQueueFromLinkedList(LinkedList *ll, Queue *q)
{
	//add your code here
	int i;
	ListNode *LN;

	while(!isEmptyQueue(q)) {
        dequeue(q);
	}

	for(i=0; i<ll->size; i++) {
        LN = findNode(ll, i);
        enqueue(q, LN->item);
    }
}

void removeOddValues(Queue *q)
{
	//add your code here
	int i, item;
	int size = q->ll.size;

	for(i=0; i<size; i++) {
        item = dequeue(q);

        if(item % 2 == 0) {
            enqueue(q, item);
		}
    }
}

//////////////////////////////////////////////////////////////////////////////////

void enqueue(Queue *q, int item) {
	insertNode(&(q->ll), q->ll.size, item);
}

int dequeue(Queue *q) {
	int item;

	if (!isEmptyQueue(q)) {
		item = ((q->ll).head)->item;
		removeNode(&(q->ll), 0);
		return item;
	}
	return -1;
}

int isEmptyQueue(Queue *q) {
	if ((q->ll).size == 0)
		return 1;
	return 0;
}

void removeAllItemsFromQueue(Queue *q)
{
	int count, i;
	if (q == NULL)
		return;
	count = q->ll.size;

	for (i = 0; i < count; i++)
		dequeue(q);
}


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
		if (ll->head == NULL)
		{
			exit(0);
		}
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
		if (pre->next == NULL)
		{
			exit(0);
		}
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

```

