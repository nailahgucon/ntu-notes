---
title: Data Structures and Algorithms
pageTitle: printSmallerValues()
---

## printSmallerValues()

<span class="tags"><a href="#">Binary Tree</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a C function <span class="functions">printSmallerValues()</span> that accepts a pointer to the root node of a binary tree and prints all integers stored in the tree that are smaller than a given value m.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void printSmallerValues(BTNode *node, int m);</span>
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

void printSmallerValues(BTNode *node, int m);

////////////////////////////////////////////////////////////////////

int main(int argc, const char * argv[]){

	int i;
	//char reply;

	printf("\n input m for question 2:");
	scanf("%d", &i);
	printf("the values smaller than %d are:", i);
	printSmallerValues(root, i);
	printf("\n\n");

	return 0;
	//printf("\nenter any key to exit:");
	//fflush(stdin);
	//scanf("%c", &reply);
}

//////////////////////////////////////////////////////////////////////////////////////////////////

void printSmallerValues(BTNode *node, int m){
	if (node==NULL) return;
	if (node->item<m)
	printf("%d,", node->item);
	 printSmallerValues(node->left, m);
	 printSmallerValues(node->right, m);

	return;
}

///////////////////////////////////////////////////////////////////////////////////////////////////
```

