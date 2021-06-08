---
title: Data Structures and Algorithms
pageTitle: levelOrderTraversal()
---

## levelOrderTraversal()

<span class="tags"><a href="#">Binary Search Tree</a></span>
<span class="tags"><a href="#">Tutorial</a></span>

<hr>

Write an iterative C function <span class="functions">levelOrderTraversal()</span> prints a level-bylevel traversal of the binary tree using a **queue**, starting at the root node level. Note that you should **only** use <span class="functions">enqueue()</span> or <span class="functions">dequeue()</span> operations when you add or remove integers from the queue. Remember to empty the queue at the beginning, if the queue is not empty.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void levelOrderIterative(BSTNode *root);</span>
<br><br>

**Following is the detailed algorithm:**

<span class="functions">
1) Create an empty queue q<br>
2) If tree is not empty, then Enqueue root to the Queue<br>
3) Repeat until Queue is empty<br>
&nbsp;&nbsp;&nbsp;&nbsp;a) Dequeue node’s data from the queue and print it<br>
&nbsp;&nbsp;&nbsp;&nbsp;b) Enqueue node’s left child to the q<br>
&nbsp;&nbsp;&nbsp;&nbsp;c) Enqueue node’s right child to the q<br>
</span>
<br>

**Let’s consider the below tree for example:**<br><br>
<img src = "{{ '/images/binary-tree-levelordertraversal.JPG' | url }}" class="diagrams">
<br><br>

Level-order Tree Traversal: **20 15 50 10 18 25 80**

<br>

```c
//////////////////////////////////////////////////////////////////////////////////

#include <stdio.h>
#include <stdlib.h>

#define BUFFER_SIZE 1024
///////////////////////////////////////////////////////////////////////////////////

typedef struct _bstnode{
	int item;
	struct _bstnode *left;
	struct _bstnode *right;
} BSTNode;   // You should not change the definition of BSTNode

typedef struct _QueueNode {
	BSTNode *data;
	struct _QueueNode *nextPtr;
}QueueNode; // You should not change the definition of QueueNode


typedef struct _queue
{
	QueueNode *head;
	QueueNode *tail;
}Queue; // You should not change the definition of queue

///////////////////////////////////////////////////////////////////////////////////

// You should not change the prototypes of these functions
void levelOrderTraversal(BSTNode *node);

void insertBSTNode(BSTNode **node, int value);

BSTNode* dequeue(QueueNode **head, QueueNode **tail);
void enqueue(QueueNode **head, QueueNode **tail, BSTNode *node);
int isEmpty(QueueNode *head);
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
	printf("2: Print the level-order traversal of the binary search tree;\n");
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
			printf("The resulting level-order traversal of the binary search tree is: ");
			levelOrderTraversal(root); // You need to code this function
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

void levelOrderTraversal(BSTNode* root)
{
    Queue q;
    q.head=NULL;
    q.tail=NULL;
    BSTNode *temp;
    temp = root;

    if(temp != NULL)
    {
          enqueue(&q.head,&q.tail,temp);
          while(!isEmpty(q.head))
          {
              temp=dequeue(&q.head,&q.tail);
              printf("%d ",temp->item);
              if(temp->left!=NULL)
                  enqueue(&q.head,&q.tail,temp->left);
              if(temp->right!=NULL)
                  enqueue(&q.head,&q.tail,temp->right);
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

// enqueue node
void enqueue(QueueNode **headPtr, QueueNode **tailPtr, BSTNode *node)
{
	// dynamically allocate memory
	QueueNode *newPtr = malloc(sizeof(QueueNode));

	// if newPtr does not equal NULL
	if (newPtr != NULL) {
		newPtr->data = node;
		newPtr->nextPtr = NULL;

		// if queue is empty, insert at head
		if (isEmpty(*headPtr)) {
			*headPtr = newPtr;
		}
		else { // insert at tail
			(*tailPtr)->nextPtr = newPtr;
		}

		*tailPtr = newPtr;
	}
	else {
		printf("Node not inserted");
	}
}

BSTNode* dequeue(QueueNode **headPtr, QueueNode **tailPtr)
{
	BSTNode *node = (*headPtr)->data;
	QueueNode *tempPtr = *headPtr;
	*headPtr = (*headPtr)->nextPtr;

	if (*headPtr == NULL) {
		*tailPtr = NULL;
	}

	free(tempPtr);

	return node;
}

int isEmpty(QueueNode *head)
{
	return head == NULL;
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

