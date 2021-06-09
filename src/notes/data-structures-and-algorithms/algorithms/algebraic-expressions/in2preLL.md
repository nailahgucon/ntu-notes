---
title: Data Structures and Algorithms
pageTitle: in2preLL()
---

## in2preLL()

<span class="tags"><a href="#">Algebraic Expressions</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write a function, <span class="functions">in2preLL()</span> to covert an infix expression into a prefix expression linked list. We assumed that the character string only contains positive integer numbers, operators (`+', `-', `*' and `/') and parentheses.
<br><br>

**You may need the following stack structure:**

<span class="functions">
enum ExpType {OPT , OPERAND };<br>
<br>
typedef struct _stackNode {<br>
&nbsp;&nbsp;&nbsp;&nbsp;char item;<br>
&nbsp;&nbsp;&nbsp;&nbsp;struct _stackNode * next;<br>
} StackNode;<br>
<br>
typedef struct _stack {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int size;<br>
&nbsp;&nbsp;&nbsp;&nbsp;StackNode * head;<br>
} Stack;<br>
<br>
typedef struct _listnode {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int item;<br>
&nbsp;&nbsp;&nbsp;&nbsp;enum ExpType type;<br>
&nbsp;&nbsp;&nbsp;&nbsp;struct _listnode * next;<br>
} ListNode;<br>
<br>
typedef struct _linkedlist {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int size;<br>
&nbsp;&nbsp;&nbsp;&nbsp;ListNode * head;<br>
} LinkedList;
</span>
<br><br>

**The following utility functions are provided. The details can refer to the given template:**

<span class="functions">
void push ( Stack *sPtr , char item );<br>
int pop ( Stack * sPtr );<br>
char peek ( Stack s);<br>
int isEmptyStack ( Stack s);<br>
<br>
void insertNode ( LinkedList *llPtr , int item , enum ExpType type );<br>
int deleteNode ( LinkedList * llPtr );<br>
void removeAllNodes ( LinkedList * llPtr );<br>
int isEmptyLinkedList ( LinkedList ll);
</span>
<br><br>

**The function prototype is given as follows:**

<span class="functions">void in2preLL ( LinkedListExp * ExpLL );</span>
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
            Input: 99+(88-77)*(66/(55-44)+33)<br>
            Output: + 99 * - 88 77 + / 66 - 55 44 33
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

#define SIZE 80 //The size of the array

enum ExpType {OPT,OPERAND};

typedef struct _stackNode{
    char item;
    struct _stackNode *next;
}StackNode;

typedef struct _stack{
   int size;
   StackNode *head;
}Stack;

void push(Stack *sPtr, char item);
int pop(Stack *sPtr);
char peek(Stack s);
int isEmptyStack(Stack s);

typedef struct _listnode
{
    int  item;
    enum ExpType type;
	struct _listnode *next;
} ListNode;

typedef struct _linkedlist{
   int size;
   ListNode *head;
} LinkedList;

void insertNode(LinkedList *llPtr, int item,enum ExpType type);
int deleteNode(LinkedList *llPtr);
void removeAllNodes(LinkedList *llPtr);
int isEmptyLinkedList (LinkedList ll);


void in2PreLL(char* infix, LinkedList *inExpLL);

void printExpLL(LinkedList inExpLL);

int main()
{
    char infix[SIZE];

    //printf("Enter an infix expression:\n");
    gets(infix);

    LinkedList inExpLL;
    inExpLL.head = NULL;
    inExpLL.size = 0;

    in2PreLL(infix, &inExpLL);

    printExpLL(inExpLL);

    removeAllNodes(&inExpLL);
    return 0;
}

int precedence(char op) {
    if(op == '*' || op == '/') {
        return 1;
    }
    else {
        return 0;
    }
}

void in2PreLL(char* infix, LinkedList *inExpLL)
{
    Stack s;
    s.head = NULL;
    s.size = 0;

    char l1[SIZE], l2[SIZE];
    char c, temp;
    int count = 0;
    int i = 0;
    int j = 0;
    int k = 0;
    
     // count char in infix
     while(infix[count]!='\0')
            count++;
    count -= 1;

    while(count >= 0) {
        c = infix[count];  
        // take note of operands; prevent num splitting in LL
        if(c >= '0' && c <= '9') {
            l1[j] = c;
            j++;
        } else if (c == '(') {
                if(j != 0) {
                    k = j;
                    for (i = 0; i < j; i++) {
                        // l2[i] = l1[k--]; <- makes everything 0
                        l2[i] = l1[k-1];
                        k--;
                    }
                    l2[i] = '\0';
                    i = 0;
                    j = 0;
                    //printf("<%c>", l2[0]);
                    insertNode(inExpLL,atoi(l2),OPERAND);
                    l1[0] = '\0';
                    l2[0] = '\0';
                }
                //populate linked list with operators
                while(peek(s) != ')'){
                    //printf("<%c>", peek(s));
                    insertNode(inExpLL,peek(s),OPT);
                    pop(&s);
                }
                pop(&s);
        } else if (c == ')') {
                if(j != 0) {
                    k = j;
                    for (i = 0; i < j; i++) {
                        l2[i] = l1[k-1];
                        k--;
                    }
                    l2[i] = '\0';
                    i = 0;
                    j = 0;
                    insertNode(inExpLL,atoi(l2),OPERAND);
                    l1[0] = '\0';
                    l2[0] = '\0';
                }
                push(&s,c);
        } else {
                if(j != 0) {
                    k = j;
                    for (i = 0; i < j; i++) {
                        l2[i] = l1[k-1];
                        k--;
                    }
                    l2[i] = '\0';
                    i = 0;
                    j = 0;
                    insertNode(inExpLL,atoi(l2),OPERAND);
                    l1[0] = '\0';
                    l2[0] = '\0';
                }
            //note the precedence comparison
            while(isEmptyStack(s) == 0 && peek(s) != '(' && precedence(peek(s)) > precedence(c)){
                insertNode(inExpLL,peek(s),OPT);
                pop(&s);
            }
            push(&s,c);
        }
        count--;
    }

    // required for first operand
    if(j != 0) {
        k = j;
        for (i = 0; i < j; i++) {
            l2[i] = l1[k-1];
            k--;
        }
        l2[i] = '\0';
        i = 0;
        j = 0;          
        insertNode(inExpLL,atoi(l2),OPERAND);
        l1[0] = '\0';
        l2[0] = '\0';
    }

    while(isEmptyStack(s) == 0){
        insertNode(inExpLL,peek(s),OPT);
        pop(&s);
    }
}



void printExpLL(LinkedList inExpLL)
{
    ListNode* temp = NULL;
    temp = inExpLL.head;
    while(temp!= NULL){
        if(temp->type == OPERAND)
            printf(" %d ",temp->item);
        else
            printf(" %c ",(char)(temp->item));
        temp = temp->next;
    }
    printf("\n");
}

void insertNode(LinkedList *LLPtr, int item, enum ExpType type) {
    ListNode *newNode;
    newNode = malloc(sizeof(ListNode));
    if(newNode==NULL) exit(0);
    newNode->item = item;
    newNode->type = type;
    newNode->next = LLPtr->head;
    LLPtr->head=newNode;
    LLPtr->size++;
}

int deleteNode(LinkedList *LLPtr) {
    if(LLPtr==NULL || LLPtr->size==0){
        return 0;
    }
    else{
       ListNode *temp = LLPtr->head;
       LLPtr->head = LLPtr->head->next;

       free(temp);
       LLPtr->size--;
       return 1;
    }
}

int isEmptyLinkedList (LinkedList ll) {
    if(ll.size==0) return 1;
    else return 0;
}

void removeAllNodes(LinkedList *LLPtr)
{
	while(deleteNode(LLPtr));
}

void push(Stack *sPtr, char item){
    StackNode *newNode;
    newNode = malloc(sizeof(StackNode));
    newNode->item = item;
    newNode->next = sPtr->head;
    sPtr->head = newNode;
    sPtr->size++;
}

int pop(Stack *sPtr){
    if(sPtr == NULL || sPtr->head == NULL){
        return 0;
    }
    else{
       StackNode *temp = sPtr->head;
       sPtr->head = sPtr->head->next;
       free(temp);
       sPtr->size--;
       return 1;
    }
}

char peek(Stack s){
    return s.head->item;
}

int isEmptyStack(Stack s){
     if(s.size == 0) return 1;
     else return 0;
}
```