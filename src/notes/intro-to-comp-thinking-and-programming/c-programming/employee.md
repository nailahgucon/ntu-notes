---
title: Intro to Computational Thinking and Programming - employee
pageTitle: employee()
---

## employee()

<span class="tags"><a href="#">Structures</a></span>

<hr>

Write a C program that creates an array of structures to hold the employee information below:
<br><br>
<span class="functions">
typedef struct {<br>
&nbsp;&nbsp;&nbsp; char name[40];<br>
&nbsp;&nbsp;&nbsp; char telno[40];<br>
&nbsp;&nbsp;&nbsp; int id;<br>
&nbsp;&nbsp;&nbsp; double salary;<br>
} Employee;
</span>
<br><br>
**You are required to implement the following three functions:**
<br><br>
<dl>
<dd>- The function <span class="functions">readin()</span> reads a number of persons’ names and their corresponding telephone numbers, passes the data to the caller via the parameter <span class="functions">p</span>, and returns the number of names that have entered. The character <span class="functions">'#'</span> is used to indicate the end of user input.</dd>
<dd>- The function <span class="functions">search()</span> allows the user to query the array using the name field. If the name is found, the program displays the message <span class="functions">“Employee found at index location: x”</span>. The function <span class="functions">search()</span> finds the employee data of an input name <span class="functions">target</span>, and then prints the name, telephone number, id and salary on the screen. If the input name cannot be found, then it will print the error message <span class="functions">“Name not found”</span> on the screen.</dd>
<dd>- If the name is not found and the array is not full, the user can then add the name as a new record into the array. Assume that the maximum size of the array is 100. The function <span class="functions">addEmployee()</span> adds a new employee record into the array. The message <span class="functions">“Added at position: x”</span> will be printed. If the database is fill, an error message <span class="functions">“Database is full”</span> will be printed on the screen. The function returns the updated size of the array after
adding the new employee record.</dd>
</dl>
<br>

**The prototypes of the functions are given below:**
<br>
<span class="functions">int readin(Employee *emp);</span><br>
<span class="functions">int search(Employee *emp, int size, char *target);</span><br>
<span class="functions">int addEmployee(Employee *emp, int size, char *target);</span>
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
			1: readin()<br>
			2: search()<br>
			3: addEmployee()<br>
			4: print()<br>
			5: exit()<br>
			Enter your choice: 1<br>
			Enter name: Hui Siu Cheung<br>
			Enter tel: 12345678<br>
			Enter id: 11<br>
			Enter salary: 123.45<br>
			Enter name: #<br>
			Enter your choice: 4<br>
			The current employee list:<br>
			Hui Siu Cheung 12345678 11 123.45<br>
			Enter your choice: 5<br>
			<br>
			<bold>(2) Test Case 2:</bold><br>
			Select one of the following options:<br>
			1: readin()<br>
			2: search()<br>
			3: addEmployee()<br>
			4: print()<br>
			5: exit()<br>
			Enter your choice: 1<br>
			Enter name: Hui Siu Cheung<br>
			Enter tel: 12345678<br>
			Enter id: 11<br>
			Enter salary: 123.45<br>
			Enter name: Kenny B<br>
			Enter tel: 23456789<br>
			Enter id: 12<br>
			Enter salary: 1234.45<br>
			Enter name: #<br>
			Enter your choice: 4<br>
			The current employee list:<br>
			Hui Siu Cheung 12345678 11 123.45<br>
			Kenny B 23456789 12 1234.45<br>
			Enter your choice: 2<br>
			Enter search name: Kenny B<br>
			Employee found at index location: 1<br>
			Kenny B 23456789 12 1234.45<br>
			Enter your choice: 5<br>
			<br>
			<bold>(3) Test Case 3:</bold><br>
			Select one of the following options:<br>
			1: readin()<br>
			2: search()<br>
			3: addEmployee()<br>
			4: print()<br>
			5: exit()<br>
			Enter your choice: 1<br>
			Enter name: Hui Siu Cheung<br>
			Enter tel: 12345678<br>
			Enter id: 11<br>
			Enter salary: 123.45<br>
			Enter name: Kenny B<br>
			Enter tel: 23456789<br>
			Enter id: 12<br>
			Enter salary: 1234.45<br>
			Enter name: #<br>
			Enter your choice: 4<br>
			The current employee list:<br>
			Hui Siu Cheung 12345678 11 123.45<br>
			Kenny B 23456789 12 1234.45<br>
			Enter your choice: 2<br>
			Enter search name: Kenny BB<br>
			Name not found!<br>
			Enter your choice: 5<br>
			<br>
			<bold>(4) Test Case 4:</bold><br>
			Select one of the following options:<br>
			1: readin()<br>
			2: search()<br>
			3: addEmployee()<br>
			4: print()<br>
			5: exit()<br>
			Enter your choice: 1<br>
			Enter name: Hui Siu Cheung<br>
			Enter tel: 12345678<br>
			Enter id: 11<br>
			Enter salary: 123.45<br>
			Enter name: Kenny B<br>
			Enter tel: 23456789<br>
			Enter id: 12<br>
			Enter salary: 1234.45<br>
			Enter name: #<br>
			Enter your choice: 4<br>
			The current employee list:<br>
			Hui Siu Cheung 12345678 11 123.45<br>
			Kenny B 23456789 12 1234.45<br>
			Enter your choice: 3<br>
			Enter new name: Kenny Tan<br>
			Enter tel: 12344321<br>
			Enter id: 13<br>
			Enter salary: 2345.67<br>
			Added at position: 2<br>
			Enter your choice: 4<br>
			The current employee list:<br>
			Hui Siu Cheung 12345678 11 123.45<br>
			Kenny B 23456789 12 1234.45<br>
			Kenny Tan 12344321 13 2345.67<br>
			Enter your choice: 5
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
#define MAX 100

typedef struct {
	char name[40];
	char telno[40];
	int id;
	double salary;
} Employee;

void printEmp(Employee *emp, int size);
int readin(Employee *emp);
int search(Employee *emp, int size, char *target);
int addEmployee(Employee *emp, int size, char *target);

int main(){
	Employee emp[MAX];
	char name[40], *p;
	int size, choice, result;

	printf("Select one of the following options: \n");
	printf("1: readin() \n");
	printf("2: search() \n");
	printf("3: addEmployee() \n");
	printf("4: print() \n");
	printf("5: exit() \n");
	do {
		printf("Enter your choice: \n");
		scanf("%d", &choice);
		switch (choice) {
			case 1:
				size = readin(emp);
				break;
			case 2:
				printf("Enter search name: \n");
				scanf("\n");
				fgets(name, 40, stdin);
				if (p=strchr(name,'\n')) *p = '\0';
				result = search(emp,size,name);
				if (result != 1)
				printf ("Name not found! \n");
				break;
			case 3:
				printf("Enter new name: \n");
				scanf("\n");
				fgets(name, 40, stdin);
				if (p=strchr(name,'\n')) *p = '\0';
				result = search(emp,size,name);
				if (result != 1)
					size = addEmployee(emp, size, name);
				else
					printf("The new name has already existed in the database\n");
				break;
			case 4:
				printEmp(emp, size);
				break;
			default:
				break;
		}
	} while (choice < 5);
	return 0;
}

void printEmp(Employee *emp, int size){
	int i;
	printf("The current employee list: \n");
	if (size==0)
		printf("Empty array\n");
	else{
	for (i=0; i<size; i++)
		printf("%s %s %d %.2f\n",emp[i].name,emp[i].telno,emp[i].id, emp[i].salary);
	}
}

int readin(Employee *emp){
	int i=0;

	getchar();
	printf("Enter name:\n");
	gets(emp[0].name);

	while(strcmp(emp[i].name, "#" ) != 0){
        printf("Enter tel:\n");
        gets(emp[i].telno);
        printf("Enter id:\n");
        scanf("%d", &emp[i].id);
        printf("Enter salary:\n");
        scanf("%lf", &emp[i].salary);
        i++;
        getchar();
        printf("Enter name:\n");
        gets(emp[i].name);
	}
	return i;
}

int search(Employee *emp, int size, char *target){
	int i = 0;

	if(size > MAX)
		return 0;

	for(i = 0; i < size; i++){
    	if(strcmp(emp[i].name, target) == 0){
        	printf("Employee found at index location: %d\n", i);
        	printf("%s %s %d %.2lf\n", emp[i].name, emp[i].telno, emp[i].id, emp[i].salary);
        	return 1;
       }
	}
	return 0;
}

int addEmployee(Employee *emp, int size, char *target){
	if(size > MAX)
		size = 0;
	else if(size == MAX){
		printf("Database is full");
		return size;
	} else {
		strcpy(emp[size].name, target);
		printf("Enter tel:\n");
		gets(emp[size].telno);
		printf("Enter id:\n");
		scanf("%d", &emp[size].id);
		printf("Enter salary:\n");
		scanf("%lf", &emp[size].salary);
		printf("Added at position: %d\n", size);
		return ++size;
	}
}
```