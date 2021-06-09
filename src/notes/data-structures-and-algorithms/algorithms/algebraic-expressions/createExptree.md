---
title: Data Structures and Algorithms
pageTitle: createExptree()
---

## createExptree()

<span class="tags"><a href="#">Algebraic Expressions</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write a function, <span class="functions">createExptree()</span> to create an expression tree structure by using a prefix expression. Each element (operands, operators, parenthese) in the prefix expression is seperated by a white space.
<br><br>

**You may need the following tree structure:**

<span class="functions">
typedef struct _btnode {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int item;<br>
&nbsp;&nbsp;&nbsp;&nbsp;struct _btnode *left;<br>
&nbsp;&nbsp;&nbsp;&nbsp;struct _btnode *right;<br>
} BTNode;
</span>
<br><br>
Next, the function will insert each operator in the given expression into the tree as an internal node and each operand is inserted as a leaf node. See example below.<br>
Write another two functions, <span class="functions">printTree()</span> and <span class="functions">printTreePostfix()</span>, to print all tree nodes by in-order and post-order traversal, respectively. For your information, the in-order traversal result should be same as the original infix expression. The post-order traversal will move operator "to the back". It is known as postfix notation or Reverse Polish notation invented by Jan Lukasiewicz in 1924. For example, infix expression: a+b*c-d &#8658; postfix notation: a b c * + d -.<br>
Lastly, write an expression evaluation function, <span class="functions">computeTree()</span> to calculate the given arithmetic expression.<br><br>

**The function prototype is given as follows:**

<span class="functions">
void createExpTree ( BTNode ** root , char * prefix );<br>
void printTree ( BTNode * node );<br>
void printTreePostfix ( BTNode * node );<br>
double computeTree ( BTNode * node );
</span>
<br><br>
<img src = "{{ '/images/algebraic-expressions-createexptree.JPG' | url }}" class="diagrams">
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
Input: <br>
+ 99 * - 88 77 + / 66 - 55 44 33<br>
Output:<br>
99 + 88 - 77 * 66 / 55 - 44 + 33<br>
99 88 77 - 66 55 44 - / 33 + * +<br>
528.00<br>
<br>
where the first row is the infix expression (the parentheses are ignored here), the second row is the postfix expression and the last row is the evaluation answer.
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
#include <string.h>

#define SIZE 200 //The number digit limitation

typedef struct _btnode{
	int item;
	struct _btnode *left;
	struct _btnode *right;
} BTNode;   // You should not change the definition of BTNode

typedef struct _node{
     BTNode* item;
     struct _node *next;
}StackNode;

typedef struct _stack{
   int size;
   StackNode *head;
}Stack;

void deleteTree(BTNode **root);

void createExpTree(BTNode** root,char* prefix);
void printTree(BTNode *node);
void printTreePostfix(BTNode *node);
double computeTree(BTNode *node);

void push(Stack *sPtr,  BTNode* item);
int pop(Stack *sPtr);
BTNode *peek(Stack s);
int isEmptyStack(Stack s);

int main()
{
    char prefix[SIZE];
    BTNode* root=NULL;

    //printf("Enter an prefix expression:\n");
    gets(prefix);

    createExpTree(&root, prefix);

    // printf("The Infix Expression:\n");
    printTree(root);
    printf("\n");
    //printf("The Postfix (Reverse Polish) Expression:\n");
    printTreePostfix(root);
    printf("\n");
    //printf("Answer ");
    printf("%.2f\n", computeTree(root));
    deleteTree(&root);
    return 0;
}

void createExpTree(BTNode** root,char* prefix)
{
    Stack s;
    s.head = NULL;
    s.size = 0;

    BTNode *op1, *op2;
    char l1[SIZE], l2[SIZE];
    char c;
    int count = 0;
    int i = 0;
    int j = 0;
    int k = 0;

    // count char in prefix
     while (prefix[count] != '\0')
        count++;
     count -= 1;

    while(count >= 0) {   
        c = prefix[count];
        if(c >= '0' && c <= '9') {
            l1[i] = c;
            i++;
        // need to check for spacing as well
        } else if (c == ' ') {
            if(i != 0) {
                    k = i;
                    for (j = 0; j < i; j++) {
                        // l2[j] = l1[k--];
                        l2[j] = l1[k-1];
                        k--;
                    }
                        l2[j] = '\0';
                        j = 0;
                        i = 0;
                        
                        // allocate memory with malloc
                        BTNode *node = (BTNode *)malloc(sizeof(BTNode));
                        // need to used atoi
                        node->left=NULL;
                        node->right=NULL;
                        node->item=atoi(l2);
                        // assign node to root
                        *root = node;
                        // push into stack
                        push(&s,*root);
                        l1[0] = '\0';
                        l2[0] = '\0';
                }
        
        } else {
            // operator nodes
            BTNode *nodeOPT = (BTNode *)malloc(sizeof(BTNode));
            nodeOPT->left = NULL;
            nodeOPT->right = NULL;
            nodeOPT->item = c;

            if(!isEmptyStack(s)) {
                op1 = peek(s);
                // printf("%c", peek(s));
                nodeOPT->left = op1;
                pop(&s);

                if(peek(s) != NULL) {
                    op2 = peek(s);
                    // printf("%c", peek(s));
                    nodeOPT->right = op2;
                    pop(&s);    
                }
            }
            *root = nodeOPT;
            push(&s,*root);            
        }
        count--;
    }

}

void printTree(BTNode *node){
    if(node!=NULL) {
        if(node->left!=NULL)
            printTree(node->left);
        
        if(node->item == '+' || node->item == '/' || node->item == '*' || node->item == '-' ) {
            printf("%c ",node->item);
        } else {
            printf("%d ",node->item);
        }

        if(node->right!=NULL)
            printTree(node->right);
    }
}


void printTreePostfix(BTNode *node){
   //Write your code here
   if(node != NULL) {
       if(node->left != NULL)
          printTreePostfix(node->left);
       
       if(node->right != NULL)
          printTreePostfix(node->right);
        
        // check for operators
        if(node->item == '+' || node->item == '/' || node->item == '*' || node->item == '-' ) {
            printf("%c ",node->item);
        } else {
            printf("%d ",node->item);
        }
   }

}

double computeTree(BTNode *node){

    double left, right;
    
    if(node != NULL) {
        if(node->left == NULL && node->right == NULL) {
            return node->item;
        }
        // traversal
        left = computeTree(node->left);
        right = computeTree(node->right);

        switch(node->item) {
            case '+':
                return left + right;
            case '-':
                return left - right;
            case '*':
                return left * right;
            default:
                return left / right;
        }
    } else {
        return 0;
    }
}

void push(Stack *sPtr, BTNode *item){
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

BTNode *peek(Stack s){
    return s.head->item;
}

int isEmptyStack(Stack s){
     if(s.size == 0) return 1;
     else return 0;
}

void deleteTree(BTNode **root){
    BTNode* temp;
    if(*root !=NULL)
    {
        temp = (*root)->right;
        deleteTree(&((*root)->left));
        free(*root);
        *root = NULL;
        deleteTree(&temp);
    }
}
```