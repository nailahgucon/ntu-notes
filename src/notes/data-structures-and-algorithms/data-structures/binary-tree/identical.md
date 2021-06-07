---
title: Data Structures and Algorithms
pageTitle: identical()
---

## identical()

<span class="tags"><a href="#">Binary Tree</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write a recursive C function <span class="functions">identical()</span> to determine whether two binary trees are structurally identical, assuming the two binary trees as <span class="functions">tree1</span> and <span class="functions">tree2</span>. This function returns 1 if two binary trees are structurally identical; otherwise, it returns 0. Note that two binary trees are structurally identical if they are both empty or if they are both non-empty and the left and the right subtrees are similar **(they are made of nodes with the same values and arranged in the same way)**.
<br><br>

**The function prototype is given as follows:**

<span class="functions">int identical(BTNode *tree1, BTNode *tree2);</span>
<br><br>
For example, if the given two trees are tree 1 (1, 3, 2, 5, 4, 7, 8) and tree 2 (1, 3, 2, 5, 4, 7, 8), as shown in Figure 1, then, tree 1 and tree 2 are **structurally identical**.
<br><br>
<img src = "{{ '/images/binary-tree-identical.JPG' | url }}" class="diagrams">
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
            1: Create a binary tree1.<br>
            2: Create a binary tree2.<br>
            3: Check whether two trees are structurally identical.<br>
            0: Quit;<br>
            <br>
            Please input your choice(1/2/3/0): 1<br>
            <br>
            Creating tree1:<br>
            Input an integer that you want to add to the binary tree. Any Alpha value will be treated as NULL.<br>
            <br>
            Enter an integer value for the root: 5<br>
            Enter an integer value for the Left child of 5: 3<br>
            Enter an integer value for the Right child of 5: 7<br>
            Enter an integer value for the Left child of 3: 1<br>
            Enter an integer value for the Right child of 3: 2<br>
            Enter an integer value for the Left child of 1: a<br>
            Enter an integer value for the Right child of 1: a<br>
            Enter an integer value for the Left child of 2: a<br>
            Enter an integer value for the Right child of 2: a<br>
            Enter an integer value for the Left child of 7: 4<br>
            Enter an integer value for the Right child of 7: 8<br>
            Enter an integer value for the Left child of 4: a<br>
            Enter an integer value for the Right child of 4: a<br>
            Enter an integer value for the Left child of 8: a<br>
            Enter an integer value for the Right child of 8: a<br>
            The resulting tree1 is: 1 3 2 5 4 7 8<br>
            Please input your choice(1/2/3/0): 2<br>
            <br>
            Creating tree2:<br>
            Input an integer that you want to add to the binary tree. Any Alpha value will be treated as NULL.<br>
            <br>
            Enter an integer value for the root: 5<br>
            Enter an integer value for the Left child of 5: 3<br>
            Enter an integer value for the Right child of 5: 7<br>
            Enter an integer value for the Left child of 3: 1<br>
            Enter an integer value for the Right child of 3: 2<br>
            Enter an integer value for the Left child of 1: a<br>
            Enter an integer value for the Right child of 1: a<br>
            Enter an integer value for the Left child of 2: a<br>
            Enter an integer value for the Right child of 2: a<br>
            Enter an integer value for the Left child of 7: 4<br>
            Enter an integer value for the Right child of 7: 8<br>
            Enter an integer value for the Left child of 4: a<br>
            Enter an integer value for the Right child of 4: a<br>
            Enter an integer value for the Left child of 8: a<br>
            Enter an integer value for the Right child of 8: a<br>
            The resulting tree2 is: 1 3 2 5 4 7 8<br>
            <br>
            Please input your choice(1/2/3/0): 3<br>
            Both trees are structurally identical.<br>
            <br>
            Please input your choice(1/2/3/0): 0
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
int identical(BTNode *tree1, BTNode *tree2);

BTNode* createBTNode(int item);

BTNode* createTree();
void push( Stack *stk, BTNode *node);
BTNode* pop(Stack *stk);

void printTree(BTNode *node);
void removeAll(BTNode **node);

///////////////////////////// main() /////////////////////////////////////////////

int main()
{
    int c, s;
    char e;
    BTNode *root1, *root2;

    root1 = NULL;
    root2 = NULL;
    c = 1;

    printf("1: Create a binary tree1.\n");
    printf("2: Create a binary tree2.\n");
    printf("3: Check whether two trees are structurally identical.\n");
    printf("0: Quit;\n");

    while(c != 0){
        printf("Please input your choice(1/2/3/0): ");
        if(scanf("%d", &c) > 0)

        {

            switch(c)
            {
            case 1:
                removeAll(&root1);
                printf("Creating tree1:\n");
                root1 = createTree();
                printf("The resulting tree1 is: ");
                printTree(root1);
                printf("\n");
                break;
            case 2:
                removeAll(&root2);
                printf("Creating tree2:\n");
                root2 = createTree();
                printf("The resulting tree2 is: ");
                printTree(root2);
                printf("\n");
                break;
            case 3:
                s = identical(root1, root2);
                if(s){
                printf("Both trees are structurally identical.\n");
                }
                else{
                printf("Both trees are different.\n");
                }
                removeAll(&root1);
                removeAll(&root2);
                break;
            case 0:
                removeAll(&root1);
                removeAll(&root2);
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

int identical(BTNode *tree1, BTNode *tree2){
   // add your code here
   // structurally identical (returns 1): tree1 & tree2 both NULL (case 1) 
   // OR 
   // tree1 & tree2 not NULL and tree1 & tree2 subtrees are similar (case 2)
   // otherwise, not structurally identical (returns 0)

   // case 1 of structurally identical
   if (tree1 == NULL && tree2 == NULL)
        return 1;
   else{
        // check case 2 of structurally identical
        if (tree1!=NULL && tree2 != NULL)  { // both not empty
            // check current node first            
            if (tree1->item != tree2->item)
                return 0;

            //// go to the left and right to check
            //// == 0: not structurally identical
            if (identical(tree1->left,tree2->left) == 0) 
                return 0; // if left handside is different, return 0
            if (identical(tree1->right,tree2->right) == 0) 
                return 0; //same goes for right side

            // current node, left and right is all the same -> structurally identical
            return 1; 
        }
        // case 2 already failed cause both is not non-empty, thus return 0
        else{
            return 0;
        } // end of small else
        } // end of big else
}

/////////////////////////////////////////////////////////////////////////////////

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
