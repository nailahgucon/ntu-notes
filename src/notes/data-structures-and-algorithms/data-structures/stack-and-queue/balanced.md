---
title: Data Structures and Algorithms - Stack & Queue
pageTitle: balanced()
---

## balanced()

<span class="tags"><a href="#">Stack & Queue</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a function <span class="functions">balanced()</span> that determines if an expression comprised of the characters ()[]{} is balanced.
<br><br>
**The function prototype is given as follows:**

<span class="functions">int balanced(char *expression);</span>
<br><br>
<img src = "{{ '/images/dsa-stackandqueue-balanced.PNG' | url }}" class="diagrams">
<br><br>

**The main function:**
<br>
<img src = "{{ '/images/dsa-stackandqueue-balanced-mainfunction.PNG' | url }}" class="diagrams">
<br><br>


```c
//#define _CRT_SECURE_NO_WARNINGS
#include "stdio.h"
#include <stdlib.h>

//////////////////////////////////   linked list //////////////////////////////////////////////

typedef struct _listnode{
   int item;
   struct _listnode *next;
} ListNode;

typedef struct _linkedlist{
   int size;
   ListNode *head;
   ListNode *tail;
} LinkedList;

////////////////////////////////// stack    //////////////////////////////////////////////

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

int  balanced(char *expression);

//////////////////////////// insert main function here //////////////////////////////////////

////////////////////////////////////////////////////////////
//Question 4

int balanced(char *expression){

	Stack s;
	s.ll.head = NULL;
	s.ll.tail = NULL;
	s.ll.size = 0;

	// Check one character at a time
	// If we see an opening bracket, store it in a stack
	// If we see a closing bracket, check stack for matching opening bracket (should be on top)
	// The moment we see a mismatch, expression is not balanced, return
	// If we finish looking at the expression and the stack is empty, it's balanced

	printf("%s\n", expression);

	while (*expression){

		if (*expression == '(' || *expression == '[' || *expression == '{'){
			push(&s, *expression);
		}

		else if (*expression == ')'){
			if (isEmptyStack(&s) || pop(&s) != '(')
				return -1;
		}

		else if (*expression == ']'){
			if (isEmptyStack(&s) || pop(&s) != '[')
				return -1;
		}

		else if (*expression == '}'){
			if (isEmptyStack(&s) || pop(&s) != '{')
				return -1 ;
		}

		expression++;

	 }

	if (isEmptyStack(&s)) return 0;
	else
		return -1;
}

////////////////////////////////////////////////////////////////////////////////

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

