---
title: Data Structures and Algorithms - Stack & Queue
pageTitle: palindrome()
---

## palindrome()

<span class="tags"><a href="#">Stack & Queue</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a function <span class="functions">palindrome()</span> that determines whether a given string is a palindrome.
<br><br>
**The function prototype is given as follows:**

<span class="functions">int palindrome(char *word);</span>
<br><br>
The function should return 0 if the string is a palindrome and -1 otherwise. You should ignore the null terminator. Ignore the case of each letter.
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
            Enter a string: A man a plan a canal Panama <br>
            The string is a palindrome. <br>
            <br>
            Enter a string: Superman in the sky <br>
            The string is not a palindrome.
			</p>
		</div>
		<div class="modal-footer">
			<button id="closeModalBtn">Close</button>
		</div>
	</div>
</div>
<br>

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

int palindrome(char *word);

//////////////////////////////////////////////////////////////////

int main()
{
	Stack s;
	Queue q;
	int item[]={1, 2, 3, 4, 5, 6, 5, 4, 3, 2, 1};
	int i;
	char *word1="A man a plan a canal Panama";
	char *word2="Superman in the sky";

	//char reply;

	palindrome(word1); //*word1="A man a plan a canal Panama";
	palindrome(word2);// *word2="Superman in the sky";

	return 0;

	//printf("enter any key to exit:");
	//fflush(stdin);
	//scanf("%c", &reply);
}

////////////////////////////////////////////////////////////////

int palindrome(char *word){
	int i, odd;
	Stack s1, s2;
	s1.ll.head=NULL;
	//s1.ll.tail =NULL;
	s1.ll.size =0;

	s2.ll.head =NULL;
	//s2.ll.tail =NULL;
	s2.ll.size=0;

	// Put the whole string in a stack and a queue, stripping out spaces
	printf("%s\n", word);
	while (*word){
		if (*word != ' '){
			push(&s1, toupper(*word));
		}
		word++;
	 }

	//pop half of the chars and push into s2;
	i= s1.ll.size /2;
	odd = s1.ll.size %2 ;
	while (i > 0){
		push(&s2, pop(&s1));
		i--;
	 }

	//if the string has odd chars, pop the middle one because we don't need to compare it.
	if (odd)
		pop(&s1);

	//compare two stacks
	while (!isEmptyStack(&s1))
		if (pop(&s1)!=pop(&s2))
		{   printf("The string is not a palindrome\n");
			return -1;
		}

	printf("The string is a palindrome\n");
	return 0;
}

void palindrome1(char *word){

	int i;
	Stack s;
	Queue q;

	s.ll.head = NULL;
	s.ll.tail = NULL;
	s.ll.size = 0;
	q.ll.head = NULL;
	q.ll.tail = NULL;
	q.ll.size = 0;

	// Put the whole string in a stack and a queue, stripping out spaces
	// Pop first half of stripped string off the stack letter by letter, comparing with second half

	printf("%s\n", word);

	while (*word){

		if (*word != ' '){
			push(&s, toupper(*word));
			enqueue(&q, toupper(*word));
		}
		word++;
	 }

	// Integer division by 2, ignores the middle character in an odd-length string

	 i = s.ll.size / 2;

	while (i > 0){
		if (pop(&s) != dequeue(&q)){
			printf("The string is not a palindrome\n");
			return;
		}
		i--;
	 }

	printf("The string is a palindrome\n");
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

