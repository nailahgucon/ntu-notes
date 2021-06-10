---
title: Data Structures and Algorithms
pageTitle: nQueens()
---

## nQueens()

<span class="tags"><a href="#">Graph</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a function, <span class="functions">nQueens()</span>, to print out all the possible solutions of the N-queen problem.
<br><br>

**The function prototype is given as follows:**

<span class="functions">int nQueens ( int ** board , int N, int col );</span>
<br><br>

**The number of possible solutions to different n are:**

<span class="functions">
If n = 4 : number of possible solutions = 2<br>
If n = 5 : number of possible solutions = 10<br>
If n = 6 : number of possible solutions = 4<br>
If n = 7 : number of possible solutions = 40<br>
If n = 8 : number of possible solutions = 92<br>
If n = 10 : number of possible solutions = 724<br>
If n = 12 : number of possible solutions = 14200<br>
</span>

There is no known formula for the exact number of solutions but the grown rate is extremely high.

```c
#include <stdio.h>
#include <stdlib.h>

int nQueens(int** board, int N, int col);
int isSafe(int** board,int N, int row, int col);
void printSolution(int** board, int N);

int main()
{
    int **board;
    int BSize;

    int i,j;

    printf("Enter the size of chessBoard:\n");
    scanf("%d",&BSize);

    board = (int **)malloc(BSize*sizeof(int *));
    for(i=0;i<BSize;i++)
        board[i] = (int *)malloc(BSize*sizeof(int));

    for(i=0;i<BSize;i++)
       for(j=0;j<BSize;j++)
           board[i][j] = 0;

    nQueens(board, BSize, 0);

    return 0;
}

int nQueens(int** board, int BSize, int col)
{
    if (col == BSize){
        printSolution(board, BSize);
        return 1;
    }

    int i;

    for (i = 0; i < BSize; i++) { // check row by row in the (col)^th column
        // Safe to place
        if (isSafe(board,BSize, i, col)) {
            // Place a queen in this square
            board[i][col] = 1;

           // recursive the next column placement
            nQueens(board,BSize, col + 1);

            //Delete the queen - Backtrack
            board[i][col] = 0;
        }
    }

    return 0;
}

//Safe checking
int isSafe(int** board,int BSize, int row, int col)
{
    int i, j;

    // Horicatal check
    for (i = 0; i < col; i++)
        if (board[row][i])
            return 0;

    // Upper left diagonal check
    for (i = row, j = col; i >= 0 && j >= 0; i--, j--)
        if (board[i][j])
            return 0;

    // Lower left diagonal check
    for (i = row, j = col; j >= 0 && i < BSize; i++, j--)
        if (board[i][j])
            return 0;

    return 1;
}

void printSolution(int** board, int BSize)
{
    int i,j;
    for (i = 0; i < BSize; i++) {
        for (j = 0; j < BSize; j++){
            if(board[i][j]==1)
                printf(" Q ");
            else
                printf(" + ");
        }
        printf("\n");
    }
    printf("\n");
}

```