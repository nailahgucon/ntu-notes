---
title: Data Structures and Algorithms
pageTitle: smallestValue()
---

## smallestValue()

<span class="tags"><a href="#">Binary Tree</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a function <span class="functions">smallestValue()</span> that returns the smallest value stored in a given tree. The function accepts a pointer to the root of the given tree.
<br><br>

**The function prototype is given as follows:**

<span class="functions">int smallestValue(BTNode *node);</span>
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

int smallestValue(BTNode *node);

////////////////////////////////////////////////////////////////////

int main(int argc, const char * argv[]){

	int i;
	//char reply;

	BTNode *root, *root2;
	BTNode btn[15];

	printf("The smallest value in the tree is %d:\n", smallestValue(root));

	return 0;
	//printf("\nenter any key to exit:");
	//fflush(stdin);
	//scanf("%c", &reply);
}

//////////////////////////////////////////////////////////////////////////////////////////////////

int smallestValue(BTNode *node)
{
	int l,r;
	if (node==NULL)
		return 100000;

	l=smallestValue(node->left);
	r=smallestValue(node->right);
	if (l<node->item && l<r)
		return l;
	else if (r<node->item && r<l)
		return r;
	else return node->item;
}

///////////////////////////////////////////////////////////////////////////////////////////////////
```

