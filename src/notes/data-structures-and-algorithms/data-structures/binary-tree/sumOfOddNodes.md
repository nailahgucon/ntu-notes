---
title: Data Structures and Algorithms
pageTitle: sumOfOddNodes()
---

## sumOfOddNodes()

<span class="tags"><a href="#">Binary Tree</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write a recursive C function <span class="functions">sumOfOddNodes()</span> that accepts a pointer to the root node of a binary tree of integers and return the sum of all odd numbers in the tree.
<br><br>

**The function prototype is given as follows:**

<span class="functions">int sumOfOddNodes(BTNode *root);</span>
<br><br>
For example, for the given binary tree (11, 40, 35, 50, 80, 60, 85) in Figure 4, the sum of all the odd values is 131. The odd values are colored in <span style="color:red;">RED</span>.
<br><br>
<img src = "{{ '/images/binary-tree-sumofoddnodes.JPG' | url }}" class="diagrams">
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
2: Find the sum of all odd numbers in the binary tree.<br>
0: Quit;<br>
<br>
Please input your choice(1/2/0): 1<br>
Input an integer that you want to add to the binary tree. Any Alpha value will be treated as NULL.<br>
<br>
Enter an integer value for the root: 50<br>
Enter an integer value for the Left child of 50: 40<br>
Enter an integer value for the Right child of 50: 60<br>
Enter an integer value for the Left child of 40: 11<br>
Enter an integer value for the Right child of 40: 35<br>
Enter an integer value for the Left child of 11: a<br>
Enter an integer value for the Right child of 11: a<br>
Enter an integer value for the Left child of 35: a<br>
Enter an integer value for the Right child of 35: a<br>
<br>
Enter an integer value for the Left child of 60: 80<br>
Enter an integer value for the Right child of 60: 85<br>
Enter an integer value for the Left child of 80: b<br>
Enter an integer value for the Right child of 80: b<br>
Enter an integer value for the Left child of 85: b<br>
Enter an integer value for the Right child of 85: b<br>
The resulting binary tree is: 11 40 35 50 80 60 85<br>
<br>
Please input your choice(1/2/0): 2<br>
The sum of all odd numbers in the binary tree is: 131.<br>
<br>
Please input your choice(1/2/0):<br>
choice(1/2/0): 0
			</p>
		</div>
		<div class="modal-footer">
			<button id="closeModalBtn">Close</button>
		</div>
	</div>
</div>
<br>

```c
//////////////////////////////////////////////////////////////////////////////

#include <stdio.h>
#include <stdlib.h>

//////////////////////////////////////////////////////////////////////////////////

typedef struct _btnode
{
    int item;
    struct _btnode *left;
    struct _btnode *right;
} BTNode;   // You should not change the definition of BTNode

/////////////////////////////////////////////////////////////////////////////////

typedef struct _stackNode
{
    BTNode *btnode;
    struct _stackNode *next;
} StackNode;

typedef struct _stack
{
    StackNode *top;
} Stack;


///////////////////////// Function prototypes ////////////////////////////////////

// You should not change the prototypes of these functions
int sumOfOddNodes(BTNode *root);

BTNode *createBTNode(int item);

BTNode *createTree();
void push( Stack *stack, BTNode *node);
BTNode* pop(Stack *stack);

void printTree(BTNode *node);
void removeAll(BTNode **node);

///////////////////////////// main() /////////////////////////////////////////////

int main()
{
    char e;
    int c,oddValueCount;
    BTNode *root;

    c = 1;
    oddValueCount = 0;
    root = NULL;

    printf("1: Create a binary tree.\n");
    printf("2: Find the sum of all odd numbers in the binary tree.\n");
    printf("0: Quit;\n");

    while(c != 0)
    {
        printf("Please input your choice(1/2/0): ");
        if( scanf("%d",&c) > 0)
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
                oddValueCount = sumOfOddNodes(root);
                printf("The sum of all odd numbers in the binary tree is: %d.\n",oddValueCount);
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

int sumOfOddNodes(BTNode *node)

{
    //add your code here
    if(node == NULL)
        return 0;

    // if it's odd, add node item
    if(node->item % 2 != 0)
        return sumOfOddNodes(node->left) + sumOfOddNodes(node->right) + node->item;
    // if it's even, no change
    else
        return sumOfOddNodes(node->left) + sumOfOddNodes(node->right);
}

//////////////////////////////////////////////////////////////////////////////////

BTNode *createBTNode(int item)
{
    BTNode *newNode = malloc(sizeof(BTNode));
    newNode->item = item;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

//////////////////////////////////////////////////////////////////////////////////


BTNode *createTree()
{
    Stack stack;
    BTNode *root, *temp;
    char s;
    int item;

    stack.top = NULL;
    root = NULL;
    printf("Input an integer that you want to add to the binary tree. Any Alpha value will be treated as NULL.\n");
    printf("Enter an integer value for the root: ");
    if(scanf("%d",&item) > 0)
    {
        root = createBTNode(item);
        push(&stack,root);
    }
    else
    {
        scanf("%c",&s);
    }

    while((temp =pop(&stack)) != NULL)
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
            push(&stack,temp->right);
        if(temp->left != NULL)
            push(&stack,temp->left);
    }
    return root;
}

void push( Stack *stack, BTNode *node)
{
    StackNode *temp;

    temp = malloc(sizeof(StackNode));
    if(temp == NULL)
        return;
    temp->btnode = node;
    if(stack->top == NULL)
    {
        stack->top = temp;
        temp->next = NULL;
    }
    else
    {
        temp->next = stack->top;
        stack->top = temp;
    }
}

BTNode* pop(Stack *stack)
{
    StackNode *temp, *top;
    BTNode *ptr;
    ptr = NULL;

    top = stack->top;
    if(top != NULL)
    {
        temp = top->next;
        ptr = top->btnode;

        stack->top = temp;
        free(top);
        top = NULL;
    }
    return ptr;
}

void printTree(BTNode *node)
{
    if(node == NULL) return;

    printTree(node->left);
    printf("%d ",node->item);
    printTree(node->right);
}

void removeAll(BTNode **node)
{
    if(*node != NULL)
    {
        removeAll(&((*node)->left));
        removeAll(&((*node)->right));
        free(*node);
        *node = NULL;
    }
}
```

