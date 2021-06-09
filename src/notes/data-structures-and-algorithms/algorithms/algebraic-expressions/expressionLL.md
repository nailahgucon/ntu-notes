---
title: Data Structures and Algorithms
pageTitle: expressionLL()
---

## expressionLL()

<span class="tags"><a href="#">Algebraic Expressions</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Given a character string of integer arithmetic expression, write a function, <span class="functions">expressionLL()</span> to split the operands and operators into a linked list. We assumed that the character string only contains digits, operators (`+', `-', `*' and `/') and parentheses.
<br><br>

**The structure of LinkedList is given below. type is used to indicate the item is an operator or an operand:**

<span class="functions">
enum ExpType {OPT , OPERAND }; // OPT : OPERATOR <br>
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
void insertNode ( LinkedList *llPtr , int item , enum ExpType type );<br>
int deleteNode ( LinkedList * llPtr );<br>
void removeAllNodes ( LinkedList * llPtr );<br>
int isEmptyLinkedList ( LinkedList ll);
</span>
<br><br>

**The function prototype is given as follows:**

<span class="functions">void expressionLL ( char * infix , LinkedListExp * inExpLL );</span>
<br><br>
For verification purpose, the <span class="functions">printExpLL()</span> will print all operands after adding a seed number.
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
Input:<br>
1+11*111/(1111-88)<br>
7 (seed number)<br>
<br>
Output:<br>
8 + 18 * 118 / ( 1118 - 95 )
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

void insertNode(LinkedList *llPtr, int item, enum ExpType type);
int deleteNode(LinkedList *llPtr);
void removeAllNodes(LinkedList *llPtr);
int isEmptyLinkedList (LinkedList ll);

void expressionLL(char* infix, LinkedList *inExpLL);

void printExpLL(LinkedList inExpQ, int seed);

int main()
{
    char infix[SIZE];

    //printf("Enter an infix expression:\n");
    gets(infix);

    LinkedList inExpLL;
    inExpLL.head = NULL;
    inExpLL.size = 0;

    expressionLL(infix, &inExpLL);

    int seed;
    //printf("Enter a seed: \n");
    scanf("%d",&seed);
    printExpLL(inExpLL,seed);

    removeAllNodes(&inExpLL);
    return 0;
}


void expressionLL(char* infix, LinkedList *inExpLL)
{
 //Write your code here
char current, temp;
char list[100];
int actualSize, value;
int i = 0;
int j = 0;
int size = 0;
int index = 0;

// count char in infix
while (infix[i] != '\0')
    i++;

i = i - 1;

while (i >= 0){
    current = infix[i];
    if(current == '+' || current == '-' || current == '*' || current == '/' || current == '(' || current == ')'){
        //need to reverse the array
        if(size != 0) {
            actualSize = size;
            while (j < size && size > 1) {
                temp = list[j];
                list[j] = list[size-1];
                list[size-1] = temp;
                j++;
                size--;
            }
            list[actualSize] = '\0';
            insertNode(inExpLL, atoi(list), OPERAND);
        }

        insertNode(inExpLL,current,OPT);
        size = 0;
        index = 0;
        list[0] = '\0';
    }
    else{
        list[index] = infix[i];
        size++;
        index++;
    }
    i--;
    j = 0;
}

if(index != 0) {
    actualSize = size;
    while (j < size && size > 1) {
                temp = list[j];
                list[j] = list[size-1];
                list[size-1] = temp;
                j++;
                size--;
    }
    list[actualSize] = '\0';
    insertNode(inExpLL, atoi(list), OPERAND);
}
// covert str to int using atoi
while(list[index] != '\0') {
    value = atoi(&list[index]);
    insertNode(inExpLL, value, OPERAND);
    index++;
}

}

void printExpLL(LinkedList inExpLL, int seed)
{
    ListNode* temp = NULL;
    temp = inExpLL.head;
    while(temp!= NULL){
        if(temp->type == OPERAND)
            printf(" %d ",temp->item+ seed);
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
    if(LLPtr==NULL || LLPtr->size==0){ //Queue is empty or NULL pointer
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
```

