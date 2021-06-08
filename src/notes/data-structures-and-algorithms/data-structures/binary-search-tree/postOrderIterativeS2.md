---
title: Data Structures and Algorithms
pageTitle: postOrderIterativeS2()
---

## postOrderIterativeS2()

<span class="tags"><a href="#">Binary Search Tree</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write an iterative C function <span class="functions">postOrderIterativeS2()</span> that prints the post-order traversal of a binary search tree using two stacks. Note that you should only use <span class="functions">push()</span> or <span class="functions">pop()</span> operations when you add or remove integers from the stacks. Remember to empty the stacks at the beginning, if the stacks are not empty.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void postOrderIterativeS2(BSTNode *root);</span>
<br><br>
**Following is the detailed algorithm:**

<span class="functions">
1) Push root to first stack.<br>
2) Loop while first stack is not empty<br>
&nbsp;&nbsp;&nbsp;&nbsp;2.1) Pop a node from first stack and push it to second stack<br>
&nbsp;&nbsp;&nbsp;&nbsp;2.2) Push left and right children of the popped node to first stack<br>
3) Print contents of second stack
</span>
<br><br>

**Let us consider the below tree for example.**<br>
<img src = "{{ '/images/binary-search-tree-postorderiteratives2.JPG' | url }}" class="diagrams">
<br><br>
Iterative Postorder Traversal: **10 18 15 25 80 50 20**
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
void postOrderIterativeS2(BSTNode *root);

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
	BSTNode * root;
	root = NULL;

	printf("1: Insert an integer into the binary search tree;\n");
	printf("2: Print the post-order traversal of the binary search tree;\n");
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
			printf("The resulting post-order traversal of the binary search tree is: ");
			postOrderIterativeS2(root); // You need to code this function
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

void postOrderIterativeS2(BSTNode *root)
{
	 /* add your code here */
	 Stack s1;
	 Stack s2;
	 s1.top = NULL;
	 s2.top = NULL;
	 BSTNode *temp = root;

	 if (temp != NULL)
     {
         push(&s1,temp);
         while(!isEmpty(&s1)){
            temp = pop(&s1);
            push(&s2,temp);
            if (temp->right!=NULL)
                push(&s1,temp->right);
            if (temp->left!=NULL)
                push(&s1,temp->left);
         }
         while(!isEmpty(&s2)){
            temp = pop(&s2);
            printf("%d ",temp->item);
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

