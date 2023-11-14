
  # two-sum

  ```c
  /**
 * Note: The returned array must be malloced, assume caller calls free().
 */
typedef struct HashNode {
    int key;
    int value;
    struct HashNode* next;
} HashNode;

typedef struct HashMap {
    HashNode** buckets;
    int size;
} HashMap;

HashMap* createHashMap(int size) {
    HashMap* map = (HashMap*)malloc(sizeof(HashMap));
    map->size = size;
    map->buckets = (HashNode**)malloc(sizeof(HashNode*) * size);
    for (int i = 0; i < size; i++) {
        map->buckets[i] = NULL;
    }
    return map;
}

int hashCode(int key, int size) {
    return abs(key) % size;
}

void insert(HashMap* map, int key, int value) {
    int index = hashCode(key, map->size);
    HashNode* newNode = (HashNode*)malloc(sizeof(HashNode));
    newNode->key = key;
    newNode->value = value;
    newNode->next = map->buckets[index];
    map->buckets[index] = newNode;
}

int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
    HashMap* map = createHashMap(numsSize);
    for (int i = 0; i < numsSize; i++) {
        int complement = target - nums[i];
        int index = hashCode(complement, numsSize);
        HashNode* current = map->buckets[index];
        while (current != NULL) {
            if (current->key == complement) {
                int* result = (int*)malloc(sizeof(int) * 2);
                result[0] = current->value;
                result[1] = i;
                *returnSize = 2;
                return result;
            }
            current = current->next;
        }
        insert(map, nums[i], i);
    }
    *returnSize = 0; // No solution found
    return NULL;
}

  ```
  