---
title: Data Structures and Algorithms
pageTitle: preOrderIterative()
---

## preOrderIterative()

<span class="tags"><a href="#">Binary Search Tree</a></span>
<span class="tags"><a href="#">Tutorial</a></span>

<hr>

Write an iterative C function <span class="functions">preOrderIterative()</span> that prints the pre-order traversal of a binary search tree using a **stack**. Note that you should **only** use <span class="functions">push()</span> or <span class="functions">pop()</span> operations when you add or remove integers from the stack. Remember to empty the stack at the beginning, if the stack is not empty.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void preOrderIterative(BSTNode *root);</span>
<br><br>

**Following is the detailed algorithm:**

<span class="functions">
1) Create an empty stack nodeStack and push root node to stack.<br>
2) Do following while nodeStack is not empty.<br>
&nbsp;&nbsp;&nbsp;&nbsp;a) Pop an item from stack and print it.<br>
&nbsp;&nbsp;&nbsp;&nbsp;b) Push right child of popped item to stack<br>
&nbsp;&nbsp;&nbsp;&nbsp;c) Push left child of popped item to stack<br>
<br>
&nbsp;&nbsp;Right child is pushed before left child to make sure that left subtree is processed first.
</span>
<br><br>
<img src = "{{ '/images/binary-tree-preorderiterative.JPG' | url }}" class="diagrams">
<br><br>

Preorder Tree Traversal: **20 15 10 18 50 25 80**

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
void preOrderIterative(BSTNode *root);

void insertBSTNode(BSTNode **node, int value);

// You may use the following functions or you may write your own
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
	BSTNode * root;
	root = NULL;

	printf("1: Insert an integer into the binary search tree;\n");
	printf("2: Print the pre-order traversal of the binary search tree;\n");
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
			printf("The resulting pre-order traversal of the binary search tree is: ");
			preOrderIterative(root); // You need to code this function
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

void preOrderIterative(BSTNode *root)
{
	Stack s;
	BSTNode *temp;

	s.top = NULL;
	temp = root;

	if (temp == NULL)
		return;
    push(&s, temp);

	do
	{
	    temp = pop(&s);
	    printf("%d ",temp->item);

	    if(temp->right != NULL)
            push(&s,temp->right);
        if(temp->left != NULL)
            push(&s,temp->left);

	} while (!isEmpty(&s));
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

