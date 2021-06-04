---
title: Data Structures and Algorithms - Stack & Queue
pageTitle: removeUntil()
---

## removeUntil()

<span class="tags"><a href="#">Stack & Queue</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a function <span class="functions">removeUntil()</span> that pops all values off a stack of integers down to but not including the first occurrence of the chosen value.
<br><br>
**The function prototype is given as follows:**

<span class="functions">void removeUntil(Stack *s, int value);</span>
<br><br>
Given a stack [1 2 3 4 5 6 5 4 3 2 1] with the topmost number displayed on the left, calling <span class="functions">removeUntil()</span> with value = 5 will produce the stack [5 6 5 4 3 2 1].
<br><br>

```c
//#define _CRT_SECURE_NO_WARNINGS
#include "stdio.h"
#include <stdlib.h>

////////////////////////////////// linked list //////////////////////////////////////////////

typedef struct _listnode{
   int item;
   struct _listnode *next;
} ListNode;

typedef struct _linkedlist{
   int size;
   ListNode *head;
   ListNode *tail;
} LinkedList;

////////////////////////////////// stack //////////////////////////////////////////////

typedef struct stack{
	LinkedList ll;
} Stack;

//////////////////////////////////// queue ////////////////////////////////////////////

typedef struct _queue{
	LinkedList ll;
} Queue;

////////////////////////////////////////////////////////////////////////////////
void printList(ListNode *head);
ListNode * findNode(LinkedList *ll, int index);
int insertNode(LinkedList *ll, int index, int value);
int removeNode(LinkedList *ll, int index);

//////////////////////////////////////////////////

void push(Stack *s, int item);
int pop(Stack *s);
int peek(Stack *s);
int isEmptyStack(Stack *s);

//////////////////////////////////////////////////

void enqueue(Queue *q, int item);
int dequeue(Queue *q);
int isEmptyQueue(Queue *s);

///////////////////////////////////////////////////////////////
void removeUntil(Stack *s, int value);

//////////////////////////////////////////////////////////////////
/////

int main()
{
	Stack s;
	Queue q;
	int item[]={1, 2, 3, 4, 5, 6, 5, 4, 3, 2, 1};
	int i;
	char *word1="A man a plan a canal Panama";
	char *word2="Superman in the sky";

	//char reply;

	//initialize the stack
	s.ll.head=NULL;
	s.ll.size =0;
	s.ll.tail =NULL;

	for(i=0;i<11;i++)
		push(&s, item[i]);

	printList(s.ll.head);
	removeUntil(&s,5);
	printList(s.ll.head);

	return 0;

	//printf("enter any key to exit:");
	//fflush(stdin);
	//scanf("%c", &reply);
}

////////////////////////////////////////////////////////////////
//Question 1

void removeUntil(Stack *s, int value){

	while (!isEmptyStack(s)){
		if (peek(s) != value)
			pop(s);

		else
			break;
	}
}

////////////////////////////////////////////////////////////

void push(Stack *s, int item){
   insertNode(&(s->ll), 0, item);
}

int pop(Stack *s){
   int item;

   item = ((s->ll).head)->item;
   removeNode(&(s->ll), 0);
   return item;
}

int peek(Stack *s){
   return ((s->ll).head)->item;
}

int isEmptyStack(Stack *s){
   if ((s->ll).size == 0)
      return 1;
   return 0;
}


////////////////////////////////////////////////////////////////////////////////

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



////////////////////////////////////////////////////////////////////////////////

void printList(ListNode *head){

   ListNode *temp = head;

   if (temp == NULL)
      return;

   while (temp != NULL){
      printf("%d ", temp->item);
      temp = temp->next;
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
      ll->tail = ll->head;
      ll->head->item = value;
      ll->head->next = cur;
      ll->size++;
      return 0;
   }

   // Inserting as new last node
   if (index == ll->size){
      pre = ll->tail;
      cur = pre->next;
      pre->next = malloc(sizeof(ListNode));
      ll->tail = pre->next;
      pre->next->item = value;
      pre->next->next = cur;
      ll->size++;
      return 0;
   }

   // Find the nodes before and at the target position
   // Create a new node and reconnect the links
   if ((pre = findNode(ll, index-1)) != NULL){
      cur = pre->next;
      pre->next = malloc(sizeof(ListNode));

      if (index == ll->size)
         ll->tail = pre->next;

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

      if (ll->size == 0)
         ll->tail = 0;

      return 0;
   }

   // Find the nodes before and after the target position
   // Free the target node and reconnect the links
   if ((pre = findNode(ll, index-1)) != NULL){

      // Removing the last node, update the tail pointer
      if (index == ll->size - 1){
         ll->tail = pre;
         free(pre->next);
         pre->next = NULL;
      }
      else{
         cur = pre->next->next;
         free(pre->next);
         pre->next = cur;
      }
      ll->size--;
      return 0;
   }

   return -1;
}

```

