---
title: Data Structures and Algorithms
pageTitle: maxDepth()
---

## maxDepth()

<span class="tags"><a href="#">Binary Tree</a></span>
<span class="tags"><a href="#">Tutorial</a></span>

<hr>

Write a c function to find the maximum depth of a binary tree.
<br><br>
<img src = "{{ '/images/binary-tree-maxdepth.JPG' | url }}" class="diagrams">
<br><br>
**The function prototype is given as follows:**

<span class="functions">int maxDepth(BTNode *node);</span>
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
1: Create a binary tree.<br>
2: Find the maximum depth of the binary tree.<br>
0: Quit;<br>
<br>
Please input your choice(1/2/0): 1<br>
Input an integer that you want to add to the binary tree. Any Alpha value will be treated as NULL.<br>
<br>
Enter an integer value for the root: 50<br>
Enter an integer value for the Left child of 50: 20<br>
Enter an integer value for the Right child of 50: 60<br>
Enter an integer value for the Left child of 20: 10<br>
Enter an integer value for the Right child of 20: 30<br>
Enter an integer value for the Left child of 10: a<br>
Enter an integer value for the Right child of 10: a<br>
Enter an integer value for the Left child of 30: 55<br>
Enter an integer value for the Right child of 30: a<br>
Enter an integer value for the Left child of 55: a<br>
Enter an integer value for the Right child of 55: a<br>
Enter an integer value for the Left child of 60: a<br>
Enter an integer value for the Right child of 60: 80<br>
Enter an integer value for the Left child of 80: a<br>
Enter an integer value for the Right child of 80: a<br>
The resulting binary tree is: 10 20 55 30 50 60 80<br>
<br>
Please input your choice(1/2/0): 2<br>
Find the maximum depth of the binary tree: 3<br>
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
//////////////////////////////////////////////////////////////////////////////////

#include <stdio.h>
#include <stdlib.h>

//////////////////////////////////////////////////////////////////////////////////
typedef struct _btnode{
	int item;
	struct _btnode *left;
	struct _btnode *right;
} BTNode;   // You should not change the definition of BTNode

/////////////////////////////////////////////////////////////////////////////////

typedef struct _stackNode{
    BTNode *btnode;
    struct _stackNode *next;
}StackNode;

typedef struct _stack{
    StackNode *top;
}Stack;

///////////////////////// function prototypes ////////////////////////////////////

// You should not change the prototypes of these functions
int maxDepth(BTNode *node);

BTNode *createBTNode(int item);

BTNode *createTree();
void push( Stack *stk, BTNode *node);
BTNode* pop(Stack *stk);

void printTree(BTNode *node);
void removeAll(BTNode **node);

///////////////////////////// main() /////////////////////////////////////////////

int main()
{
    int c;
    char e;
	c = 1;

    BTNode *root;
    root = NULL;

    printf("1: Create a binary tree.\n");
    printf("2: Find the maximum depth of the binary tree.\n");
    printf("0: Quit;\n");

    while(c != 0){
        printf("\nPlease input your choice(1/2/0): ");
        if(scanf("%d", &c) > 0)
        {
            switch(c)
            {
            case 1:
                removeAll(&root);
                root = createTree();
                printf("The resulting binary tree is: ");
                printTree(root);
                printf("\n");
                break;
            case 2:
                c = maxDepth(root);
                printf("The maximum depth of the binary tree is: %d\n",c);
                removeAll(&root);
                break;
            case 0:
                removeAll(&root);
                break;
            default:
                printf("Choice unknown;\n");
                break;
            }
		}
        else
        {
            scanf("%c",&e);
        }

    }

    return 0;
}

//////////////////////////////////////////////////////////////////////////////////

int maxDepth(BTNode *node)
{
    if(node == NULL){
        return -1;
    }
    else{
        int ldepth = maxDepth(node->left);
        int rdepth = maxDepth(node->right);

        if(ldepth > rdepth) return ldepth+1;
        else{
            return rdepth+1;
        }
    }

}

///////////////////////////////////////////////////////////////////////////////////

BTNode *createBTNode(int item){
    BTNode *newNode = malloc(sizeof(BTNode));
    newNode->item = item;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}


//////////////////////////////////////////////////////////////////////////////////

BTNode *createTree()
{
    Stack stk;
    BTNode *root, *temp;
    char s;
    int item;

    stk.top = NULL;
    root = NULL;

    printf("Input an integer that you want to add to the binary tree. Any Alpha value will be treated as NULL.\n");
    printf("Enter an integer value for the root: ");
    if(scanf("%d",&item) > 0)
    {
        root = createBTNode(item);
        push(&stk,root);
    }
    else
    {
        scanf("%c",&s);
    }

    while((temp =pop(&stk)) != NULL)
    {

        printf("Enter an integer value for the Left child of %d: ", temp->item);

        if(scanf("%d",&item)> 0)
        {
            temp->left = createBTNode(item);
        }
        else
        {
            scanf("%c",&s);
        }

        printf("Enter an integer value for the Right child of %d: ", temp->item);
        if(scanf("%d",&item)>0)
        {
            temp->right = createBTNode(item);
        }
        else
        {
            scanf("%c",&s);
        }

        if(temp->right != NULL)
            push(&stk,temp->right);
        if(temp->left != NULL)
            push(&stk,temp->left);
    }
    return root;
}

void push( Stack *stk, BTNode *node){
    StackNode *temp;

    temp = malloc(sizeof(StackNode));
    if(temp == NULL)
        return;
    temp->btnode = node;
    if(stk->top == NULL){
        stk->top = temp;
        temp->next = NULL;
    }
    else{
        temp->next = stk->top;
        stk->top = temp;
    }
}

BTNode* pop(Stack *stk){
   StackNode *temp, *top;
   BTNode *ptr;
   ptr = NULL;

   top = stk->top;
   if(top != NULL){
        temp = top->next;
        ptr = top->btnode;

        stk->top = temp;
        free(top);
        top = NULL;
   }
   return ptr;
}

void printTree(BTNode *node){
    if(node == NULL) return;

    printTree(node->left);
    printf("%d ",node->item);
    printTree(node->right);
}

void removeAll(BTNode **node){
    if(*node != NULL){
        removeAll(&((*node)->left));
        removeAll(&((*node)->right));
        free(*node);
        *node = NULL;
    }
}

```

