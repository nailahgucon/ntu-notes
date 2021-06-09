---
title: Data Structures and Algorithms
pageTitle: Sum To C
---

## Sum To C

<span class="tags"><a href="#">Graph</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write a function, <span class="functions">sumToC()</span> to determine and print all possible sequences in ascending positive integers
that are summed to give a positive integer C where C < 50.
<br><br>

**For example, if the input value for C is 6, the output should be:**

<span class="functions">
1&nbsp;&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;&nbsp;3<br>
1&nbsp;&nbsp;&nbsp;&nbsp;5<br>
2&nbsp;&nbsp;&nbsp;&nbsp;4<br>
6
</span>
<br><br>

**The function prototype is given as follows:**

<span class="functions">
void sumToC ( LinkedList * ll , int C, ArrayList * al);
</span>
<br><br>

**The following structures are given for storing sequences:**

<span class="functions">
typedef struct _arraynode {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int * itemArray;<br>
&nbsp;&nbsp;&nbsp;&nbsp;int sizeArray; // the size of a possible sequence<br>
&nbsp;&nbsp;&nbsp;&nbsp;struct _arraynode * next;<br>
} ArrayNode;<br>
<br>
typedef struct _arraylist {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int size; // the number of possible sequences<br>
&nbsp;&nbsp;&nbsp;&nbsp;rrayNode * head;<br>
} ArrayList;<br>
<br>
typedef struct _listnode {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int item;<br>
&nbsp;&nbsp;&nbsp;&nbsp;struct _listnode * next;<br>
} ListNode;<br>
<br>
typedef struct _linkedlist {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int sum;<br>
&nbsp;&nbsp;&nbsp;&nbsp;int size;<br>
&nbsp;&nbsp;&nbsp;&nbsp;ListNode * head;<br>
} LinkedList;
</span>

<br><br>
All possible sequences (arrays with different length) will be stored in an ArrayList. LinkedList and ListNode is used for finding a sequence. The following utility functions are provided.
<br><br>

**The details can refer to the given template:**

<span class="functions">
int insertNode ( LinkedList *ll , int index , int coin );<br>
int removeNode ( LinkedList *ll , int index );<br>
ListNode * findNode ( LinkedList ll , int index );<br>
void removeAllItems ( LinkedList *ll);
</span>
<br><br>

*Hint: Using backtracking algorithm for finding all possible sequences.*
<br>

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct _arraynode
{
    int *itemArray;
    int sizeArray;
    struct _arraynode *next;
}ArrayNode;

typedef struct _arraylist{
   int size; //the size of a possible sequence
   ArrayNode *head;
} ArrayList;

typedef struct _listnode
{
    int item;
	struct _listnode *next;
} ListNode;

typedef struct _linkedlist{
   int sum; //the number of possible sequences
   int size;
   ListNode *head;
} LinkedList;

// You should not change the prototypes of these functions
//////LinkedList///////////////////////////////////////////
int insertNode(LinkedList *ll, int index, int coin);
int removeNode(LinkedList *ll, int index);
ListNode *findNode(LinkedList ll, int index);
void removeAllItems(LinkedList *ll);
///////////////////////////////////////////////////
void DFS_R(int x, LinkedList *ll, ArrayList *al);

void sumToC(LinkedList* ll, int C, ArrayList* al);
int main()
{
    int C;
    printf("Enter a number:\n");
    scanf("%d",&C);

    LinkedList ll;
    ll.head = NULL;
    ll.sum = 0;
    ll.size = 0;
    ArrayList al;
    al.head = NULL;
    al.size = 0;

    sumToC(&ll,C,&al);
    ArrayNode* temp;
    int i,j;
    temp = al.head;
    for(i=0;i<al.size;i++){
        for(j=0;j<temp->sizeArray;j++)
            printf(" %d ",temp->itemArray[j]);
        printf("\n");
        temp = temp->next;
    }

    return 0;
}

////////////////////////////////////////////////////////////////////////////////
// all these have to be global variables to be accessible for DFS_R and sumtoC
int results[50];
int sum = 0;
//int position = 0;
int position = -1;
int goal;
ArrayNode *an = NULL;

void DFS_R(int num, LinkedList *ll, ArrayList *al)
{
	int x;
	int total = sum + num;
	position++;

	results[position] = num;

	if (total > goal)
		return;

	if (total == goal){
		// printf("%d", goal);
		int *ar = (int *)malloc(sizeof(int) * position);
		for (x = 1; x <= position; x++){
			// ar[x] = results[x]; 
			ar[x - 1] = results[x];
		}
		// increase array list size
		al->size++;

		// inside array node: int *itemArray; int sizeArray; struct _arraynode *next;
		ArrayNode *an2 = (ArrayNode *)malloc(sizeof(ArrayNode));
		an2->itemArray = ar;
		an2->sizeArray = position;
		an2->next = NULL;
		// printf("%d",an2->sizeArray);

		if (al->size == 1)
			al->head = an2;
		else
			an->next = an2;
			// al->next = an2; 
		// al = an2;
		an = an2;
		return;
	}

	// for (i = num; i <= goal; i++) {	
	for (x = num + 1; sum + x <= goal; x++) {
		sum += num;
		// recursion
		// printf("%d", i);
		// printf("%d", sum);
		DFS_R(x, ll, al);
		sum -= num;
		// printf("%d", sum);
		position--;
	}
}

void sumToC(LinkedList* ll, int C, ArrayList* al)
{
	goal = C;
	// printf("%d", C);
	// for backtracking, need to use depth first search
	DFS_R(0, ll, al);
}
///////////////////////////////////////////////////////
int insertNode(LinkedList *ll, int index, int value){

	ListNode *pre, *cur;

	if (ll == NULL || index < 0 || index > ll->size)
		return 0;

        if (index == 0){
		cur = ll->head;
		ll->head = (ListNode*) malloc(sizeof(ListNode));
		ll->head->item = value;
		ll->head->next = cur;
		ll->sum += value;
		ll->size++;
		return 1;
	}


	// Find the nodes before and at the target position
	// Create a new node and reconnect the links
	if ((pre = findNode(*ll, index - 1)) != NULL){
		cur = pre->next;
		pre->next = malloc(sizeof(ListNode));
		pre->next->item = value;
		pre->next->next = cur;
		ll->sum += value;
		ll->size++;
		return 1;
	}

	return 0;
}


int removeNode(LinkedList *ll, int index){

	ListNode *pre, *cur;

	// Highest index we can remove is size-1
	if (ll == NULL || index < 0 || index > ll->size)
		return 0;

	// If removing first node, need to update head pointer
	if (index == 0){
		cur = ll->head->next;
		ll->sum -= ll->head->item;
		free(ll->head);
		ll->head = cur;
		ll->size--;
		return 1;
	}

	// Find the nodes before and after the target position
	// Free the target node and reconnect the links
	if ((pre = findNode(*ll, index - 1)) != NULL){

		if (pre->next == NULL)
			return 0;

		cur = pre->next;
		ll->sum -= cur->item;
		pre->next = cur->next;
		free(cur);
		ll->size--;
		return 1;
	}

	return 0;
}

ListNode *findNode(LinkedList ll, int index){

	ListNode *temp;

	if (index < 0 || index >= ll.size)
		return NULL;

	temp = ll.head;

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
	ll->sum =0;
}
```