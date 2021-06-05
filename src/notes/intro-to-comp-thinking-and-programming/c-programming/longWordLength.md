---
title: Intro to Computational Thinking and Programming - longWordLength
pageTitle: longWordLength()
---

## longWordLength()

<span class="tags"><a href="#">Character Strings</a></span>

<hr>

Write a C function that accepts an English sentence as parameter, and returns the length of the longest word in the sentence. For example, if the sentence is <span class="functions">"I am happy."</span>, then the length of the longest word <span class="functions">"happy"</span> in the sentence 5 will be returned. Assume that each word is a sequence of English letters. 
<br><br>
**The function prototype is given as follows:**
<br>
<span class="functions">int longWordLength(char *s);</span>
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
            Enter a string: I am happy.<br>
            longWordLength(): 5<br>
            <br>
            <bold>(2) Test Case 2:</bold><br>
            Enter a string: There are forty students in the class.<br>
            longWordLength(): 8<br>
            <br>
            <bold>(3) Test Case 3:</bold><br>
            Enter a string: Good day!<br>
            longWordLength(): 4<br>
            <br>
            <bold>(4) Test Case 4:</bold><br>
            Enter a string: Hello<br>
            longWordLength(): 5
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
#include <ctype.h>
int longWordLength(char *s);

int main(){
    char str[80], *p;
    printf("Enter a string: \n");
    fgets(str, 80, stdin);
    if (p=strchr(str,'\n')) *p = '\0';
    printf("longWordLength(): %d\n", longWordLength(str));
    return 0;
}
int longWordLength(char *s){
    int longest = 0;
    int current = 0;
    
    while(*s != '\0'){
        if(isalpha(*s)){
            current++;
        }else{
            current = 0;
        }
        if(current > longest){
            longest = current;
        } s++;
    }
    return longest;
}

```