---
title: Data Structures and Algorithms
pageTitle: hasGreatGrandchild()
---

## hasGreatGrandchild()

<span class="tags"><a href="#">Binary Tree</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a recursive function <span class="functions">hasGreatGrandchild()</span> that prints the values stored in all nodes of a binary tree that have at least one great-grandchild. The function accepts a single parameter: a pointer to the root note of the binary tree.
<br><br>

**The function prototype is given as follows:**

<span class="functions">int hasGreatGrandchild(BTNode *node);</span>
<br><br>
_Hint: Determine the common property shared by nodes with great-grandchild nodes, and write a recursive function that computes that property._

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

int hasGreatGrandchild(BTNode *node);

////////////////////////////////////////////////////////////////////

int main(int argc, const char * argv[]){

	int i;
	//char reply;

	// Create a tree for Q4: Tall enough so some nodes have great-grandchildren
	// Use array of BTNodes, create tree by linking nodes together
	for (i = 0; i <= 6; i++){
		btn[i].item = i;
		btn[i].left = &(btn[i * 2 + 1]);
		btn[i].right = &(btn[i * 2 + 2]);
	}

	for (i = 7; i <= 14; i++){
		btn[i].item = i;
		btn[i].left = NULL;
		btn[i].right = NULL;
	}
	root2 = &btn[0];

	printf("The tree for question 4 visited by in-order is \n");
	printTree_InOrder(root2);
	printf("\nthe values stored in all nodes of the tree that have at least one great-grandchild are: ");

	hasGreatGrandchild(root2);

	return 0;
	//printf("\nenter any key to exit:");
	//fflush(stdin);
	//scanf("%c", &reply);
}

///////////////////////////////////////////////////////////////////////////////////////////////

int hasGreatGrandchild(BTNode *node){

	int l, r;

	// Calculate the height of each node in the tree
	// Print out (data stored in) node that has height > n

	if (node == NULL)
		return -1;

	l = hasGreatGrandchild(node->left);
	r = hasGreatGrandchild(node->right);

	if (r > l)
		l = r;
	if (l > 1)
		printf("%d ", node->item);

	return (l + 1);

}

//////////////////////////////////////////////////////////////////////////////////////////////////
```

