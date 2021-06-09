---
title: Data Structures and Algorithms
pageTitle: Shortest Distance
---

## Shortest Distance

<span class="tags"><a href="#">Graph</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Write a function, <span class="functions">BFS()</span>, to find the shortest distance from vertex v to vertex w, in a directed graph. Vertices ranged from 1 to |V|. The distance is measured by the number of edges. If there is no path from v to w, then -1 is returned. You may assume that the input graph is always valid (no duplicate or any invalid link etc.).
<br><br>

**The function prototype is given as follows:**

<span class="functions">
int BFS ( Graph G, int v, int w);
</span>
<br>

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct _listnode
{
    int vertex;
	struct _listnode *next;
} ListNode;

typedef struct _graph{
    int V;
    int E;
    ListNode **list;
}Graph;

typedef ListNode QueueNode;

typedef struct _queue{
   int size;
   QueueNode *head;
   QueueNode *tail;
} Queue;

int BFS (Graph G, int v, int w);

void printGraphList(Graph );

// You should not change the prototypes of these functions
void enqueue(Queue *qPtr, int item);
int dequeue(Queue *qPtr);
int getFront(Queue q);
int isEmptyQueue(Queue q);
void removeAllItemsFromQueue(Queue *qPtr);

int main()
{
    Graph g;
    int i,j;
    ListNode *temp;

    printf("Enter the number of vertices:\n");
    scanf("%d",&g.V);

    g.list = (ListNode **) malloc(g.V*sizeof(ListNode *));

    for(i=0;i<g.V;i++)
        g.list[i] = NULL;

    printf("Enter two vertices which are adjacent to each other:\n");
    while(scanf("%d %d",&i,&j)==2)
    {
        i=i-1;

        if(g.list[i]==NULL){
            g.list[i] = (ListNode *)malloc(sizeof(ListNode));
            g.list[i]->vertex = j;
            g.list[i]->next = NULL;
        }
        else{
            temp = (ListNode *)malloc(sizeof(ListNode));
            temp->next = g.list[i];
            temp->vertex = j;
            g.list[i] = temp;
        }
        g.E++;
        printf("Enter two vertices which are adjacent to each other:\n");
    }
    scanf("%*c");
    printf("Enter two vertices for finding their shortest distance:\n");
    scanf("%d %d", &i, &j);

    int d = BFS(g,i,j);
	
    if(d==-1)
        printf("%d and %d are unconnected.\n",i,j);
    else
        printf("The shortest distance is %d\n",d);
    printGraphList(g);
    return 0;
}

// need to be global variables or wrong answer
int dis[500];
int vis[500];

int BFS (Graph g, int v, int w){
 // BFS uses Queue data structure for finding the shortest path 
 // DFS uses Stack data structure
 // in queue: int size; QueueNode *head; QueueNode *tail;
    int i;
    Queue queue;
    queue.head = NULL;
    queue.tail = NULL;
    queue.size = 0;

    // distance = 0 and visited = 1
    dis[v] = 0;
    vis[v] = 1;
    
    // enquece start vertex
    enqueue(&queue, v);
    // printf("%d", v);
    while (!isEmptyQueue(queue)){
        // similar to stack peek()
        int cur = getFront(queue);
        dequeue(&queue);
        // ListNode *ln = g.list[cur];
        // need to -1, if not, runtime error
        ListNode *ln = g.list[cur - 1];

        // while loop takes too long
        //while(ln != NULL){
        for (; ln != NULL; ln = ln->next){
            i = ln->vertex;
            // continue if already been visited
            if (vis[i])
                continue;
            vis[i] = 1;
            // must add 1 to dis[cur]
            dis[i] = dis[cur] + 1;
            //printf("i = %d", dis[i]);
            //printf(" cur = %d ", dis[cur])
            
            //printf("i = %d", i);
            //printf(" w = %d ", w);
            // goal reached, return dis
            if (i == w)
                return dis[i];
            // mark it visited and enqueue it
            enqueue(&queue, i);

            //ln = ln->next;
        }
    }
    return -1;
}

void printGraphList(Graph g){
    int i;
    ListNode* temp;

    for(i=0;i<g.V;i++)
    {
        printf("%d:\t",i+1);
        temp = g.list[i];
        while(temp!=NULL){
            printf("%d -> ",temp->vertex);
            temp = temp->next;
        }
        printf("\n");
    }
}

void enqueue(Queue *qPtr, int item) {
    QueueNode *newNode;
    newNode = malloc(sizeof(QueueNode));
    if(newNode==NULL) exit(0);

    newNode->vertex = item;
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
```