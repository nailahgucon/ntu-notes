---
title: Intro to Computational Thinking and Programming - ComputeSalary
pageTitle: ComputeSalary
---

## ComputeSalary

<span class="tags"><a href="#">Pointers</a></span>

<hr>

Write a C program that determines the gross pay for each employee in a company. The company
pays “straight-time” for the first 160 hours worked by each employee for four weeks and pays
“time-and-a-half” for all hours worked in excess of 160 hours. You are given a list of employee
Ids (an integer), the number of hours each employee worked for the four weeks, and the hourly
rate of each employee. The program should input this information for each employee, then
determine and display the employee’s gross pay. The sentinel value of –1 is used for the employee
id to indicate the end of input. Your program should include three functions, apart from the main()
function, to handle the input, and the computation of the gross pay. The function prototypes for the
functions are given as follows:
<br><br>
<span class="functions">void readInput(int *id, int *noOfHours, int *payRate);</span>

<span class="functions">double computeSalary1(int noOfHours, int payRate);</span>

<span class="functions">void computeSalary2(int noOfHours, int payRate, double *grossPay);</span>
<br><br>

The function **computeSalary1()** uses call by value for returning the result to the calling function. <br>
The function **computeSalary2()** uses call by reference to pass the result through the pointer
parameter, grossPay, to the caller.
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
            Enter ID (-1 to end): 11<br>
            Enter number of hours: 155<br>
            Enter hourly pay rate: 8<br>
            computeSalary1(): ID 11 grossPay 1240.00<br>
            computeSalary2(): ID 11 grossPay 1240.00<br>
            Enter ID (-1 to end): 12<br>
            Enter number of hours: 165<br>
            Enter hourly pay rate: 8<br>
            computeSalary1(): ID 12 grossPay 1340.00<br>
            computeSalary2(): ID 12 grossPay 1340.00<br>
            Enter ID (-1 to end): -1<br>
            <br>
            <bold>(2) Test Case 2:</bold><br>
            Enter ID (-1 to end): 11<br>
            Enter number of hours: 155<br>
            Enter hourly pay rate: 8<br>
            computeSalary1(): ID 11 grossPay 1240.00<br>
            computeSalary2(): ID 11 grossPay 1240.00<br>
            Enter ID (-1 to end): 12<br>
            Enter number of hours: 160<br>
            Enter hourly pay rate: 8<br>
            computeSalary1(): ID 12 grossPay 1280.00<br>
            computeSalary2(): ID 12 grossPay 1280.00<br>
            Enter ID (-1 to end): 13<br>
            Enter number of hours: 200<br>
            Enter hourly pay rate: 8<br>
            computeSalary1(): ID 13 grossPay 1760.00<br>
            computeSalary2(): ID 13 grossPay 1760.00<br>
            Enter ID (-1 to end): -1<br>
            <br>
            <bold>(3) Test Case 3:</bold><br>
            Enter ID (-1 to end): 11<br>
            Enter number of hours: 165<br>
            Enter hourly pay rate: 8<br>
            computeSalary1(): ID 11 grossPay 1340.00<br>
            computeSalary2(): ID 11 grossPay 1340.00<br>
            Enter ID (-1 to end): -1
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
void readInput(int *id, int *noOfHours, int *payRate);
double computeSalary1(int noOfHours, int payRate);
void computeSalary2(int noOfHours, int payRate, double *grossPay);

int main(){
    int id = -1, noOfHours, payRate;
    double grossPay;
    readInput(&id, &noOfHours, &payRate);
    while (id != -1) {
        printf("computeSalary1(): ");
        grossPay = computeSalary1(noOfHours, payRate);
        printf("ID %d grossPay %.2f \n", id, grossPay);
        printf("computeSalary2(): ");
        computeSalary2(noOfHours, payRate, &grossPay);
        printf("ID %d grossPay %.2f \n", id, grossPay);
        readInput(&id, &noOfHours, &payRate);
    }
    return 0;
}

void readInput(int *id, int *noOfHours, int *payRate){
  printf("Enter ID (-1 to end): \n");
  scanf("%d", id);

  if(*id == -1)
   return;

  printf("Enter number of hours: \n");
  scanf("%d", noOfHours);
  printf("Enter hourly pay rate: \n");
  scanf("%d", payRate);

  if(*noOfHours < 0 || *payRate < 0)
   *id = -1;
}

double computeSalary1(int noOfHours, int payRate){
if(noOfHours <= 160)
   return noOfHours * payRate;
  else
   return (160 * payRate) + ((noOfHours-160) * (payRate * 1.5));
}

void computeSalary2(int noOfHours, int payRate, double *grossPay){
if(noOfHours <= 160)
   *grossPay = noOfHours * payRate;
  else
   *grossPay = (160 * payRate) + ((noOfHours-160) * (payRate * 1.5));
}
```