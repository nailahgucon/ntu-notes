---
title: Intro to Computational Thinking and Programming - cipherText
pageTitle: cipherText
---

## cipherText

<span class="tags"><a href="#">Character Strings</a></span>

<hr>

Cipher text is a popular encryption technique. What we do in cipher text is that we can encrypt each apha <span class="functions">('a' .. 'z', 'A' .. 'Z')</span> character with +1. For example, <span class="functions">"Hello"</span> can be encrypted with +1 cipher to <span class="functions">"Ifmmp"</span>. If a character is <span class="functions">'z'</span> or <span class="functions">'Z'</span>, the corresponding encrypted character will be <span class="functions">'a'</span> or <span class="functions">'A'</span> respectively. For other characters, no encryption is performed. We use call by reference in the implementation. Write the C functions <span class="functions">cipher()</span> and <span class="functions">decipher()</span> with the following function prototypes:
<br><br>
<span class="functions">void cipher(char *s);</span>
<span class="functions">void decipher(char *s);</span>
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
            Select one of the following options:<br>
            1: cipher()<br>
            2: decipher()<br>
            3: exit()<br>
            Enter your choice: 1<br>
            Enter the string: 123a<br>
            To cipher: 123a -> 123b<br>
            Enter your choice: 3<br>
            <br>
            <bold>(2) Test Case 2:</bold><br>
            Select one of the following options:<br>
            1: cipher()<br>
            2: decipher()<br>
            3: exit()<br>
            Enter your choice: 2<br>
            Enter the string: 123b<br>
            To decipher: 123b -> 123a<br>
            Enter your choice: 3<br>
            <br>
            <bold>(3) Test Case 3:</bold><br>
            Select one of the following options:<br>
            1: cipher()<br>
            2: decipher()<br>
            3: exit()<br>
            Enter your choice: 1<br>
            Enter the string: abcxyz<br>
            To cipher: abcxyz -> bcdyza<br>
            Enter your choice: 2<br>
            Enter the string: bcdyza<br>
            To decipher: bcdyza -> abcxyz<br>
            Enter your choice: 3<br>
            <br>
            <bold>(4) Test Case 4:</bold><br>
            Select one of the following options:<br>
            1: cipher()<br>
            2: decipher()<br>
            3: exit()<br>
            Enter your choice: 1<br>
            Enter the string: HELLO Hello<br>
            To cipher: HELLO Hello -> IFMMP Ifmmp<br>
            Enter your choice: 2<br>
            Enter the string: IFMMP Ifmmp<br>
            To decipher: IFMMP Ifmmp -> HELLO Hello<br>
            Enter your choice: 3
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
void cipher(char *s);
void decipher(char *s);
int main(){
    char str[80], dummychar, *p;
    int choice;

    printf("Select one of the following options: \n");
    printf("1: cipher() \n");
    printf("2: decipher() \n");
    printf("3: exit() \n");

    do {
        printf("Enter your choice: \n");
        scanf("%d", &choice);
        switch (choice) {
            case 1:
                scanf("%c",&dummychar);
                printf("Enter the string: \n");
                fgets(str, 80, stdin);
                if (p=strchr(str,'\n')) *p = '\0';
                printf("To cipher: %s -> ", str);
                cipher(str);
                printf("%s\n", str);
                break;
            case 2:
                scanf("%c",&dummychar);
                printf("Enter the string: \n");
                fgets(str, 80, stdin);
                if (p=strchr(str,'\n')) *p = '\0';
                printf("To decipher: %s -> ", str);
                decipher(str);
                printf("%s\n", str);
                break;
            default:
                break;
        }
    } while (choice < 3);
    return 0;
}

void cipher(char *s){
    int i = 0;

    while(s[i] != '\0'){
        if(!isdigit(s[i]) && s[i] != ' '){
            if(s[i] != 'Z' && s[i] != 'z')
                ++s[i];
            else
                s[i] -= 25;
     }
     ++i;
    }    
}

void decipher(char *s){
    int i = 0;

    while(s[i] != '\0'){
        if(!isdigit(s[i]) && s[i] != ' '){
            if(s[i] != 'A' && s[i] != 'a')
                --s[i];
            else
                s[i] += 25;
     }
     ++i;
    }   
}

```