---
title: Intro to Computational Thinking and Programming - extEvenDigits
pageTitle: extEvenDigits
---

## extEvenDigits

<span class="tags"><a href="#">Pointers</a></span>

<hr>

Write a function that extracts the even digits from a positive number, and combines the even digits sequentially into a new number. The new number is returned to the calling function. If the input number does not contain any even digits, then the function returns -1. For example, if the input number is 1234567, then 246 will be returned; and if the input number is 13, then –1 will returned.
You do not need to consider the input number such as 0, 20, 3033, etc. Write the function in two versions. The function <span class="functions">extEvenDigits1()</span> returns the result to the caller, while the function <span class="functions">extEvenDigits2()</span> returns the result through the pointer parameter, <span class="functions">result</span>. The function prototypes are given as follows:
<br><br>
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
#define INIT_VALUE 999
int extEvenDigits1(int num);
void extEvenDigits2(int num, int *result);
int main(){
    int number, result = INIT_VALUE;
    printf("Enter a number: \n");
    scanf("%d", &number);
    printf("extEvenDigits1(): %d\n", extEvenDigits1(number));
    extEvenDigits2(number, &result);
    printf("extEvenDigits2(): %d\n", result);
    return 0;
}

int extEvenDigits1(int num){
    int i=1, newValue=0;
    while(num != 0){
        if((num % 10) % 2 != 1){
          newValue += (num % 10) * i;
          i *= 10;
        }
        num /= 10;
    }
    return (newValue != 0) ? newValue : -1;
}

void extEvenDigits2(int num, int *result){
    int i=1;
    *result = 0;

    while(num != 0){
        if((num % 10) % 2 != 1){
            *result += (num % 10) * i;
            i *= 10;
        }
        num /= 10;
    }
    if(*result == 0)
        *result = -1;
}

```