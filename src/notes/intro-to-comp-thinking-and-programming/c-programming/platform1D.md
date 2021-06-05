---
title: Intro to Computational Thinking and Programming - platform1D
pageTitle: platform1D()
---

## platform1D()

<span class="tags"><a href="#">Pointers</a></span>

<hr>

Write a function that extracts the even digits from a positive number, and combines the even digits sequentially into a new number. The new number is returned to the calling function. If the input number does not contain any even digits, then the function returns -1. For example, if the input number is 1234567, then 246 will be returned; and if the input number is 13, then –1 will returned. You do not need to consider the input number such as 0, 20, 3033, etc. Write the function in two versions. The function **extEvenDigits1()** returns the result to the caller, while the function **extEvenDigits2()** returns the result through the pointer parameter, **result**. 
<br><br>
**The function prototypes are given as follows:**
<br>
<span class="functions">int extEvenDigits1(int num);</span><br>
<span class="functions">void extEvenDigits2(int num, int *result);</span>
<br><br>
<button id="openModalBtn">Click here for sample inputs/outputs</button>
<div class="modal-wrapper" id="modal">
	<div class="modal">
		<div class="modal-header">
			<h3>Sample Inputs & Outputs</h3>
		</div>
		<div class="modal-body">
			<p class="functions">
			<bold>(1) Test Case 1:</bold><br>
            Enter a number: 1234<br>
            extEvenDigits1(): 24<br>
            extEvenDigits2(): 24<br>
            <br>
            <bold>(2) Test Case 2:</bold><br>
            Enter a number: 1357<br>
            extEvenDigits1(): -1<br>
            extEvenDigits2(): -1<br>
            <br>
            <bold>(3) Test Case 3:</bold><br>
            Enter a number: 2468<br>
            extEvenDigits1(): 2468<br>
            extEvenDigits2(): 2468<br>
            <br>
            <bold>(4) Test Case 4:</bold><br>
            Enter a number: 6<br>
            extEvenDigits1(): 6<br>
            extEvenDigits2(): 6<br>
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
int platform1D(int ar[], int size);
int main(){
    int i,b[50],size;
    printf("Enter array size: \n");
    scanf("%d", &size);
    printf("Enter %d data: \n", size);
    for (i=0; i<size; i++)
    scanf("%d",&b[i]);
    printf("platform1D(): %d\n", platform1D(b,size));
    return 0;
}

int platform1D(int ar[], int size) {
    int i = 1, j = 0, length = 1, currentNum, prevNum, max;
    int lengthArr[20];

    while (i < size){
       currentNum = ar[i];
       prevNum = ar[i-1];

       if (currentNum == prevNum)
           length++;

       if (currentNum != prevNum || i == size-1){
           lengthArr[j] = length;
           length = 1;
           j++;
       }
       i++;
   }

    if (j == 0)
       return 1;
    else
       max = lengthArr[0];

    while (j > 0){
       if (max < lengthArr[j-1]){
           max = lengthArr[j-1];
       }
       j--;
   }
    return max;
}
```