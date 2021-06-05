---
title: Intro to Computational Thinking and Programming - findSubstring
pageTitle: findSubstring()
---

## findSubstring()

<span class="tags"><a href="#">Character Strings</a></span>

<hr>

Write a C function that takes two character string arguments, <span class="functions">str</span> and <span class="functions">substr</span> as input and returns 1 if <span class="functions">substr</span> is a substring of <span class="functions">str</span> (i.e. if <span class="functions">substr</span> is contained in <span class="functions">str</span>) and 0 if not. For example, the function will return 1 if <span class="functions">substr</span> is <span class="functions">"123"</span> and <span class="functions">str</span> is <span class="functions">"abc123xyz"</span>, but it will return 0 if otherwise. Note that for this question you are not allowed to use any string functions from the standard C library. 
<br><br>
**The prototype of the function is given below:**
<br>
<span class="functions">int findSubstring(char *str, char *substr);</span>
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
            Enter the string: abcde fgh<br>
			Enter the substring: abc<br>
			findSubstring(): Is a substring<br>
			<br>
			<bold>(2) Test Case 2:</bold><br>
			Enter the string: abcdefgh<br>
			Enter the substring: bc<br>
			findSubstring(): Is a substring<br>
			<br>
			<bold>(3) Test Case 3:</bold><br>
			Enter the string: abcde f<br>
			Enter the substring: cdef<br>
			findSubstring(): Not a substring<br>
			<br>
			<bold>(4) Test Case 4:</bold><br>
			Enter the string: abcdef<br>
			Enter the substring: xy<br>
			findSubstring(): Not a substring
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
#include <string.h>
#define INIT_VALUE 999
int findSubstring(char *str, char *substr);
int main()
{
	char str[40], substr[40], *p;
	int result = INIT_VALUE;

	printf("Enter the string: \n");
	fgets(str, 80, stdin);
	if (p=strchr(str,'\n')) *p = '\0';
	printf("Enter the substring: \n");
	fgets(substr, 80, stdin);
	if (p=strchr(substr,'\n')) *p = '\0';
	result = findSubstring(str, substr);
	if (result == 1)
		printf("findSubstring(): Is a substring\n");
	else if ( result == 0)
		printf("findSubstring(): Not a substring\n");
	else
		printf("findSubstring(): An error\n");
	return 0;
}

int findSubstring(char *str, char *substr){
	int i;

	while(*str != '\0'){
    	i = 0;

    	while(substr[i] != '\0'){
        	if(substr[i] != str[i])
        		break;
        	else if(substr[i+1] == '\0')
        		return 1;
        	++i;
     }
     ++str;
 }
return 0;
}

```