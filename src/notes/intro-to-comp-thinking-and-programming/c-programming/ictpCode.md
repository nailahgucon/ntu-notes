---
title: Intro to Computational Thinking and Programming
pageTitle: More Code done in ICTP
---

## More Code done in ICTP

*Functions of questions that i do not have the question paper of*
<br><br>

<div class="tab">
  <a class="tablinks" href="#control-flow" onclick="openTab(event, 'control-flow')" id="defaultOpen">Control Flow</a>
  <a class="tablinks" href="#arrays" onclick="openTab(event, 'arrays')">Arrays</a>
  <a class="tablinks" href="#character-strings" onclick="openTab(event, 'character-strings')">Character Strings</a>
  <a class="tablinks" href="#functions-and-pointers" onclick="openTab(event, 'cfunctions-and-pointers')">Functions & Pointers</a>
  <a class="tablinks" href="#structures" onclick="openTab(event, 'structures')">Structures</a>
</div>

<a id="control-flow"></a>
<h3 style="text-align:center; padding-top:100px;">Control Flow</h3><br>
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
<h3 style="text-align:center; padding-top:100px;">Arrays</h3><br>
<span class="functions">printReverse()</span>

```c
// Parameters: ar[], size
int i;
if(size > 0){
    for(i = size - 1; i >= 0; i--){
        printf("%d", ar[i]);
    }
    printf("\n");
}
```

<span class="functions">reverseAr1D()</span>

```c
// Parameters: ar[], size
int i, temp;
if(size > 0){
    for(i = 0; i < size/2; i++){
        temp = ar[i];
        ar[i] = ar[size - i - 1];
        ar[size - i - 1] = temp;
    }
}
```

<span class="functions">findAr1D()</span>

```c
// Parameters: size, ar[], target
int j;
for(j = 0; j < size; j++){
    if(ar[i] == target)
        return j;
    return -1;
}
```

<span class="functions">swap2Rows()</span>

```c
// Parameters: int ar[][SIZE], int r1, int r2
int temp;
int n;
for(n = 0; n < SIZE; n++){
    temp = ar[r1][n];
    ar[r1][n] = ar[r2][n];
    ar[r2][n] = temp;
}

// if its for col, e.g. ar[n][c1]
```

<span class="functions">Transpose2D()</span>

```c
// Parameters: int ar[][SIZE], int rowSize, int colSize
int h, k;
int temp;

for(h = 1; h < rowSize; h++){
    for(k = 0; k < colSize; k++){
        temp = ar[h][k];
        ar[h][k] = ar[k][h];
        ar[k][h] = temp;
    }
}
```

<span class="functions">reduceMatrix2D()</span>

```c
// Parameters: int ar[][SIZE], int rowSize, int colSize
int i, j, sum;
for(j = 0; j < colSize; j++){
    sum = 0;
    for(i = j+1; i < rowSize; i++){
        sum += ar[i][j];
        ar[i][j] = 0;
    }
    ar[j][j] += sum;
}
```

<span class="functions">compress2D()</span>

```c
// Parameters: int data[SIZE][SIZE], int rowSize, int colSize
int i, j, count, val;
for(i = 0; i < colSize; i++){
    val = *( *(data + i) + 0 );
    count = 0;
    for(j = 0; j < rowSize; j++){
        if(data[i][j] == val){
            count++;
        }
        else{
            printf("%d", val);
            printf("%d", count);
            count = 1;
            val = data[i][j];
        }
    }
    printf("%d", val);
    printf("%d", count);
    printf("\n");
}
```

<span class="functions">symmetry2D()</span>

```c
// Parameters: M[][SIZE], int rowSize, int colSize
int i, j, result = 1;
for(i = 0; i < rowSize; i++){
    for(j = 0; j < colSize; j++){
        if(M[i][j] != M[j][i]){
            result = 0;
            break;
        }
    }
}
return result;
```

<span class="functions">swapMinMax1D()</span>

```c
// Parameters: ar[], size
int min, max, temp, i;
min = 0;
max = 1;
if(ar[min] > ar[max]){
    temp = max;
    max = min;
    min = temp;
}
for(i = 2; i < size; i++){
    if(ar[i] >= ar[max]){
        max = i;
    } else if(ar[i] <= ar[min]){
        min = i;
    }
}
temp = ar[max];
ar[max] = ar[min];
ar[min] = temp;
```

<span class="functions">computeTotal2D()</span>

```c
// set hardcoded (4x4) 2D array
// Parameters: float matrix[4][4]
float average1 = (matrix[0][0] + matrix[0][1] + matrix[0][2])/3;
float average2 = (matrix[1][0] + matrix[1][1] + matrix[1][2])/3;
float average3 = (matrix[2][0] + matrix[2][1] + matrix[2][2])/3;
float average4 = (matrix[3][0] + matrix[3][1] + matrix[3][2])/3;

matrix[0][3] = average1;
matrix[1][3] = average2;
matrix[2][3] = average3;
matrix[3][3] = average4;
```

<span class="functions">SpecialNumbers1D()</span>

```c
// Parameters: int ar[], int num, int *size
int i = 100;
int a, b, c;
double sum = 0;

for(i = 100; i <= num; i++){
    a = (i/10)/10; //first number 
    b = (i/10)%10; //second number 
    c = i%10; //third number 
    sum = a*a*a + b*b*b + c*c*c;
    if(sum == i){
        ar[*size] = sum;
        ++(*size);
    }
}
```

<span class="functions">findMinMax1D()</span>

```c
// Parameters: ar[], size, *min, *max
int temp;

if(size == 1){
    *max = ar[0];
    *min = ar[0];
}else{
    *max = ar[0];
    *min = ar[1];
    if(*max < *min){
        temp = *max;
        *max = *min;
        *min = temp;
    }
    for(i = 2; i < size; i++){
        if(a[i] > *max){
            *max = a[i];
        }else if(a[i] < *min){
            *min = a[i];
        }
    }
}
```

<span class="functions">find2Max1D()</span>

```c
// Parameters: ar[], size, *max1, *max2
int i = 0;
int temp = 0;
*max1 = ar[0];
*max2 = ar[1];

if(*max2 > *max1){
    temp = *max1;
    *max1 = *max2;
    *max2 = temp;
}

for(i = 2; i < size; i++){
    if(ar[i] > *max1){
        *max2 = *max1;
        *max1 = ar[i];
    }else if(ar[i] < *max1 && ar[i] > *max2){
        *max2 = ar[i];
    }
}
```

<span class="functions">absoluteSum1D()</span>

```c
// Parameters: size, vector[]
int i = 0;
float sum = 0.0;

for(i = 0; i < size; i++){
    // fabs: float absolute, abs: int absolute
    sum += fabs(vector[i]);
}
return sum;
```

<span class="functions">insertChar()</span>

```c
// Parameters: *str1, *str2, ch
int i = 0;
int j = 0;

while(str1[i] != '\0'){
    if(i % 3 == 0 && i != 0){
        str2[j++] = str1[i++];
        str2[j++] = ch;
    }else{
        str2[j] = str1[i];
        j++;
        i++;
    }
}
str2[j] = '\0';
```

<span class="functions">findMinOfMax2D()</span>

```c
// Parameters: int ar[][SIZE], rowSize, colSize
for(i = 0; i < rowSize; i++){
    max = ar[i][0];
    for(j = 1; j < colSize; j++){
        if(ar[i][j] > max){
            max = ar[i][j];
        }
    }
    armax[i] = max;
}
min = armax[0];

for(k = 1; k < colSize; k++){
    if(armax[k] < min){
        min = armax[k];
    }
}
return min;
```
<br><br>
<!--- //////////////////////////////// MD Separator ////////////////////////////////////////// -->
<a id="character-strings"></a>
<h3 style="text-align:center; padding-top:100px;">Character Strings</h3><br>
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
<h3 style="text-align:center; padding-top:100px;">Functions & Pointers</h3><br>
<span class="functions">extEvenDigits()</span>

```c
// Parameters: num
int rem = 0;
int factor = 0;
int rev = 0;
int newfactor = 0;
int newrem = 0;

while(num != 0){
    rem = num % 10;
    if(rem % 2 == 0){
        factor += rem;
        factor *= 10;
    }
    num = num / 10;
}
newfactor = factor / 10;
while(newfactor != 0){
    newrem = newfactor % 10;
    rev = rev * 10 + newrem;
    newfactor /= 10;
}
if(factor == 0){
    return -1;
}else{
    return rev;
}
```

<span class="functions">allEvenDigits()</span>

```c
// Parameters: num
int count = 0;
int rem = 0;

while(num != 0){
    rem = num % 10;
    if(rem % 2 != 0){
        count++;
    }
    num = num / 10;
}
if(count > 0){
    return 0;
}else{
    return 1;
}
```

<span class="functions">countEvenDigits()</span>

```c
// Parameters: number
int count = 0;
int rem = 0;
while(number != 0){
    rem = number % 10;
    if(rem % 2 == 0){
        count++;
    }
    number /= 10;
}
return count;
```

<span class="functions">sumSqDigits()</span>

```c
// Parameters: num
int rem = 0;
int sqr = 0;

while(num != 0){
    rem = num % 10;
    sqr = sqr + (rem * rem);
    num = num / 10;
}
return sqr;
```

<span class="functions">computeTotal()</span>

```c
// Parameters: noOfLines
int i = 0;
int noOfNum = 0;
int num = 0;
int total = 0;
int j = 1;
for(i = 1; i <= noOfLines; i++){
    num = 0;
    total = 0;
    printf("Enter line %d: \n", i);
    scanf("%d", &noOfNum);
    while(j <= noOfNum){
        scanf("%d", &num);
        total += num;
        j++;
    }
    j = 1;
    printf("Total: %d \n", total);
}
```

<span class="functions">printPattern3()</span>

```c
// Parameters: height
int i = 1;
int j = 1;
int number = 1;

for(i = 1; i <= height; i++){
    for(j = 1; j <= i; j++){
        if(number == 10){
            number = 0;
        }
        if(j == 1){
            number = i;
        }
        printf("%d", number);
        number++;
    }
    printf("\n");
}
```

<span class="functions">printPattern2()</span>

```c
// Parameters: height
int i = 0;
int even = 0;
int odd = 0;

for(i = 1; i <= height; i++){
    if(i % 2 != 0){
        for(odd = 0; odd < i; odd++){
            if(odd % 2 != 0){
                printf("B");
            }else{
                printf("A");
            }
        }
        printf("\n");
    }else{
        for(even = 0; even < i; even++){
            if(even % 2 != 0){
                printf("A");
            }else{
                printf("B");
            }
        }
        printf("\n");
    }
}
```

<span class="functions">perfectProd()</span>

```c
// Parameters: num
int n, i, sum, result = 1;

for(n = 1; n <= num; n++){
    i = 1;
    sum = 0;
    while(i < n){
        if(n % i == 0){
            sum += i;
        }
        i++;
    }
    if(sum == n){
        printf("Perfect number: %d \n", n);
        result *= n;
    }
}
return result;
```

<span class="functions">power()</span>

```c
// Parameters: num, p
int i = 0;
int k = 0;
float result = 1;

if(p < 0){
    for(k = 0; k < abs(p); k++){
        result /= num;
    }
}else{
    for(i = 0; i < p; i++){
        result *= num;
    }
}
return result;
```

<span class="functions">reverseDigits()</span>

```c
// Parameters: int num
int rem = 0;
int rev = 0;
while(num != 0){
    rem = num % 10; // takes last number
    rev = rev * 10 + rem; //add rem to back of rev
    num = num / 10; // remove last digit
}
return rev;

// for *result, set it to 0 and replace rev
```

<span class="functions">ComputePay()/ComputeSalary()</span>

```c
// ComputePay1
int excessHours = 0;
int totalpay = 0;
if(noOfHours <= 160){
    return noOfHours * PayRate;
}else{
    excessHours = noOfHours - 160;
    totalpay = (160 * PayRate) + (excessHours * PayRate * 1.5);
    return totalpay;
}

// ComputePay2
int excessHours = 0;
if(noOfHours <= 160){
    *grossPay = noOfHours * PayRate;
}else{
    excessHours = noOfHours - 160;
    *grossPay = (160 * PayRate) + (excessHours * PayRate * 1.5);
}

//readInput
// Parameters: *id, *noOfHours, *payRate
printf("Enter ID: \n");
scanf("%d", id);
if(*id == -1)
    return;
printf("Enter no. of hrs: \n");
scanf("%d", noOfHours);
printf("Enter hourlt pay: \n");
scanf("%d", payRate);
```
<br><br>
<!--- //////////////////////////////// MD Separator ////////////////////////////////////////// -->
<a id="structures"></a>
<h3 style="text-align:center; padding-top:100px;">Structures</h3><br>
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
<span class="functions">Compute1()</span>

```c
// Parameters: beexpression expr

float result;
switch (expr.op){
    case '+': 
        result = expr.operand1 + expr.operand2;
        break;
    case '-': 
        result = expr.operand1 - expr.operand2;
        break;
    case '*': 
        result = expr.operand1 *+* expr.operand2;
        break;
    case '/': 
        result = expr.operand1 / expr.operand2;
        break;
}
return result;
```

<span class="functions">PhoneBook()</span>

```c
// Parameters: PhoneBk *pb, int size, char *target

int i;
for(i = 0; i < size; i++){
    if(strcmp(pb->name, target) == 0){
        printf("Name = %s, Tel = %d", target, pb->telno);
        break;
    }
}

if(i == size)
    printf("name not found\n");
```

<span class="functions">Student()</span>

```c
// inputStud()
// Parameters: Student *s, int size
int i = 0;
while(i < size){
    printf("Enter ID: \n");
    scanf("%d", s[i].id);
    printf("Enter Name: \n");
    scanf("\n");
    fgets(s[i].name, 50, stdin);
    i++;
}

// PrintStud()
// Parameters: Student *s, int size
int i = 0;
printf("The current student list: \n");
for(i = 0; i < size; i++){
    printf("Student ID: %d Student Name: %s", s[i].id, s[i].name);
}
```

<span class="functions">Customer()</span>

```c
// nextCustomer()
// Parameters: struct account *acct
printf("Enter names (firstName lastName): \n");
scanf("%s %s", acct->names.firstName, acct->names.lastName);

// printCustomer()
// Parameters: struct account acct
printf("Enter account number: \n");
scanf("%d", &acct.accountNum);
printf("Enter balance: \n");
scanf("%lf", &acct.balance);
printf("Customer record: \n");
printf("%s %s %d %.2lf \n", acct.names.firstName, acct.names.lastName, acct.accountNum, acct.balance);
```

<span class="functions">Employee()</span>

```c
// readin()
// Parameters: *emp
int i = 0;
getchar();
printf("Enter name: \n");
gets(emp[0].name);
while(strcmp(emp[i].name, "#") == 0){
    printf("Enter tel: \n");
    gets(emp[i].telno);
    printf("Enter id: \n");
    scanf("%d", &emp[i].id);
    printf("Enter salary: \n");
    scanf("%lf", &emp[i].salary);
    i++;
    getchar();
    printf("Enter name: \n");
    gets(emp[i].name);
}
return i;

// search()
// Parameters: *emp, size, *target
int i = 0;
for(i = 0; i < size; i++){
    if(strcmp(emp[i].name, target) == 0){
        printf("Employee found at index location: %d", i);
        printf("%s %d %d %lf", emp[i].name, emp[i].telno, emp[i].id, emp[i].salary);
        return 1;
    }
}
return 0;

// addEmployee()
if(size == MAX){
    printf("Database is full");
    return size;
}else{
    strcpy(emp[size].name, target);
    printf("Enter tel: \n");
    gets(emp[size].telno);
    printf("Enter id: \n");
    scanf("%d", &emp[size].id);
    printf("Enter salary: \n");
    scanf("%lf", &emp[size].salary);
    printf("Added at position: %d \n", size);
    return ++size;
}
```
<br><br>
<!--- //////////////////////////////// MD Separator ////////////////////////////////////////// -->

<script>
function openTab(evt, tabName) {
  var i, tablinks;
  tablinks = document.getElementsByClassName("tablinks");
  for (i = 0; i < tablinks.length; i++) {
    tablinks[i].className = tablinks[i].className.replace(" active", "");
  }
  evt.currentTarget.className += " active";
}

// Get the element with id="defaultOpen" and click on it
document.getElementById("defaultOpen").click();
</script>