---
title: Data Structures and Algorithms
pageTitle: Coalesced Hashing
---

## Coalesced Hashing

<span class="tags"><a href="#">Hashing</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Coalesced hashing is a combination of closed addressing and linear probing. Each slot is not only storing the key, but also the link (index) to the next slot. The structure of hash slots is given below.
<br><br>
<span class="functions">
enum Marker {EMPTY , USED };<br>
<br>
typedef struct _slot {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int key;<br>
&nbsp;&nbsp;&nbsp;&nbsp;enum Marker indicator;<br>
&nbsp;&nbsp;&nbsp;&nbsp;int next;<br>
} HashSlot;
</span>
<br><br>

**The insertion and searching function prototypes are given as follows:**

<span class="functions">
int HashInsert (int key , HashSlot hashTable []) ;<br>
int HashFind ( int key , HashSlot hashTable []) ;
</span>
<br><br>
Both functions' return value is an index of the slot where the key is inserted and searched respectively.<br>
For insertion function, inserting a duplicate key will return -1. Return value larger than the table size implies that the table is full. For searching function, finding an non-existing key will return -1.<br>
<br>
<img src = "{{ '/images/hashing-coalesced-hashing.JPG' | url }}" class="diagrams">
<br>

```c
#include <stdio.h>
#include <stdlib.h>

#define TABLESIZE 37
#define PRIME     13

enum Marker {EMPTY,USED};

typedef struct _slot{
    int key;
    enum Marker indicator;
    int next;
} HashSlot;

int HashInsert(int key, HashSlot hashTable[]);
int HashFind(int key, HashSlot hashTable[]);

int hash(int key)
{
    return (key % TABLESIZE);
}

int main()
{
    int opt;
    int i;
    int key;
    int index;
    HashSlot hashTable[TABLESIZE];

    for(i=0;i<TABLESIZE;i++){
        hashTable[i].next = -1;
        hashTable[i].key = 0;
        hashTable[i].indicator = EMPTY;
    }

    printf("============= Hash Table ============\n");
    printf("|1. Insert a key to the hash table  |\n");
    printf("|2. Search a key in the hash table  |\n");
    printf("|3. Print the hash table            |\n");
    printf("|4. Quit                            |\n");
    printf("=====================================\n");

    printf("Enter selection: ");
    scanf("%d",&opt);
    while(opt>=1 && opt <=3){
        switch(opt){
        case 1:
            printf("Enter a key to be inserted:\n");
            scanf("%d",&key);
            index = HashInsert(key,hashTable);
            if(index <0)
                printf("Duplicate key\n");
            else if(index < TABLESIZE)
                printf("Insert %d at index %d\n",key, index);
            else
                printf("Table is full.\n");
            break;
        case 2:
            printf("Enter a key for searching in the HashTable:\n");
            scanf("%d",&key);
            index = HashFind(key, hashTable);

            if(index!=-1)
                printf("%d is found at index %d.\n",key,index);
            else
                printf("%d is not found.\n",key);
            break;

        case 3:
            printf("index:\t key \t next\n");
            for(i=0;i<TABLESIZE;i++) printf("%d\t%d\t%d\n",i, hashTable[i].key,hashTable[i].next);
            break;
        }
        printf("Enter selection: ");
        scanf("%d",&opt);
    }
    return 0;
}

int HashInsert(int key, HashSlot hashTable[])
{
    int index, temp; 
    int count = 0;
    index = hash(key);

    if(hashTable[index].indicator == EMPTY) {
        hashTable[index].key = key;
        hashTable[index].indicator = USED;
        return index;
    } else {
        if (hashTable[index].key == key)
            return -1;

        while(hashTable[index].next != -1){
            if(hashTable[index].key == key)
                return -1;
            index = hashTable[index].next;
        }

        if(hashTable[index].key == key) {
            return -1;
        }
        temp = index;
        index +=1;
        index = hash(index);


        while(hashTable[index].indicator != EMPTY) {
            if(count > TABLESIZE) {
                return count;
            }
            index = hash(++index);
            count++;
        }
        hashTable[index].key = key;
        hashTable[index].indicator = USED;
        hashTable[temp].next = index;
        return index;
    }
}

int HashFind(int key, HashSlot hashTable[])
{
    int index = hash(key);
    // while(hashTable[i].next != NULL){
    while(hashTable[index].next != -1){
        // printf("check");
        if(hashTable[index].indicator == USED && hashTable[index].key == key) {
            return index;
        }
        index = hashTable[index].next; 
    }

    if(hashTable[index].indicator == USED && hashTable[index].key == key) {
        return index;
    }
    return -1;
}
```