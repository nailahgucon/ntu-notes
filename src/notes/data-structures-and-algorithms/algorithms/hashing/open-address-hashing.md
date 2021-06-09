---
title: Data Structures and Algorithms
pageTitle: Open Address Hashing
---

## Open Address Hashing

<span class="tags"><a href="#">Hashing</a></span>
<span class="tags"><a href="#">Assignment</a></span>

<hr>

Implement an open addressing hash table by double hashing to perform insertion and deletion. The structure of hash slots is given below and a hash table with 37 hashslots is created in the main function.
<br><br>
<span class="functions">
enum Marker {EMPTY ,USED , DELETED};<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;typedef struct _slot {<br>
&nbsp;&nbsp;&nbsp;&nbsp;int key;<br>
&nbsp;&nbsp;&nbsp;&nbsp;enum Marker indicator;<br>
} HashSlot ;
</span>
<br><br>

**The hash functions are provided. The hash2() is the incremental hash function for double hashing:**

<span class="functions">
int hash1 (int key);<br>
int hash2 (int key);
</span>
<br><br>

**The insertion and deletion function prototypes are given as follows:**

<span class="functions">
int HashInsert (int key , HashSlot hashTable []);<br>
int HashDelete (int key , HashSlot hashTable []);
</span>
<br><br>
Both functions' return value is the number of key comparisons done during insertion and deletion respectively. Inserting a duplicate key will return -1. If the number of key comparisons is more than the table size, it implies that the table is full. For the deletion function, it will return -1 if the deleting key does not exist. The number of key comparisons in deletion cannot be more than table size. Once the key is deleted, you are not allowed to read it. You only can check its marker if it is a deleted slot.
<br><br>

```c
#include <stdio.h>
#include <stdlib.h>

#define TABLESIZE 37
#define PRIME     13

enum Marker {EMPTY,USED,DELETED};

typedef struct _slot{
    int key;
    enum Marker indicator;
} HashSlot;

int HashInsert(int key, HashSlot hashTable[]);
int HashDelete(int key, HashSlot hashTable[]);

int hash1(int key);
int hash2(int key);

int main()
{
    int opt;
    int i;
    int key;
    int comparison;
    HashSlot hashTable[TABLESIZE];

    for(i=0;i<TABLESIZE;i++){
        hashTable[i].indicator = EMPTY;
        hashTable[i].key = 0;
    }

    printf("============= Hash Table ============\n");
    printf("|1. Insert a key to the hash table  |\n");
    printf("|2. Delete a key from the hash table|\n");
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
            comparison = HashInsert(key,hashTable);
            if(comparison <0)
                printf("Duplicate key\n");
            else if(comparison < TABLESIZE)
                printf("Insert: %d Key Comparisons: %d\n",key, comparison);
            else
                printf("Key Comparisons: %d. Table is full.\n",comparison);
            break;
        case 2:
            printf("Enter a key to be deleted:\n");
            scanf("%d",&key);
            comparison = HashDelete(key,hashTable);
            if(comparison <0)
                printf("%d does not exist.\n", key);
            else if(comparison <= TABLESIZE)
                printf("Delete: %d Key Comparisons: %d\n",key, comparison);
            else
                printf("Error\n");
            break;
        case 3:
            for(i=0;i<TABLESIZE;i++) printf("%d: %d %c\n",i, hashTable[i].key,hashTable[i].indicator==DELETED?'*':' ');
            break;
        }
        printf("Enter selection: ");
        scanf("%d",&opt);
    }
    return 0;
}

int hash1(int key)
{
    return (key % TABLESIZE);
}

int hash2(int key)
{
    return (key % PRIME) + 1;
}

int HashInsert(int key, HashSlot hashTable[])
{
    int hashOne = hash1(key);
    int hashTwo = hash2(key);
    int i = 0;
    int index = 0;
    int compareNo = 0;
    int delIndex = -1;
    int delslot = 0;

    while(i < TABLESIZE) {
        // formula
        index = (hashOne + i * hashTwo) % TABLESIZE;
        
        // check empty slots 
        if(hashTable[index].indicator == EMPTY) {
            hashTable[index].key = key;
            hashTable[index].indicator = USED;
            return i;
        } 

        // duplicate
        if (hashTable[index].indicator == USED) {
            if(hashTable[index].key == key)
                return -1;
        } 
        
        // check deleted slots
        // even when can slot key, need to check the other slots for possible duplicates
        if (hashTable[index].indicator == DELETED){
            // printf("%d", i);
            delslot = i + 1;
            
            // check through hash table before insertion
            while(delslot < TABLESIZE) {
                // need to apply formula again
                delIndex = (hashOne + delslot * hashTwo) % TABLESIZE;
                
                // increment compareNo 
                if(hashTable[delIndex].indicator == USED){
                    // duplicate
                    // need to increment here
                    compareNo++;
                    if(hashTable[delIndex].key == key) 
                        return -1;
                    //compareNo++;
                    
                } else if(hashTable[delIndex].indicator == EMPTY) {
                    break;
                }
                delslot++;
            }
            
            // check done can insert
            hashTable[index].key = key;
            hashTable[index].indicator = USED;
            // printf("%d", i);
            // printf("%d", compareNo);
            
            // need to add compareNo and i
            compareNo = compareNo + i;
            return compareNo;
        }
        i++;
    }
    return i;
}

int HashDelete(int key, HashSlot hashTable[])
{
    int hashOne = hash1(key);
    int hashTwo = hash2(key);
    int i = 0;
    int index = 0;
    int compareNo = 0;

    while (i < TABLESIZE) {
        //index = hash1(key + ((i++) * hash2(key))) % TABLESIZE;
        index = (hashOne + (i * hashTwo)) % TABLESIZE;

        // target key found
        if(hashTable[index].key == key) {
            // used change to deleted
            if(hashTable[index].indicator == USED) {
                hashTable[index].indicator = DELETED;
                // return compareNo++; <- doesn't work
                return compareNo + 1;
            }
        }
        compareNo++;
        i++;
    }

    // unsuccessful delete
    return -1;
}
```