---
title: Data Structures and Algorithms
pageTitle: inOrderIterative()
---

## inOrderIterative()

<span class="tags"><a href="#">Binary Search Tree</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write an iterative C function <span class="functions">inOrderIterative()</span> that prints the inorder traversal of a binary search tree using a stack. Note that you should **only** use <span class="functions">push()</span> or <span class="functions">pop()</span> operations when you add or remove integers from the stack. Remember to empty the stack at the beginning, if the stack is not empty.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void inOrderIterative(BSTNode *root);</span>
<br><br>
**Following is the detailed algorithm:**

<span class="functions">
1) Create an empty stack S.<br>
2) Initialize current node as root.<br>
3) Push the current node to S and set current = current->left until current is NULL<br>
4) If current is NULL and stack is not empty then<br>
&nbsp;&nbsp;&nbsp;&nbsp;a) Pop the top item from stack<br>
&nbsp;&nbsp;&nbsp;&nbsp;b) Print the popped item, set current = popped_item->right<br>
&nbsp;&nbsp;&nbsp;&nbsp;c) Go to step 3.<br>
5) If current is NULL and stack is empty then you are done
</span>
<br><br>

**Let us consider the below tree for example.**<br>
<img src = "{{ '/images/binary-search-tree-inorderiterative.JPG' | url }}" class="diagrams">
<br><br>
Iterative Inorder Tree Traversal: **10 15 18 20 50**
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
1: Insert an integer into the binary search tree;<br>
2: Print the in-order traversal of the binary search tree;<br>
0: Quit;<br>
<br>
Please input your choice(1/2/0): 1<br>
Input an integer that you want to insert into the Binary Search Tree: 20<br>
Please input your choice(1/2/0): 1<br>
Input an integer that you want to insert into the Binary Search Tree: 15<br>
Please input your choice(1/2/0): 1<br>
Input an integer that you want to insert into the Binary Search Tree: 50<br>
Please input your choice(1/2/0): 1<br>
Input an integer that you want to insert into the Binary Search Tree: 10<br>
Please input your choice(1/2/0): 1<br>
Input an integer that you want to insert into the Binary Search Tree: 18<br>
Please input your choice(1/2/0): 2<br>
<br>
The resulting in-order traversal of the binary search tree is: 10 15 18 20 50<br>
<br>
Please input your choice(1/2/0):
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

typedef struct _bstnode{
	int item;
	struct _bstnode *left;
	struct _bstnode *right;
} BSTNode;   // You should not change the definition of BSTNode

typedef struct _stackNode{
	BSTNode *data;
	struct _stackNode *next;
}StackNode; // You should not change the definition of StackNode

typedef struct _stack
{
	StackNode *top;
}Stack; // You should not change the definition of Stack

///////////////////////// function prototypes ////////////////////////////////////

// You should not change the prototypes of these functions
void inOrderIterative(BSTNode *root);

void insertBSTNode(BSTNode **node, int value);

void push(Stack *stack, BSTNode *node);
BSTNode *pop(Stack *s);
BSTNode *peek(Stack *s);
int isEmpty(Stack *s);
void removeAll(BSTNode **node);

///////////////////////////// main() /////////////////////////////////////////////

int main()
{
	int c, i;
	c = 1;

	//Initialize the Binary Search Tree as an empty Binary Search Tree
	BSTNode *root;
	root = NULL;

	printf("1: Insert an integer into the binary search tree;\n");
	printf("2: Print the in-order traversal of the binary search tree;\n");
	printf("0: Quit;\n");


	while (c != 0)
	{
		printf("Please input your choice(1/2/0): ");
		scanf("%d", &c);

		switch (c)
		{
		case 1:
			printf("Input an integer that you want to insert into the Binary Search Tree: ");
			scanf("%d", &i);
			insertBSTNode(&root, i);
			break;
		case 2:
			printf("The resulting in-order traversal of the binary search tree is: ");
			inOrderIterative(root); // You need to code this function
			printf("\n");
			break;
		case 0:
			removeAll(&root);
			break;
		default:
			printf("Choice unknown;\n");
			break;
		}

	}

	return 0;
}

//////////////////////////////////////////////////////////////////////////////////

void inOrderIterative(BSTNode *root)
{
	// add your code here
	Stack s;
	 s.top = NULL;
	 BSTNode *temp;
	 temp = root;

	 //if not empty tree
	 if (temp!=NULL){
        while (1){//infinite loop or replace by a do while loop
            if (temp!=NULL){
                push(&s,temp);
                temp= temp->left;
            }
            else{//temp is null
                if (!isEmpty(&s)){
                    temp = pop(&s);
                    printf("%d ",temp->item);
                    temp = temp->right;
                }
                else
                    break;
            }
        }
	 }
}

///////////////////////////////////////////////////////////////////////////////

void insertBSTNode(BSTNode **node, int value){
	if (*node == NULL)
	{
		*node = malloc(sizeof(BSTNode));

		if (*node != NULL) {
			(*node)->item = value;
			(*node)->left = NULL;
			(*node)->right = NULL;
		}
	}
	else
	{
		if (value < (*node)->item)
		{
			insertBSTNode(&((*node)->left), value);
		}
		else if (value >(*node)->item)
		{
			insertBSTNode(&((*node)->right), value);
		}
		else
			return;
	}
}

//////////////////////////////////////////////////////////////////////////////////

void push(Stack *stack, BSTNode * node)
{
	StackNode *temp;

	temp = malloc(sizeof(StackNode));

	if (temp == NULL)
		return;
	temp->data = node;

	if (stack->top == NULL)
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

BSTNode * pop(Stack * s)
{
	StackNode *temp, *t;
	BSTNode * ptr;
	ptr = NULL;

	t = s->top;
	if (t != NULL)
	{
		temp = t->next;
		ptr = t->data;

		s->top = temp;
		free(t);
		t = NULL;
	}

	return ptr;
}

BSTNode * peek(Stack * s)
{
	StackNode *temp;
	temp = s->top;
	if (temp != NULL)
		return temp->data;
	else
		return NULL;
}

int isEmpty(Stack *s)
{
	if (s->top == NULL)
		return 1;
	else
		return 0;
}


void removeAll(BSTNode **node)
{
	if (*node != NULL)
	{
		removeAll(&((*node)->left));
		removeAll(&((*node)->right));
		free(*node);
		*node = NULL;
	}
}

```

