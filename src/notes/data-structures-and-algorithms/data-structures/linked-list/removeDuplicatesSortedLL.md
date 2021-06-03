---
title: Data Structures and Algorithms - Linked List
pageTitle: removeDuplicatesSortedLL()
---

## removeDuplicatesSortedLL()

<span class="tags"><a href="#">Linked List</a></span>
<span class="tags"><a href="#">Tutorial</a></span>

<hr>

Write a C function <span class="functions">removeDuplicatesSortedLL()</span> that removes all duplicate values from a sorted linked list. You may assume that the list is already in ascending sorted order.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void removeDuplicatesSortedLL(LinkedList *ll);</span>
<br><br>
**For example:**

If the linked list is (1, 2, 2, 4, 4, 5, 5 ), the resulting linked list will be (1, 2, 4, 5).<br>
If the linked list is (1, 2, 3, 4, 5), the resulting linked list will be (1, 2, 3, 4, 5)
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
            1: Insert an integer to the linked list:<br>
            2: Remove duplicates from a sorted linked list:<br>
            0: Quit:<br>
            <br>
            Please input your choice(1/2/0): 1<br>
            Input an integer that you want to add to the linked list: 1<br>
            The resulting linked list is: 1<br>
            Please input your choice(1/2/0): 1<br>
            Input an integer that you want to add to the linked list: 2<br>
            The resulting linked list is: 1 2<br>
            Please input your choice(1/2/0): 1<br>
            Input an integer that you want to add to the linked list: 2<br>
            The resulting linked list is: 1 2 2<br>
            Please input your choice(1/2/0): 1<br>
            Input an integer that you want to add to the linked list: 4<br>
            The resulting linked list is: 1 2 2 4<br>
            Please input your choice(1/2/0): 1<br>
            Input an integer that you want to add to the linked list: 4<br>
            The resulting linked list is: 1 2 2 4 4<br>
            Please input your choice(1/2/0): 1<br>
            Input an integer that you want to add to the linked list: 5<br>
            The resulting linked list is: 1 2 2 4 4 5<br>
            Please input your choice(1/2/0): 1<br>
            Input an integer that you want to add to the linked list: 5<br>
            The resulting linked list is: 1 2 2 4 4 5 5<br>
            <br>
            Please input your choice(1/2/0): 2<br>
            The resulting linked list after removing duplicate values from the sorted linked list is: 1 2 4 5<br>
            <br>
            Please input your choice(1/2/0): 0
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
	int item;
	struct _listnode *next;
} ListNode;			// You should not change the definition of ListNode

typedef struct _linkedlist{
	int size;
	ListNode *head;
} LinkedList;			// You should not change the definition of LinkedList


///////////////////////// function prototypes ////////////////////////////////////

// You should not change the prototype of this function
void removeDuplicatesSortedLL(LinkedList *ll);
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

	//Initialize the linked list as an empty linked list
	ll.head = NULL;
	ll.size = 0;

	printf("1: Insert an integer to the linked list:\n");
	printf("2: Remove duplicates from a sorted linked list:\n");
	printf("0: Quit:\n");;

    while (c != 0)
	{
		printf("Please input your choice(1/2/0): ");
		scanf("%d", &c);

		switch (c)
		{
		case 1:
			printf("Input an integer that you want to add to the linked list: ");
			scanf("%d", &i);
			j = insertNode(&ll, ll.size, i);
			printf("The resulting linked list is: ");
			printList(&ll);
			break;
		case 2:
			removeDuplicatesSortedLL(&ll); // You need to code this function
			printf("The resulting linked list after removing duplicate values from the sorted linked list is: ");
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

void removeDuplicatesSortedLL(LinkedList *ll)
{
	ListNode *current = ll->head;
	if (current == NULL)
		return;
	while (current->next != NULL)
	{
		if (current->item == current->next->item)
		{
			ListNode *temp = current->next->next;
			free(current->next);
			current->next = temp;
			ll->size--;
		}
		else
		{
			current = current->next;
		}
	}
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

```

