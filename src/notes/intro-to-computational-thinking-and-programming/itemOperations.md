---
title: Intro to Computational Thinking and Programming - itemOperations
pageTitle: itemsOperations
---

## itemOperations

<span class="tags"><a href="#">Pointers</a></span>
<span class="tags"><a href="#">Arrays</a></span>
<hr>

Write a C program for the following functions that work on arrays which can store up to 10
integers:<br><br>
<span class="functions"><bold>(1) void insert(int max, int *size, int ar[], int num);</bold></span><br>
This function inserts the number <span class="functions">num</span> into the array <span class="functions">ar</span> where the pointer parameter size stores the number of integers in <span class="functions">ar</span>. Before and after the function call, <span class="functions">ar</span> is an array of integers in <strong>ascending order</strong>. <span class="functions">max</span> is the maximum number of integers which can be stored in <span class="functions">ar</span>. This means that the function should issue an error message <span class="functions">"The array is full\n"</span> and no insertion should be done if <span class="functions">*size</span> is equal to <span class="functions">max</span> before insertion.
<br><br>

<span class="functions"><bold>(2) void iremove(int *size, int ar[], int num);</bold></span><br>
This function removes the <strong>first appearance</strong> of the number <span class="functions">num</span> from the array <span class="functions">ar</span> which has <span class="functions">*size</span> numbers in it. Before and after the function call, <span class="functions">ar</span> is an array of integers in <strong>ascending order</strong>. Please note:
<dl>
<dd>- After the number is removed, the message <span class="functions">"The integer is removed\n"</span> should be displayed.</dd>
<dd>- If <span class="functions">*size</span> is equal to zero, the error message <span class="functions">"The array is empty\n"</span> should be displayed.</dd>
<dd>- If <span class="functions">num</span> does not appear in <span class="functions">ar</span>, the function should issue an error message <span class="functions">"The number is not in the array\n"</span>.</dd>
</dl>
<br>

<span class="functions"><bold>(3) void initialize(int *size, int ar[]);</bold></span><br>
This function reads in a specified number of integers and uses <span class="functions">insert()</span> to store them in <span class="functions">ar</span>. The pointer parameter <span class="functions">size</span> returns the actual number of integers stored in <span class="functions">ar</span>, and <span class="functions">ar</span> will be an array of integers in <strong>ascending order</strong>.
<br><br>

<span class="functions"><bold>(4) void display(int size, int ar[]);</bold></span><br>
This function prints the numbers stored in <span class="functions">ar</span>. <span class="functions">size</span> gives the number of integers
stored in <span class="functions">ar</span>.
<br><br>

<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
			<bold>(1) Test Case 1: /* initialize */</bold><br>
            Enter your choice: 1<br>
            Enter the total number of integers (MAX=10): 5<br>
            Enter the integers: 3 5 2 1 4<br>
            Enter your choice: 4<br>
            The 5 numbers in the array: 1 2 3 4 5<br>
            Enter your choice: 5<br>
            <br>
            <bold>(2) Test Case 2: /*insert */</bold><br>
            Enter your choice: 1<br>
            Enter the total number of integers (MAX=10): 9<br>
            Enter the integers: 5 6 7 8 10 1 2 3 4<br>
            Enter your choice: 2<br>
            Enter an integer: 9<br>
            Enter your choice: 4<br>
            The 10 numbers in the array: 1 2 3 4 5 6 7 8 9 10<br>
            Enter your choice: 2<br>
            Enter an integer: 11<br>
            The array is full<br>
            Enter your choice: 5<br>
            <br>
            <bold>(3) Test Case 3: /* iremove */</bold><br>
            Enter your choice: 1<br>
            Enter the total number of integers (MAX=10): 2<br>
            Enter the integers: 5 6<br>
            Enter your choice: 3<br>
            Enter the integer to be removed: 5<br>
            The integer is removed<br>
            Enter your choice: 3<br>
            Enter the integer to be removed: 4<br>
            The number is not in the array<br>
            Enter your choice: 3<br>
            Enter the integer to be removed: 6<br>
            The integer is removed<br>
            Enter your choice: 3<br>
            Enter the integer to be removed: 3<br>
            The array is empty<br>
            Enter your choice: 5<br>
			</p>
		</div>
		<div class="modal-footer">
			<button id="closeModalBtn">Close</button>
		</div>
	</div>
</div>
<br>

```c
#include <stdio.h>
#define MAX 10
void initialize(int *size, int ar[]);
void insert(int max, int *size, int ar[], int num);
void iremove(int *size, int ar[], int num);
void display(int size, int ar[]);
int main(){
    int option = 0;
    int num, ar[MAX], size = 0;
    printf("Please select an option: \n");
    printf("(1) Initialize the array \n");
    printf("(2) Insert an integer \n");
    printf("(3) Remove an integer \n");
    printf("(4) Display the numbers stored in the array \n");
    printf("(5) Quit \n");
    do {
        printf("Enter your choice: \n");
        scanf("%d", &option);
        switch (option) {
            case 1:
            initialize(&size, ar);
            break;
            case 2:
            printf("Enter an integer: \n");
            scanf("%d", &num);
            insert(MAX, &size, ar, num);
            break;
            case 3:
            printf("Enter the integer to be removed: \n");
            scanf("%d", &num);
            iremove(&size, ar, num);
            break;
            case 4:
            display(size, ar);
            break;
            default:
            break;
        }
    } while (option < 5);
    return 0;
}

void display(int size, int ar[]){
    int i;
    printf("The %d numbers in the array: \n", size);
    for(i = 0; i < size; i++)
    printf("%d ", ar[i]);
    printf("\n");
}

void initialize(int *size, int ar[]){
    int total, i, num;
    printf("Enter the total number of integers (MAX=%d): \n", MAX);
    scanf("%d", &total);
    (*size) = 0;
    printf("Enter the integers: \n");
    for (i = 0; i < total; i++) {
        scanf("%d", &num);
        insert(MAX, size, ar, num);
    }
}

void insert(int max, int *size, int ar[], int num){
    int n = *size;
    int i, j;
    int k = 0;

    if(*size == 10){
        printf("%s", "The array is full\n");
    }else{
    for (i = 0; i < n + 1; i++)
    if (!k) {
        if (ar[i] > num || i == n) {
        for (j = n - 1; j >= i; j--) {
            ar[j + 1] = ar[j];
        }
        ar[i] = num;
        n++;
        k = 1;
        }
    }
    *size = n;
    }
}

void iremove(int *size, int ar[], int num){
    int c, pos, found = 0, n = *size;
    if(*size == 0){
    printf("The array is empty\n");
    }else{
    // check the element to be deleted is in array or not
    for(c = 0; c < n; c++){
        if(ar[c] == num){
            found = 1;
            pos = c;
            break;  // terminate the loop
        }
    }
    if(found == 1) // the element to be deleted exists in the array
    {
        for(c = pos; c < n-1; c++)
            ar[c] = ar[c+1];
            n -= 1;
            printf("Size of array: %d\n", *size);
        printf("%s", "The integer is removed\n");
    }
    else
        printf("not found in the array\n");
    *size = n;
    }
}
```