---
title: Data Structures and Algorithms
pageTitle: exePostfix()
---

## exePostfix()

<span class="tags"><a href="#">Algebraic Expressions</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a C program to evaluate a postfix expression. You may assume that operands are single-digit numbers.
<br><br>

**The function prototype is given as follows:**

<span class="functions">double exePostfix( char * postfix );</span>
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
1. Input: 987-654-/3+*+<br>
Output: 18.00<br>
<br>
2. Input: 25+89/9*7*+<br>
Output: 63.00<br>
<br>
3. Input: 88/8*77+7+5*6*-<br>
Output: -622.00
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

#define SIZE 80 //The limit of expression length

typedef struct _stackNode{
    double item;
    struct _stackNode *next;
}StackNode;

typedef struct _stack{
   int size;
   StackNode *head;
}Stack;

void push(Stack *sPtr, double item);
int pop(Stack *sPtr);
double peek(Stack s);
int isEmptyStack(Stack s);

double exePostfix(char*);

int main()
{
    char postfix[SIZE];

    printf("Enter a postfix expression:\n");
    gets(postfix);

    printf("The answer is %.2lf.\n",exePostfix(postfix));

    return 0;
}


double exePostfix(char* postfix)
{
    Stack s;
    s.head = NULL;
    s.size = 0;

    int i=0;
    double op1, op2;
    char c;
    double result;
    while(postfix[i]!='\0')
    {
        c = postfix[i++];
        if(c=='*' || c=='/' || c=='+' || c=='-')
        {

            op1 = peek(s); pop(&s);
            op2 = peek(s); pop(&s);

            switch(c)
            {
            case '*':
                push(&s, op2*op1);
                break;
            case '/':
                push(&s, op2/op1);
                break;
            case '+':
                push(&s, op2+op1);
                break;
            case '-':
                push(&s, op2-op1);
            }
        }
        else
            push(&s, (c-'0')) ;

    }

   result = peek(s); pop(&s);
   return result;

}

void push(Stack *sPtr, double item){
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

double peek(Stack s){
    return s.head->item;
}

int isEmptyStack(Stack s){
     if(s.size == 0) return 1;
     else return 0;
}

```