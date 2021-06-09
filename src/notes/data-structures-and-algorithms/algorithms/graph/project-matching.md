---
title: Data Structures and Algorithms
pageTitle: Project Matching
---

## Project Matching

<span class="tags"><a href="#">Graph</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

In CX4321, each student will be assigned to a project and a mentor. Students has their own preferences but each project or mentor can only be assigned to one of the students. The course coordinator needs an algorithm to maximize the matching between students and projects and between students and mentors.
<br><br>

**Input:** First line is number of students, **S**, number of projects, **P** and number of mentors, **M**. The following **S** lines indicate the corresponding students' The number of preference projects, the number of preference mentors, the IDs of preference projects [1,P] and the IDs of preference mentors, [1,M].

**Output:** The maximum number of matches
<br><br>

**Sample Case**:<br>
<span class="functions">
Input:<br>
4&nbsp;&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;&nbsp;3<br>
2&nbsp;&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;&nbsp;1<br>
2&nbsp;&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;2<br>
2&nbsp;&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;2<br>
2&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;&nbsp;3<br>
<br>
Output:<br>
3
</span>
<br><br>

In the given input, we have 4 students, 3 projects and 3 mentors (first line). Student 1 likes project 1 and project 3. Student 1 prefers to mentor 2 and mentor 1 (second line). The corresponding bipartite graph is as follow:<br><br>
<img src = "{{ '/images/graph-project-matching.JPG' | url }}" class="diagrams">
<br><br>

**Figure 7.1** <br>
The graph of the given sample case: 

The Project indicates as P*i*, the Student indicates as S*j*, and the Mentor indicates as M*k*.
<br><br>
*Hint: You may not be able to use this graph to solve the problem directly. Think about some extreme cases like all students selected the same project and the same mentor.*

<br>

**To assist in testing, <a href="https://github.com/nailahgucon/ntu-notes-files/blob/main/algorithms-extra/random-number-generator.ipynb" target="_blank">click here</a> to be redirected to my github to download a random input generator.**
<br><br>

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct _listnode
{
    int vertex;
    struct _listnode *next;
} ListNode;
typedef ListNode StackNode;

// typedef struct _graph{
//     int V;
//     int E;
//     ListNode **list;
// }Graph;

typedef struct _graph{
    int V;
    int E;
    ListNode **list;
    int **matrix; // add on matrix
}Graph;

typedef ListNode QueueNode;

typedef struct _queue{
    int size;
    QueueNode *head;
    QueueNode *tail;
} Queue;

typedef struct _stack
{
    int size;
    StackNode *head;
} Stack;

void insertAdjVertex(ListNode** AdjList,int vertex);
void removeAdjVertex(ListNode** AdjList,int vertex);
int matching(Graph g);

void enqueue(Queue *qPtr, int item);
int dequeue(Queue *qPtr);
int getFront(Queue q);
int isEmptyQueue(Queue q);
void removeAllItemsFromQueue(Queue *qPtr);
void printQ(QueueNode *cur);
//////STACK///////////////////////////////////////////
void push(Stack *sPtr, int vertex);
int pop(Stack *sPtr);
int peek(Stack s);
int isEmptyStack(Stack s);
void removeAllItemsFromStack(Stack *sPtr);
//////////////////////////////////
int BFS_FF(Graph g, int init, int target);

int main()
{
    int Prj, Std, Mtr; 
    int noOfProjects,noOfMentors;
    int V_total, foundmatches, e, i, j; 
    int src = 1;
    int sink = 1;

    scanf("%d %d %d", &Std, &Prj, &Mtr);
    // printf("%d %d %d", Std, Prj, Mtr);

    // need to add std twice
    // V_total =  Prj + Std + Mtr; <- error
    V_total =  Prj + Std + Std + Mtr;

    Graph graph;
    graph.V = V_total + src + sink;
    // memory allocation (from lab)
    graph.matrix = (int **)malloc(graph.V*sizeof(int *));

    for(i = 0; i < graph.V; i++){
        graph.matrix[i] = (int *)malloc(graph.V*sizeof(int));
    }

    for(i = 0; i < graph.V; i++) {
        for (j = 0; j < graph.V; j++){
            graph.matrix[i][j] = 0;
        }
    }

    // based on student do a for loop
    i = 1;
    while(i <= Std){
        scanf("%d %d", &noOfProjects, &noOfMentors);

        //printf("new input: %d %d", &noOfProjects, &noOfMentors)
        //printf("og input: %d %d", Prj, Mtr)

        // checking input pref cannot exceed actual
        if (noOfProjects > Prj)
            return 0;

        while(noOfProjects != 0) {
            scanf("%d", &e);
            // printf("proj edge: %d", e);
            graph.matrix[e][Prj + i] = 1;
            noOfProjects--;
        }

        if (noOfMentors > Mtr)
            return 0;

        while(noOfMentors != 0)
        {
            scanf("%d",&e);
            // printf("mtr edge: %d", e);
            graph.matrix[Prj + Std + i][Prj + Std + Std + e] = 1;
            noOfMentors--;
        }
        i++;
    }

    j = Prj + Std + Std + src;
    for (; j < Prj + Std + Std + Mtr + src; j++)
        graph.matrix[j][graph.V-1] = 1;

    j = Prj + src;
    for(;j < Prj + Std + src; j++){
        graph.matrix[j][j + Std] = 1;
    }

    for (j = src; j < Prj + src; j++)
        graph.matrix[0][j] = 1;

    foundmatches = matching(graph);
    printf("%d", foundmatches);
    return 0;
}

int matching(Graph g)
{
    Graph graph;
    graph = g;
    int noOfMatch = 0;

    while((BFS_FF(graph, 0, graph.V - 1)) == 1)
        noOfMatch = noOfMatch + 1;
        // printf("%d", noOfMatch);

    return noOfMatch;
}

int BFS_FF(Graph g, int init, int target)
{
    int trackpath[g.V]; //need this to track path
    int visited[g.V];
    int x, y, storeV;

    // bfs makes use of queue
    Queue queue;
    queue.size = 0;
    queue.head = NULL;
    queue.tail = NULL;

    //need to instatiate visited
    for(x = 0; x < g.V; x++)
        visited[x] = 0;

    //enqueue the initial
    enqueue(&queue, init);
    visited[init] = 1;

    while(!isEmptyQueue(queue))
    {
        // similar to stack peek
        storeV = getFront(queue);
        dequeue(&queue);
        
        for(x = 0; x < g.V; x++){
            if(g.matrix[storeV][x] == 1 && visited[x] != 1){
                // check if x equals to the destination
                if(x == target){
                    // printf("%d %d", x, target);
                    trackpath[x] = storeV;
                    visited[x] = 1;
                    // for (y = g.V - 1; y > 0; y++){
                    for (y = g.V - 1; y > 0; y = trackpath[y]){
                        g.matrix[y][trackpath[y]] += 1;
                        g.matrix[trackpath[y]][y] -= 1;
                    }
                    return 1;
                }
                else{
                    trackpath[x] = storeV;
                    visited[x] = 1;
                    enqueue(&queue, x);
                }
            }
        }
    }
    return 0;
}

void removeAdjVertex(ListNode** AdjList,int vertex)
{
    ListNode *temp, *preTemp;
    if(*AdjList != NULL)
    {
        if((*AdjList)->vertex ==vertex){//first node
            temp = *AdjList;
            *AdjList = (*AdjList)->next;
            free(temp);
            return;
        }
        preTemp = *AdjList;
        temp = (*AdjList)->next;
        while(temp!=NULL && temp->vertex != vertex)
        {
            preTemp= temp;
            temp = temp->next;
        }
        preTemp->next = temp->next;
        free(temp);
    }

}
void insertAdjVertex(ListNode** AdjList,int vertex)
{
    ListNode *temp;
    if(*AdjList==NULL)
    {
        *AdjList = (ListNode *)malloc(sizeof(ListNode));
        (*AdjList)->vertex = vertex;
        (*AdjList)->next = NULL;
    }
    else{
        temp = (ListNode *)malloc(sizeof(ListNode));
        temp->vertex = vertex;
        temp->next = *AdjList;
        *AdjList = temp;
    }
}
void enqueue(Queue *qPtr, int vertex) {
    QueueNode *newNode;
    newNode = malloc(sizeof(QueueNode));
    if(newNode==NULL) exit(0);

    newNode->vertex = vertex;
    newNode->next = NULL;

    if(isEmptyQueue(*qPtr))
        qPtr->head=newNode;
    else
        qPtr->tail->next = newNode;

    qPtr->tail = newNode;
    qPtr->size++;
}

int dequeue(Queue *qPtr) {
    if(qPtr==NULL || qPtr->head==NULL){ //Queue is empty or NULL pointer
        return 0;
    }
    else{
        QueueNode *temp = qPtr->head;
        qPtr->head = qPtr->head->next;
        if(qPtr->head == NULL) //Queue is emptied
            qPtr->tail = NULL;

        free(temp);
        qPtr->size--;
        return 1;
    }
}

int getFront(Queue q){
    return q.head->vertex;
}

int isEmptyQueue(Queue q) {
    if(q.size==0) return 1;
    else return 0;
}

void removeAllItemsFromQueue(Queue *qPtr)
{
    while(dequeue(qPtr));
}

void printQ(QueueNode *cur){
    if(cur==NULL) printf("Empty");

    while (cur != NULL){
        printf("%d ", cur->vertex);
        cur = cur->next;
    }
    printf("\n");
}

void push(Stack *sPtr, int vertex)
{
    StackNode *newNode;
    newNode= malloc(sizeof(StackNode));
    newNode->vertex = vertex;
    newNode->next = sPtr->head;
    sPtr->head = newNode;
    sPtr->size++;
}

int pop(Stack *sPtr)
{
    if(sPtr==NULL || sPtr->head==NULL){
        return 0;
    }
    else{
        StackNode *temp = sPtr->head;
        sPtr->head = sPtr->head->next;
        free(temp);
        sPtr->size--;
        return 1;
    }
}

int isEmptyStack(Stack s)
{
    if(s.size==0) return 1;
    else return 0;
}

int peek(Stack s){
    return s.head->vertex;
}

void removeAllItemsFromStack(Stack *sPtr)
{
    while(pop(sPtr));
}

```