---
title: Intro to Computational Thinking and Programming
pageTitle: More Code done in ICTP
---

## More Code done in ICTP

*Functions of questions that i do not have the question paper of*
<br><br>

**Jump to:** 
<span class="tags"><a href="#control-flow">Control Flow</a></span>
<span class="tags"><a href="#arrays">Arrays</a></span>
<span class="tags"><a href="#character-strings">Character Strings</a></span>
<span class="tags"><a href="#functions-and-pointers">Functions & Pointers</a></span>
<span class="tags"><a href="#structures">Structures</a></span>
<hr>
<br>
<a id="control-flow"></a>
<h3 style="text-align:center">Control Flow</h3><br>
<span class="functions">grade()</span>

```c
// main()
int studentNumber=0, mark;
printf("Enter ID:\n");
scanf("%d", &studentNumber);
while(studentNumber != -1){
    if mark >= 75){
        printf("grade = A\n");
    }
    // continue with grade = B to E...
    else{
        printf("grade = F\n");
    }
    printf("StudentID:");
    scanf("%d",&studentNumber);
}
return c;
```
<br><br>
<!--- //////////////////////////////// MD Separator ////////////////////////////////////////// -->
<a id="arrays"></a>
<h3 style="text-align:center">Arrays</h3><br>
<span class="functions">functionnamehere</span>

```c
// insert code here
```
<span class="functions">functionnamehere2</span>

```c
// insert code here
```
<br><br>
<!--- //////////////////////////////// MD Separator ////////////////////////////////////////// -->
<a id="character-strings"></a>
<h3 style="text-align:center">Character Strings</h3><br>
<span class="functions">palindrome()</span>

```c
// Parameters: *str

char newstr[100];
int i,j=0;
int len = strlen(str);
for(i=len-1;i>=0;i--){
    newstr[j++] = str[i];
}
if(strcmp(newstr,str) == 0){
    return 1;
}
return 0;
```

<span class="functions">SweepSpace()</span>

```c
// Parameters: *str

int i, j = 0, len;
len = strlen(str);

for(i=0; i < len; i++;){
    if(str[i] != ' '){
        str[j] = str[i];
        j++;
    }
}
str[j] = "\0";
return str;
```

<span class="functions">strIntersect()</span>

```c
// Parameters: *str1, *str2, *str3

int index = 0;
while(*str1){
    // strchr: find occurence of str2 in str1
    if(strchr(str2,*str1)){
        str3[index]=*str1;
        index++;
    }
    str1++;
}
str3[index] = "\0";
```

<span class="functions">maxCharToFront()</span>

```c
// Parameters: *str

int i = 0;
char max = str[0];
int maxindex = 0;
for(i=1;i<strlen(str);i++){
    if(str[i]>max){
        max=str[i];
        maxindex=i;
    }
}
for(i=maxindex;i>0;i--){
    str[i]=str[i-1];
}
str[0]=max;
```

<span class="functions">findMinMaxStr()</span>

```c
// Parameters: word[][40],*first,*last,size

int i = 1;

strcpy(*first,word[0]);
strcpy(*last,word[0]);

for(i=1;i<size;i++){
    if(strcmp(first,word[i])>0){
        strcpy(first,word[i]);
    }
    if(strcmp(last,word[i])<0){
        strcpy(last,word[i]);
    }
}
```

<span class="functions">longestStrInAr()</span>

```c
// Parameters: char str[N][40], int size, int *length

int i = 0;

*length = strlen(str[0]);
for(i=1;i<size;i++){
    if(strlen(str[i])>(*length)){
        *length = strlen(str[i]);
    }
}
i=0;
for(i=0;i<size;i++){
    if(strlen(str[i])==(*length)){
        return str[i];
    }
}
```

<span class="functions">cipherText()</span>

```c
// Parameters: *s
// include ctype.h

int i = 0;

while(s[i] != '\0'){
    if(!isdigit(s[i]) && s[i] != ' '){
        if(s[i] != 'Z' && s[i] != 'z'){
            ++s[i];
        }else{
            s[i] -= 25;
        }
        ++i;
    }
}
```

<span class="functions">decipherText()</span>

```c
// Parameters: *s
// include ctype.h

int i = 0;

while(s[i] != '\0'){
    if(!isdigit(s[i]) && s[i] != ' '){
        if(s[i] != 'A' && s[i] != 'a'){
            --s[i];
        }else{
            s[i] += 25;
        }
        ++i;
    }
}
```
<span class="functions">CountWords()</span>

```c
// Parameters: *s

int count = 1;
int i = 0;

for(i=0;i<strlen(s);i++){
    if(s[i] == '\0'){
        break;
    }else if(s[i] == ' '){
        count++;
    }
}
return count;
```

<span class="functions">LongWordLength()</span>

```c
// Parameters: *s
// include ctype.h, string.h

int longest = 0;
int current  = 0;

while(*s != '\0'){
    if(isalpha(*s)){
        current++;
    }else{
        current = 0;
    }
    if(current > longest){
        longest = current;
    }s++;
    return longest;
}
```

<span class="functions">processStrings()</span>

```c
// Parameters: *str, *totVowels, *totDigits
// include ctype.h

int i = 0;
*totVowels = 0;
*totDigits = 0;

for(i=0;i<strlen(str);i++){
    if(str[i]=='a' || str[i]=='e' || str[i]=='i' || str[i]=='o' || str[i]=='u' || 
    str[i]=='A' || str[i]=='E' || str[i]=='I' || str[i]=='O' || str[i]=='U'){
        *totVowels += 1;
    }
    if(isdigit(str[i])){
        *totDigits += 1;
    }
}
```

<span class="functions">locateFirstChar()</span>

```c
// Parameters: *str, ch

int i = 0;

for(i=0;i<strlen(str);i++){
    if(str[i]==ch){
        return i;
    }
}
return -1;
```

<span class="functions">countSubString()</span>

```c
// Parameters: str[], substr[]

int i = 0;
int count = 0;

while(*str != '\0'){
    while(substr[i] != '\0'){
        if(str[i] != substr[i]){
            break;
        }else if(substr[i+1] == '\0'){
            count++;
        }
        i++;
    }
    str++;
}
return count;
```
<br><br>
<!--- //////////////////////////////// MD Separator ////////////////////////////////////////// -->
<a id="functions-and-pointers"></a>
<h3 style="text-align:center">Functions & Pointers</h3><br>
<span class="functions">functionnamehere</span>

```c
// insert code here
```
<span class="functions">functionnamehere2</span>

```c
// insert code here
```
<br><br>
<!--- //////////////////////////////// MD Separator ////////////////////////////////////////// -->
<a id="structures"></a>
<h3 style="text-align:center">Structures</h3><br>
<span class="functions">CircleIntersect()</span>

```c
// Intersect()
// Parameters: struct circle c1, struct circle c2

double a, b;
int result;

a = c1.x - c2.x;
b = c1.y - c2.y;

return (sqrt(a*a + b*b) <= (c1.radius + c2.radius));

// Contain()
// Parameters: struct circle *c1, struct *circle c2

double a, b;

a = c1->x - c2->x;
b = c1->y - c2->y;

return (c1->radius >= (c2->radius + sqrt(a*a + b*b))); 
```
<span class="functions">functionnamehere2</span>

```c
// insert code here
```
<br><br>
<!--- //////////////////////////////// MD Separator ////////////////////////////////////////// -->