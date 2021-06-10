---
title: Data Structures and Algorithms
pageTitle: in2Post()
---

## in2Post()

<span class="tags"><a href="#">Algebraic Expressions</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a C program to convert an infix expression to a postfix expression. The input and the output of the function are character strings. The input expression contains only four possible operators: +, -, * and /. Operands can be any alphanumeric. Each operand is represented by a character symbol. The parentheses are allowed in the input expression. You may assume that the expression is always valid.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void in2Post( char * infix , char * postfix );</span>
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
1. Infix: (A+B)+(C-D)<br>
Postfix: AB+CD-+<br>
<br>
2. Infix: a+b*c-d*(e/f)<br>
Postfix: abc*+def/*-<br>
<br>
3. Infix: 9+(8-7)*(6/(5-4)+3)<br>
Postfix: 987-654-/3+*+
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

void in2Post(char*, char*);
int precedence(char);

int main()
{
    char infix[SIZE];
    char postfix[SIZE];

    printf("Enter an infix expression:\n");
    gets(infix);

    in2Post(infix,postfix);
    printf("The postfix expression is \n");
    printf("%s\n",postfix);
    return 0;
}

void in2Post(char* infix, char* postfix)
{
    Stack s;
    s.head = NULL;
    s.size = 0;

    int i = 0;
    int j = 0;
    char c;

    while(i<SIZE && infix[i]!='\0')
    {
        c = infix[i++];
        switch(c)
        {
        case '*': //operators
        case '/':
        case '+':
        case '-':
            while(isEmptyStack(s)==0 && peek(s) != '(' && precedence(peek(s)) >= precedence(c) )
            {
                postfix[j++] = peek(s);
                pop(&s);
            }
            push(&s,c);
            break;
        case '(':
            push(&s,c);
            break;
        case ')':
            while(isEmptyStack(s)==0)
            {
                if(peek(s)!='(')
                {
                    postfix[j++]=peek(s);
                    pop(&s);
                }
                else
                {
                    pop(&s);
                    break;
                }
            }
            break;
        default: //operand
            postfix[j++] = c;
        }
    }

    while(isEmptyStack(s)==0)
    {
        postfix[j++] = peek(s);
        pop(&s);
    }
    postfix[j] = '\0';
}

int precedence(char op)
{
    if(op == '*' || op == '/')
        return 1;
    else return 0;
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