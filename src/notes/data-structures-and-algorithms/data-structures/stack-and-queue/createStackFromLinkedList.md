---
title: Data Structures and Algorithms - Stack & Queue
pageTitle: createStackFromLinkedList()
---

## createStackFromLinkedList()

<span class="tags"><a href="#">Stack & Queue</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write a C function <span class="functions">createStackFromLinkedList()</span> to create a stack (linked-list-based) by pushing all integers that are storing in the linked list. The first node of the linked list is pushed first, and then the second node, and so on. Remember to empty the stack at the beginning, if the stack is not empty.
<br><br>
After the stack is built, write another C function <span class="functions">removeEvenValues()</span> to remove all even integers from the stack. Note that you should only use <span class="functions">push()</span> or <span class="functions">pop()</span> when you add or remove integers from stack.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void createStackFromLinkedList(LinkedList *ll , Stack *stack);</span><br>
<span class="functions">void removeEvenValues(Stack *s);</span>
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
            The resulting linked list is: 1 3 5 6 7<br>
            <br>
            Please input your choice(1/2/3/0): 2<br>
            The resulting stack is: 7 6 5 3 1<br>
            <br>
            Please input your choice(1/2/3/0): 3<br>
            The resulting stack after removing even integers is: 7 5 3 1
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

typedef struct _stack
{
	LinkedList ll;
}Stack;  // You should not change the definition of Stack

///////////////////////// function prototypes ////////////////////////////////////

// You should not change the prototypes of these functions
void createStackFromLinkedList(LinkedList *ll , Stack *stack);
void removeEvenValues(Stack *s);

void push(Stack *s , int item);
int pop(Stack *s);
int isEmptyStack(Stack *s);
void removeAllItemsFromStack(Stack *s);

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
	Stack s;

	c = 1;
	// Initialize the linked list as an empty linked list
	ll.head = NULL;
	ll.size = 0;

	// Initalize the stack as an empty stack
	s.ll.head = NULL;
	s.ll.size = 0;

	printf("1: Insert an integer into the linked list:\n");
	printf("2: Create the stack from the linked list:\n");
	printf("3: Remove even numbers from the stack:\n");
	printf("0: Quit:\n");

	while (c != 0)
	{
		printf("Please input your choice(1/2/3/0): ");
		scanf("%d", &c);

		switch (c)
		{
		case 1:
			printf("Input an integer that you want to add to the linked list: ");
			scanf("%d", &i);
			insertNode(&ll, ll.size, i);
			printf("The resulting linked list is: ");
			printList(&ll);
			break;
		case 2:
			createStackFromLinkedList(&ll, &s); // You need to code this function
			printf("The resulting stack is: ");
			printList(&(s.ll));
			break;
		case 3:
			removeEvenValues(&s); // You need to code this function
			printf("The resulting stack after removing even integers is: ");
			printList(&(s.ll));
			removeAllItemsFromStack(&s);
			removeAllItems(&ll);
			break;
		case 0:
			removeAllItemsFromStack(&s);
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

void createStackFromLinkedList(LinkedList *ll, Stack *s)
{
	//add your code here
	int i, size = ll->size;
    ListNode *LN;

    while(!isEmptyStack(s)){
        pop(s);
	}

    for(i=0; i<size; i++)
    {
        LN = findNode(ll, i);
        push(s, LN->item);
    }
}

void removeEvenValues(Stack *s)
{
	// add your code here
	int num;

	if(isEmptyStack(s)){
        return;
	}

	num = pop(s);
	removeEvenValues(s);

	if(num % 2 != 0){
        push(s, num);
	}
}

//////////////////////////////////////////////////////////////////////////////////

void push(Stack *s, int item)
{
	insertNode(&(s->ll), 0, item);
}

int pop(Stack *s)
{
	int item;
	if (s->ll.head != NULL)
	{
		item = ((s->ll).head)->item;
		removeNode(&(s->ll), 0);
		return item;
	}
	else
		return MIN_INT;
}

int isEmptyStack(Stack *s)
{
	if ((s->ll).size == 0)
		return 1;
	else
		return 0;
}


void removeAllItemsFromStack(Stack *s)
{
	if (s == NULL)
		return;
	while (s->ll.head != NULL)
	{
		pop(s);
	}
}

//////////////////////////////////////////////////////////////////////////////////////////


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

