---
title: Data Structures and Algorithms - Linked List - Assignments
---

## insertSortedLL() 

<span class="tags"><a href="/notes/data-structures-and-algorithms/linked-list/linked-list-main/">Linked List</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write a C function <span class="functions">insertSortedLL()</span> that asks the user to input an integer, then inserts it into the linked list in ascending order. The function, <span class="functions">insertSortedLL()</span>, should not allow inserting an integer if it already exists in the current linked list. The function should return the index position where the new item was added; if the function could not complete successfully, it should return a value of -1. You can assume that the linked list is either a sorted linked list or an
empty list.
<br><br>

**The function prototype is given as follows:**

<span class="functions">int insertSortedLL(LinkedList *ll, int item);</span>
<br><br>
If the current linked list is: **2 3 5 7 9**

Calling <span class="functions">insertSortedLL()</span> with a value of **8** will result in the following linked list:

**2 3 5 7 8 9**
<br><br>
The function should return the index position where the new item was added as follows:

*The value 8 was added at index 4*
<br><br>
If the current linked list is: **5 7 9 11 15**

Calling <span class="functions">insertSortedLL()</span> with a value of **7** will result in the following linked list:

**5 7 9 11 15**
<br><br>
The function does not complete successfully (does not insert the value of 7 to the linked list) hence
it should return a value of -1:

*The value 7 was added at index -1*
<br><br>
Your function should print the contents of the linked list after it has been created. This function
may be called multiple times for each time your program is running.
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
			1: Insert an integer to the sorted linked list: <br>
			2: Print the index of the most recent input value: <br>
			3: Print sorted linked list: <br>
			0: Quit: <br><br>
			Please input your choice (1/2/3/0): 1 <br>
			Input an integer that you want to add to the linked list: 2 <br>
			The resulting linked list is: 2 <br><br>
			Please input your choice (1/2/3/0): 1 <br> 
			Input an integer that you want to add to the linked list: 3 <br>
			The resulting linked list is: 2 3 <br><br>
			Please input your choice (1/2/3/0): 1 <br>
			Input an integer that you want to add to the linked list: 5 <br>
			The resulting linked list is: 2 3 5 <br><br>
			Please input your choice (1/2/3/0): 1 <br>
			Input an integer that you want to add to the linked list: 7 <br>
			The resulting linked list is: 2 3 5 7 <br><br>
			Please input your choice (1/2/3/0):1 <br>
			Input an integer that you want to add to the linked list: 9 <br>
			The resulting linked list is: 2 3 5 7 9 <br><br>
			Please input your choice (1/2/3/0): 1 <br>
			Input an integer that you want to add to the linked list: 8 <br>
			The resulting linked list is: 2 3 5 7 8 9 <br><br>
			Please input your choice (1/2/3/0): 2 <br>
			The value 8 was added at index 4 <br><br>
			Please input your choice(1/2/3/0):3 <br>
			The resulting sorted linked list is: 2 3 5 7 8 9 <br><br>
			Please input your choice(1/2/3/0): 1 <br>
			Input an integer that you want to add to the linked list: 5 <br>
			The resulting linked list is: 5 <br><br>
			Please input your choice(1/2/3/0): 1 <br>
			Input an integer that you want to add to the linked list: 7 <br>
			The resulting linked list is: 5 7 <br><br>
			Please input your choice(1/2/3/0): 1 <br>
			Input an integer that you want to add to the linked list: 9 <br>
			The resulting linked list is: 5 7 9 <br><br>
			Please input your choice(1/2/3/0): 1 <br>
			Input an integer that you want to add to the linked list: 5 <br>
			The resulting linked list is: 5 7 9 <br><br>
			Please input your choice (1/2/3/0): 2 <br>
			The value 5 was added at index -1 <br><br>
			Please input your choice(1/2/3/0):3 <br> 
			The resulting sorted linked list is: 5 7 9 <br><br>
			Please input your choice(1/2/3/0):
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

//////////////////////////////////////////////////////////////////////////////////

typedef struct _listnode{
	int item;
	struct _listnode *next;
} ListNode;			// You should not change the definition of ListNode

typedef struct _linkedlist{
	int size;
	ListNode *head;
} LinkedList;			// You should not change the definition of LinkedList


///////////////////////// function prototypes ////////////////////////////////////

//You should not change the prototype of this function
int insertSortedLL(LinkedList *ll, int item);

void printList(LinkedList *ll);
void removeAllItems(LinkedList *ll);
ListNode *findNode(LinkedList *ll, int index);
int insertNode(LinkedList *ll, int index, int value);
int removeNode(LinkedList *ll, int index);


//////////////////////////// main() //////////////////////////////////////////////

int main()
{
	LinkedList ll;
	int c, i, j;
	c = 1;

	//Initialize the linked list 1 as an empty linked list
	ll.head = NULL;
	ll.size = 0;

	printf("1: Insert an integer to the sorted linked list:\n");
	printf("2: Print the index of the most recent input value:\n");
	printf("3: Print sorted linked list:\n");
	printf("0: Quit:");

	while (c != 0)
	{
		printf("\nPlease input your choice(1/2/3/0): ");
		scanf("%d", &c);

		switch (c)
		{
		case 1:
			printf("Input an integer that you want to add to the linked list: ");
			scanf("%d", &i);
			j = insertSortedLL(&ll, i);
			printf("The resulting linked list is: ");
			printList(&ll);
			break;
		case 2:
			printf("The value %d was added at index %d\n", i, j);
			break;
		case 3:
			printf("The resulting sorted linked list is: ");
			printList(&ll);
			removeAllItems(&ll);
			break;
		case 0:
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

int insertSortedLL(LinkedList *ll, int item)
{
	/* add your code here */
    int i = 0;
    int size = ll->size;
	ListNode *p;

	if (size == 0)
    {
        insertNode(ll, 0, item);
        return 0;
    }

    p = ll->head;

    while (i < size)
    {
        p = findNode(ll, i);

        if (p->item == item)
            return -1;

        if (p->item > item)
        {
            insertNode(ll, i, item);
            //printf("The value %d was added at index %d \n", item, i);
            return i;
        }

        i++;
    }

    insertNode(ll, i, item);
    return i;
}

///////////////////////////////////////////////////////////////////////////////////

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


ListNode *findNode(LinkedList *ll, int index){

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

	if (ll == NULL || index < 0 || index > ll->size)
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
```

