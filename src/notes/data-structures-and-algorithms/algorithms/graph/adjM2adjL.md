---
title: Data Structures and Algorithms
pageTitle: adjM2adjL()
---

## adjM2adjL()

<span class="tags"><a href="#">Graph</a></span>
<span class="tags"><a href="#">Lab</a></span>

<hr>

Write a function adjM2adjL() to convert an adjacency matrix to an adjacency list.
<br><br>

**The structure of a graph is given below:**

<span class="functions">
enum GraphType { ADJ_MATRIX , ADJ_LIST }; // Types of Graph Representation<br>
<br>
typedef struct _listnode {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int vertex;<br>
&nbsp;&nbsp;&nbsp;&nbsp;struct _listnode * next;<br>
} ListNode;<br>
<br>
union GraphForm {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int ** matrix;<br>
&nbsp;&nbsp;&nbsp;&nbsp;ListNode ** list;<br>
};<br>
<br>
typedef struct _graph {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int V;<br>
&nbsp;&nbsp;&nbsp;&nbsp;int E;<br>
&nbsp;&nbsp;&nbsp;&nbsp;enum GraphType type;<br>
&nbsp;&nbsp;&nbsp;&nbsp;union GraphForm adj;<br>
} Graph;
</span>
<br><br>
the vertices are named from 1 to |V|.
<br><br>

**The function prototype is given as follows:**

<span class="functions">void adjM2adjL ( Graph *g);</span>
<br><br>

```c
#include <stdio.h>
#include <stdlib.h>

enum GraphType {ADJ_MATRIX, ADJ_LIST}; // Types of Graph Representation

typedef struct _listnode
{
    int vertex;
	struct _listnode *next;
} ListNode;

union GraphForm{
    int **matrix;
    ListNode **list;
};

typedef struct _graph{
    int V;
    int E;
    enum GraphType type;
    union GraphForm adj;
}Graph;

void printGraphMatrix(Graph );
void adjM2adjL(Graph *);
void adjL2adjM(Graph *);
void printGraphList(Graph );
void calDegreeV(Graph,int *);
void printDegreeV(int *,int );

int main()
{
    Graph g;
    int i,j;

    int* degreeV;

    printf("Enter the number of vertices:\n");
    scanf("%d",&g.V);

    g.E = 0;
    g.adj.matrix = (int **)malloc(g.V*sizeof(int *));
    for(i=0;i<g.V;i++)
        g.adj.matrix[i] = (int *)malloc(g.V*sizeof(int));

    for(i=0;i<g.V;i++)
        for(j=0;j<g.V;j++)
            g.adj.matrix[i][j] = 0;
    g.type = ADJ_MATRIX;

    degreeV = (int *) malloc(g.V*sizeof(int));
    for(i=0;i<g.V;i++)
        degreeV[i]=0;

    int V1, V2;
    printf("Enter two vertices which are adjacent to each other:\n");
    while(scanf("%d %d",&V1,&V2)==2)
    {
        if(V1>0 && V1<=g.V && V2>0 && V2<=g.V)
        {
            g.adj.matrix[V1-1][V2-1] = 1;
            g.adj.matrix[V2-1][V1-1] = 1;
            g.E++;
        }
        else
            break;
        printf("Enter two vertices which are adjacent to each other:\n");
    }

    calDegreeV(g,degreeV);

    printGraphMatrix(g);
    printDegreeV(degreeV,g.V);

    adjM2adjL(&g);

    calDegreeV(g,degreeV);

    printGraphList(g);
    printDegreeV(degreeV,g.V);

    adjL2adjM(&g);
    printGraphMatrix(g);

    return 0;
}

void printGraphMatrix(Graph g)
{
    int i,j;
    if(g.type == ADJ_LIST) {printf("Error"); return;}

    for(i=0;i<g.V;i++){
        for(j=0;j<g.V;j++)
            printf("%d\t",g.adj.matrix[i][j]);
        printf("\n");
    }

}

void adjM2adjL(Graph *g)
{
    int i,j;
    ListNode **list;
    ListNode *temp;

    if(g->type == ADJ_LIST) {printf("Error"); return;}
    if(g->V<=0){printf("Empty graph!"); return;}

    list = (ListNode **) malloc(g->V*sizeof(ListNode *));
    for(i=0;i<g->V;i++)
        list[i] = NULL;

    for(i=0;i<g->V;i++){
        for(j=0;j<g->V;j++){
            if(g->adj.matrix[i][j]==1){
                if(list[i]==NULL){
                    list[i] = (ListNode *)malloc(sizeof(ListNode));
                    list[i]->vertex = j+1;
                    list[i]->next = NULL;
                    temp = list[i];
                }
                else{
                    temp->next = (ListNode *)malloc(sizeof(ListNode));
                    temp->next->vertex = j+1;
                    temp->next->next =NULL;
                    temp = temp->next;
                }
            }
        }
    }

    g->type = ADJ_LIST; //change representation form

    //free adjMatrix
    for(i=0;i<g->V;i++)
        free(g->adj.matrix[i]);
    free(g->adj.matrix);

    g->adj.list = list;

}

void adjL2adjM(Graph *g){
    int i,j;
    ListNode *temp;

    if(g->type == ADJ_MATRIX) {printf("Error"); return;}
    if(g->V<=0){printf("Empty graph!"); return;}

    int ** mat = (int **)malloc(g->V*sizeof(int *));
    for(i=0;i<g->V;i++)
        mat[i] = (int *)malloc(g->V*sizeof(int));

    for(i=0;i<g->V;i++)
        for(j=0;j<g->V;j++)
            mat[i][j] = 0;

    for(i=0;i<g->V;i++){
        temp = g->adj.list[i];
        while(temp!=NULL){
            mat[i][(temp->vertex)-1]=1;
            temp = temp->next;
        }
    }

    g->type = ADJ_MATRIX;

    ListNode *next;
    for(i=0;i< g->V;i++){
        temp = g->adj.list[i];
        while(temp!=NULL)
        {
            next = temp->next;
            free(temp);
            temp = next;
        }
    }
    free(g->adj.list);

    g->adj.matrix = mat;

}

void printGraphList(Graph g){
    int i;
    ListNode* temp;

    if(g.type == ADJ_MATRIX) {printf("Error"); return;}

    for(i=0;i<g.V;i++)
    {
        printf("%d:\t",i+1);
        temp = g.adj.list[i];
        while(temp!=NULL){
            printf("%d -> ",temp->vertex);
            temp = temp->next;
        }
        printf("\n");
    }
}

void calDegreeV(Graph g, int *degreeV)
{
    int i,j;
    ListNode *temp = NULL;

    if(g.type == ADJ_MATRIX){
        for(i=0;i<g.V;i++){
            degreeV[i] = 0;
            for(j=0;j<g.V;j++){
                degreeV[i] += g.adj.matrix[i][j];
            }
        }
    }
    else{
        for(i=0;i<g.V;i++){
            degreeV[i]=0;
            ListNode *temp = g.adj.list[i];
            while(temp != NULL){
                degreeV[i]++;
                temp = temp->next;
            }
        }
    }
}

void printDegreeV(int *degreeV,int V)
{
    int i;
    for(i=0;i<V;i++)
        printf("%d: %d degree\n",i+1,degreeV[i]);
}

```