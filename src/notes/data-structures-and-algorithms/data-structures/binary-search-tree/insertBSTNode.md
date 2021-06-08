---
title: Data Structures and Algorithms
pageTitle: insertBSTNode()
---

## insertBSTNode()

<span class="tags"><a href="#">Binary Search Tree</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a function <span class="functions">insertBSTNode()</span> that adds an item to a Binary Search Tree.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void insertBSTNode(BTNode **node, int value);</span>
<br><br>
BST nodes should be created dynamically using a <span class="functions">malloc()</span> call.
<br><br>
Hint: The core of this function has been provided in the lecture slides. Make sure that your code is able to correctly add a node into an empty BST.
<br><br>

*Bonus Questions - findMin function : finding the min value of a node in a BST*

```c

//#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
////////////////////////////////////////////////////////////////////

typedef struct _btnode{
int item;
struct _btnode *left;
struct _btnode *right;
} BTNode;

////////////////////////////////////////////////////////////////////

void insertBSTNode(BTNode **node, int value);
BTNode *findMin(BTNode *p);

////////////////////////////////////////////////////////////////////

int main(){
	int i=0;

	BTNode *root=NULL;

	//question 1
	do{
		printf("input a value you want to insert(-1 to quit):");

		scanf("%d",&i);
		if (i!=-1)
			insertBSTNode(&root,i);
	}while(i!=-1);

	return 0;
}

//////////////////////////////////////////////////////////////////////

void insertBSTNode(BTNode **node, int value)
{

	if (*node==NULL) //if the tree is empty
	{
		*node=malloc(sizeof(BTNode));
		(*node)->item =value;
		(*node)->left =NULL;
		(*node)->right = NULL;
		return;
	}
	if ((*node)->item > value) //value is smaller than the node
		insertBSTNode(&((*node)->left), value);
	else if ((*node)->item <value) //value is larger than the node
		insertBSTNode(&((*node)->right), value);
	else // (*node)->item == value, value will not be inserted
	{
		printf("Already exists in the BST\n");
		return;
	}
	return;
}

///////////////////////////////////////////////////////////////////////////

BTNode *findMin(BTNode *p)
{
	if (p->left !=NULL)
		return findMin(p->left);
	else
		return p;
}

///////////////////////////////////////////////////////////////////////////

```

