---
title: Data Structures and Algorithms
pageTitle: Closed Address Hashing
---

## Closed Address Hashing

<span class="tags"><a href="#">Hashing</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Implement a closed addressing hash table to perform insertion and deletion by using a doubly linked list below.
<br><br>
<span class="functions">
typedef struct _listnode {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int key;<br>
&nbsp;&nbsp;&nbsp;&nbsp;struct _listnode * next;<br>
&nbsp;&nbsp;&nbsp;&nbsp;struct _listnode * pre;<br>
} ListNode;<br>
<br>
typedef struct _linkedlist {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int size;<br>
&nbsp;&nbsp;&nbsp;&nbsp;ListNode * head;<br>
} HashTableNode;<br>
<br>
typedef struct _hashTable {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int hSize;<br>
&nbsp;&nbsp;&nbsp;&nbsp;int nSize;<br>
&nbsp;&nbsp;&nbsp;&nbsp;HashTableNode * Table;<br>
} HashTable;
</span>
<br><br>

**The following utility functions are provided. The details can refer to the given template:**

<span class="functions">ListNode * HashSearch ( HashTable , int );</span>
<br><br>

**The insertion and deletion function prototypes are given as follows:**

<span class="functions">
int HashInsert ( HashTable * Q1 , int key );<br>
int HashDelete ( HashTable * Q1 , int key );
</span>
<br><br>
Both functions' return value indicates success (1) or failure (0).
<br><br>

```c
#include <stdio.h>
#include <stdlib.h>

#define LOAD_FACTOR 3

typedef struct _listnode{
    int key;
    struct _listnode *next;
    struct _listnode *pre;
} ListNode;

typedef struct _linkedlist{
   int size;
   ListNode *head;
} HashTableNode;

typedef struct _hashTable{
   int hSize;
   int nSize;
   HashTableNode *Table;
} HashTable;

int Hash(int key,int hSize);

ListNode* HashSearch(HashTable, int);
int HashInsert(HashTable *, int);
int HashDelete(HashTable *, int);

//In Practice, we will not do it
void HashPrint(HashTable);

int main()
{
    int opt;
    int size;

    int i;
    int key;

    //Create a HashTable
    HashTable Q1;

    printf("============= Hash Table ============\n");
    printf("|1. Create a hash table             |\n");
    printf("|2. Insert a key to the hash table  |\n");
    printf("|3. Search a key in the hash table  |\n");
    printf("|4. Delete a key from the hash table|\n");
    printf("|5. Print the hash table            |\n");
    printf("|6. Quit                            |\n");
    printf("=====================================\n");

    printf("Enter selection: ");
    scanf("%d",&opt);
    while(opt>=1 && opt <=5){
        switch(opt){
        case 1:
            printf("Enter number of data to be inserted:\n");
            scanf("%d",&size);

            Q1.hSize = (int)size/ LOAD_FACTOR;
            Q1.nSize = 0;

            Q1.Table = (HashTableNode *) malloc(sizeof(HashTableNode)*(Q1.hSize));

            for(i=0;i<Q1.hSize;i++){
                Q1.Table[i].head = NULL;
                Q1.Table[i].size = 0;
            }
            printf("HashTable is created.\n");
            break;
        case 2: //Insertion
            printf("Enter a key to be inserted:\n");
            scanf("%d",&key);
            if(HashInsert(&Q1,key))
                printf("%d is inserted.\n",key);
            else
                printf("%d is a duplicate. No key is inserted.\n",key);
            break;
        case 3: //Search
            printf("Enter a key for searching in the HashTable:\n");
            scanf("%d",&key);
            ListNode* node = HashSearch(Q1, key);

            if(node!=NULL)
                printf("%d is found.\n",key);
            else
                printf("%d is not found.\n",key);
            break;
        case 4: //Deletion
            printf("Enter a key to be deleted:\n");
            scanf("%d",&key);
            if(HashDelete(&Q1,key))
                printf("%d is deleted.\n",key);
            else
                printf("%d is not existing.\n",key);
            break;
        case 5:
            HashPrint(Q1);
            break;
        }

    printf("Enter selection: ");
    scanf("%d",&opt);
    }

    for(i=0;i<Q1.hSize;i++)
    {
        while(Q1.Table[i].head)
        {
            ListNode *temp;
            temp = Q1.Table[i].head;
            Q1.Table[i].head = Q1.Table[i].head->next;
            free(temp);
        }
    }
    free(Q1.Table);

    return 0;
}



int HashInsert(HashTable* Q1Ptr, int key)
{
    int index;
    ListNode *newNode;

    if(HashSearch(*Q1Ptr, key)!=NULL)   //duplicate
        return 0;

    if(Q1Ptr->hSize!=0)
        index = Hash(key,Q1Ptr->hSize);

    if(Q1Ptr->Table[index].head == NULL){
        newNode = (ListNode *) malloc(sizeof(ListNode));

        newNode->key = key;
        newNode->next = NULL;
        newNode->pre = NULL;
        Q1Ptr->Table[index].head = newNode;

        Q1Ptr->Table[index].size++;
        Q1Ptr->nSize++;
        return 1;
    }
        newNode = (ListNode *) malloc(sizeof(ListNode));
        newNode->key = key;
        newNode->next= Q1Ptr->Table[index].head;
        Q1Ptr->Table[index].head = newNode;
        newNode->pre = NULL;

        Q1Ptr->Table[index].head->next->pre = Q1Ptr->Table[index].head;
        Q1Ptr->Table[index].size++;
        Q1Ptr->nSize++;
        return 1; //insertion is done successfully
}

int HashDelete(HashTable* Q1Ptr, int key)
{
      int index;
      ListNode *temp, *cur;
      index = Hash(key, Q1Ptr->hSize); 
      if(HashSearch(*Q1Ptr, key) == NULL)
            return 0;

      // first element check
      if(Q1Ptr->Table[index].head->key == key){
        // only 1 node LL 
        if(Q1Ptr->Table[index].head->next == NULL){
            free(Q1Ptr->Table[index].head);
            Q1Ptr->Table[index].head = NULL;
            return 1;
        // >1 node LL
        }else{
            temp = (ListNode *) malloc(sizeof(ListNode));
            temp = Q1Ptr->Table[index].head->next;
            free(Q1Ptr->Table[index].head);
            Q1Ptr->Table[index].head = temp;
            return 1;
        }
      }

      cur = (ListNode *) malloc(sizeof(ListNode));
      cur = Q1Ptr->Table[index].head;
      while(cur->next != NULL)
      {
            if(cur->key == key)   
            {
                  temp = cur;

                  cur->pre->next = temp->next;
                  cur->next->pre = temp->pre;

                  free(temp);
                  Q1Ptr->Table[index].size--;
                  return 1;
            }
            cur = cur->next;
      }
      if(cur->key == key){
        cur->pre->next = NULL;
        free(cur);
        Q1Ptr->Table[index].size--;
        return 1;
      }
}

int Hash(int key,int hSize)
{
    return key%hSize;
}

ListNode* HashSearch(HashTable Q1, int key)
{
    int index;

    ListNode *temp;

    if(Q1.hSize != 0)
      index = Hash(key,Q1.hSize);
    else
      return NULL;

    temp = Q1.Table[index].head;
    while(temp !=NULL){
        if(temp->key == key)
            return temp;
        temp = temp->next;
    }

    return NULL;
}

void HashPrint(HashTable Q1)
{
    int i;
    ListNode *temp;
    for(i=0;i<Q1.hSize;i++)
    {
        temp =Q1.Table[i].head;
        printf("%d:  ",i);
        while(temp !=NULL)
        {
            printf("%d -> ", temp->key);
            temp = temp->next;
        }
        printf("\n");
    }
}
```