---
title: Data Structures and Algorithms
pageTitle: postOrderIterativeS1()
---

## postOrderIterativeS1()

<span class="tags"><a href="#">Binary Search Tree</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write an iterative C function <span class="functions">postOrderIterativeS1()</span> that prints the post-order traversal of a binary search tree using a stack. Note that you should only use <span class="functions">push()</span> or <span class="functions">pop()</span> operations when you add or remove integers from the stack. Remember to empty the stack at the beginning, if the stack is not empty.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void postOrderIterativeS1(BSTNode *node);</span>
<br><br>
**Following is the detailed algorithm:**

<span class="functions">
1.1 Create an empty stack<br>
2.1 Do following while root is not NULL<br>
&nbsp;&nbsp;&nbsp;&nbsp;a) Push root's right child and then root to stack.<br>
&nbsp;&nbsp;&nbsp;&nbsp;b) Set root as root's left child.<br>
2.2 Pop an item from stack and set it as root.<br>
&nbsp;&nbsp;&nbsp;&nbsp;a) If the popped item has a right child and the right child is at top of stack, then remove the right child from stack, push the root back and set root as root's right child.<br>
&nbsp;&nbsp;&nbsp;&nbsp;b) Else print root's data and set root as NULL.<br>
2.3 Repeat steps 2.1 and 2.2 while stack is not empty.
</span>
<br><br>

**Let us consider the below tree for example.**<br>
<img src = "{{ '/images/binary-search-tree-postorderiteratives1.JPG' | url }}" class="diagrams">
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
void postOrderIterativeS1(BSTNode *node);

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
			postOrderIterativeS1(root); // You need to code this function
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

void postOrderIterativeS1(BSTNode *root)
{
	 /* add your code here */
	 Stack s;
	 s.top = NULL;
	 BSTNode *cur;
	 cur = root;

	 if (cur!=NULL){
        do{
            while (cur!=NULL){
                if (cur->right!=NULL)
                    push(&s,cur->right);
                push(&s,cur);
                cur = cur->left;
            }

            cur = pop(&s);
            if (cur->right != NULL && peek(&s)== cur->right)
                {
                    pop(&s); //remove the right not processed
                    push(&s,cur); //push the previous root to the stack
                    cur = cur->right;//set the current node to the right side so it can be processed (branch in deeper)
                }
            else{
                printf("%d", cur->item);
                cur = NULL; //when looping back no need dig deeper
            }

        }while (!isEmpty(&s));

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

