---
title: Data Structures and Algorithms
pageTitle: mirrorTree()
---

## mirrorTree()

<span class="tags"><a href="#">Binary Tree</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a recursive function <span class="functions">mirrorTree()</span> that will modify a binary tree so that the resulting tree is a mirror image of the original structure.
<br><br>
<img src = "{{ '/images/binary-tree-mirrortree.JPG' | url }}" class="diagrams">
<br><br>
**The function prototype is given as follows:**

<span class="functions">void mirrorTree(BTNode *node);</span>
<br><br>
You should not create any intermediate or temporary trees. The function accepts a single parameter: a pointer to the root note of the binary tree to be mirrored.
<br>

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

void mirrorTree(BTNode *node);
void printTree_InOrder(BTNode *node);

////////////////////////////////////////////////////////////////////

int main(int argc, const char * argv[]){

	int i;
	//char reply;

	BTNode *root, *root2;
	BTNode btn[15];

	// Create the tree in Q1
	// Using manual dynamic allocation of memory for BTNodes

	root = malloc(sizeof(BTNode));
	root->item = 4;

	root->left = malloc(sizeof(BTNode));
	root->left->item = 5;

	root->right = malloc(sizeof(BTNode));
	root->right->item = 2;

	root->left->left = NULL;

	root->left->right = malloc(sizeof(BTNode));
	root->left->right->item = 6;

	root->left->right->left = NULL;
	root->left->right->right = NULL;

	root->right->left = malloc(sizeof(BTNode));
	root->right->left->item = 3;

	root->right->right = malloc(sizeof(BTNode));
	root->right->right->item = 1;

	root->right->left->left = NULL;

	root->right->left->right = NULL;

	root->right->right->left = NULL;

	root->right->right->right = NULL;

	printTree_InOrder(root);
	printf("\n");
	mirrorTree(root);
	printTree_InOrder(root);
	printf("\n\n");

	return 0;
	//printf("\nenter any key to exit:");
	//fflush(stdin);
	//scanf("%c", &reply);
}

//////////////////////////////////////////////////////////////////////////////////////////////////

void mirrorTree(BTNode *node){

	BTNode *temp;

	if (node == NULL)
	return;

	// Swap left and right BTNode pointers
	// Using pre-order traversal
/*
	temp = node->left;
	node->left = node->right;
	node->right = temp;
	mirrorTree(node->left);
	mirrorTree(node->right);
*/
	// Using post-order traversal
/*
	 mirrorTree(node->left);
	 mirrorTree(node->right);
	 temp = node->left;
	 node->left = node->right;
	 node->right = temp;
*/

	// What about using in-order traversal?

	mirrorTree(node->left);
	temp = node->left;
	node->left = node->right;
	node->right = temp;
	mirrorTree(node->left);

}

///////////////////////////////////////////////////////////////////////////////////////////////

void printTree_InOrder(BTNode *node){

	if (node==NULL) return;
	printTree_InOrder(node->left);
	printf("%d, ",node->item);
	printTree_InOrder(node->right);
	return;
}

//////////////////////////////////////////////////////////////////////////////////////////////////////

```

