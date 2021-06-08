---
title: Data Structures and Algorithms
pageTitle: printBSTInOrder()
---

## printBSTInOrder()

<span class="tags"><a href="#">Binary Search Tree</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a function <span class="functions">printBSTInOrder()</span> that prints a sorted list of items stored in Binary SearchTree using an in-order traversal pattern.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void printBSTInOrder(BTNode *node);</span>
<br><br>

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
void printBSTInOrder(BTNode *node);

////////////////////////////////////////////////////////////////////

int main(){
	int i=0;

	BTNode *root=NULL;

	do{
		printf("input a value you want to insert(-1 to quit):");

		scanf("%d",&i);
		if (i!=-1)
			insertBSTNode(&root,i);
	}while(i!=-1);

	printf("\n");
	printBSTInOrder(root);

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

//////////////////////////////////////////////////////////////
void printBSTInOrder(BTNode *node)
{
	if (node==NULL)
		return;

	printBSTInOrder(node->left );
	printf("%d, ", node->item);
	printBSTInOrder(node->right);

	return;

}
///////////////////////////////////////////////////////////////////////////

```

