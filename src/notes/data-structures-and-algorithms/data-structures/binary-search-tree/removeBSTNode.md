---
title: Data Structures and Algorithms
pageTitle: removeBSTNode()
---

## removeBSTNode()

<span class="tags"><a href="#">Binary Search Tree</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a function <span class="functions">removeBSTNode()</span> that removes a given item from a Binary Search Tree.The function should return 0 if the item was found and successfully removed and 1 otherwise.
<br><br>

**The function prototype is given as follows:**

<span class="functions">BTNode *removeBSTNode(BTNode *node, int value);</span>
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
BTNode *removeBSTNode(BTNode *node, int value);

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

	do{
		printf("\ninput a value you want to remove(-1 to quit):");
		scanf("%d",&i);
		if (i!=-1)
		{
			root=removeBSTNode(root,i);
			printBSTInOrder(root);
		}
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

/////////////////////////////////////////////////////////////////

BTNode *removeBSTNode(BTNode *node, int value)
{
	BTNode *p;

	if (node==NULL)
	{
		printf("can't find the value!\n");
		return NULL;
	}

	if (node->item >value) //go left tree
		 node->left = removeBSTNode(node->left, value);

	else if (node->item <value) //go right tree
		 node->right = removeBSTNode(node->right, value);

	else// if ((*node)->item ==value) found the node!
		if (node->left!=NULL && node->right !=NULL ) //*node has two children
		{
			p=findMin(node->right);
			node->item =p->item;
			node->right = removeBSTNode(node->right,p->item );
		}
		else //x has no children or one child
		{
			p=node;

			if (node->left !=NULL)
				node=node->left;
			else
				node=node->right;

			free(p);
		}
	return node;
}

///////////////////////////////////////////////////////////////////////////
```

