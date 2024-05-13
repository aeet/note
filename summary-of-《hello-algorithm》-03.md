---
title: "Summary of 《Hello, Algorithm》- 03"
date: "2023-12-04"
categories: 
  - "algorithm"
  - "hello-algorithm"
tags: 
  - "algorithm"
coverImage: "cfcb137bbbe3415aae44301a00ea154c.jpg"
---

# Array

- An array is a type of linear data structure that stores elements of the same type in contiguous memory space.
    
- Initializing an array
    
    - Two ways to initialize an array:
        
        - Without initial values.
            
        - With given initial values.
            
        - ```cpp
            // Stored on the stack
            int arr[5];
            int nums[5] = {1, 2, 3, 4, 5};
            // Stored on the heap
            // Requires manual memory deallocation
            int* arr1 = new int[5];
            int* nums1 = new int[5]{1, 2, 3, 4, 5};
            ```
            
- Accessing elements
    
    - Array elements are stored in contiguous memory space.
    - ```
        Array: [1, 3, 2, 5, 4]
        Element index: [0, 1, 2, 3, 4]
        Address: [00, 04, 08, 12, 16]
        Element length: 4
        Element address = Array address + Element length * Element index
        // Example: Finding the memory address of element 3.
        Address = 0000 + 4 * 3 = 0012
        ```
        
    - The essence of indexing is essentially the offset of memory address.
- Accessing an element in the array at `O(1) time`.
    
    - ```cpp
        int randomAccess(int *nums, int size){
            int randomIndex = rand() % size;
            int randomNum = nums[randomIndex];
            return randomNum;
        }
        ```
        
- Inserting an element
    
    - If you want to insert an element in the middle of an array, you'll need to shift all elements after that element one position backward and then assign the element to that index.
    - Because the length of the array is fixed, inserting an element will necessarily result in the 'loss' of the element at the end of the array.
- Deleting an element
    
    - If you want to delete the element at index 𝑖, you'll need to shift all elements after index 𝑖 one position forward.
- Traversing the array
    
    - You can traverse the array either by iterating through indices or by directly accessing each element in the array.
- Searching for an element
    
    - Linear search: Traverse the array to find the element.
- Resizing the array
    
    - Sequencing makes it difficult to ensure the availability of memory space after the array, hence making it unsafe to expand the array's capacity.
    - In most programming languages, the length of an array is immutable.
    - To resize an array, a larger array needs to be created, and then the elements of the original array are sequentially copied to the new array. This operation has a time complexity of `O(n)`.
- Advantages
    
    - High space efficiency.
    - Supports random access.
    - Cache locality.
- Limitations
    
    - Low efficiency in insertion and deletion operations.
    - Immutable length.
    - Wastage of space.

# Linked List

- A linked list is a type of linear structure where each element is a node object, and these nodes are connected via 'references'.
- The references store the memory address of the next node, allowing access from the current node to the next one.
- A linked list allows nodes to be stored at scattered memory locations, and their memory addresses do not need to be contiguous.
- Initializing a linked list
    - ```cpp
        struct ListNode{
            int val;
            ListNode *next;
            ListNode(int x): val(x), next(nullptr){}
        };
        ListNode* n0 = new ListNode(1);
        ListNode* n1 = new ListNode(3);
        ListNode* n2 = new ListNode(2);
        ListNode* n3 = new ListNode(5);
        ListNode* n4 = new ListNode(4);
        n0->next = n1;
        n1->next = n2;
        n2->next = n3;
        n3->next = n4;
        ```
        
- Inserting a node
    - To insert a new node between two adjacent nodes, you only need to modify the references (pointers) of those two nodes, and this operation has a time complexity of `O(1)`.
    - ```cpp
        void insert(ListNode *n0, ListNode *P){
            ListNode *n1 = n0->next;
            P->next = n1;
            n0->next = P;
        }
        ```
        
- Deleting a node
    - Changing the reference (pointer) of a node is sufficient.
    - ```cpp
        void remove(ListNode *n0){
            if(n0->next == nullptr)
                return;
            // n0 -> p -> n1
            ListNode *P = n0->next;
            ListNode *n1 = P->next;
            n0->next = n1;
            delete P;
        }
        ```
        
- Accessing a node
    - To access the `i-th` node in a linked list, it requires `i-1` iterations, resulting in a time complexity of `O(n)`.
    - ```cpp
        ListNode *access(ListNode *head, int index){
            for(int i = 0; i < index; i++){
                if(head == nullptr)
                    return nullptr;
                head = head->next;
            }
            return head;
        }
        ```
        
- Searching a node
    - ```cpp
        int find(ListNode *head, int target) {
            int index = 0;
            while (head != nullptr) {
                if (head->val == target)
                    return index;
                head = head->next;
                index++;
            }
            return -1;
        }
        ```
        
- Common types of linked lists
    - Singly linked list
    - Doubly linked list
    - Circular linked list

# List

- List is a dynamic array.
- Initializing
    - ```cpp
        vector list1;
        vector list = {1, 2, 3, 4, 5};
        ```
        
- Accessing (`O(1)`)
    - ```cpp
        int num = list[1];
        list[1] = 0;
        ```
        
- Inserting & Deleting
    - ```cpp
        /* Clear the list */
        list.clear();
        /* Append element */
        list.push_back(1);
        list.push_back(3);
        list.push_back(2);
        list.push_back(5);
        list.push_back(4);
        /* Insert element */
        list.insert(list.begin() + 3, 6);
        // Remove element
        list.erase(list.begin() + 3); 
        ```
        
- Traverse the list
    - ```cpp
        int count = 0;
        for (int i = 0; i < list.size(); i++) {
            count++;
        }
        count = 0;
        for (int n : list) {
            count++;
        ```
        
- Contacting the list
    - ```cpp
        vector list1 = {6,7,8};
        list.insert(list.end(),list1.begin(),list1.end());
        ```
        
- Sorting the list
    - ```cpp
        sort(list.begin(),list.end());
        ```
        
- Impl

```cpp
class MyList{
    private:
        int *nums;
        int numsCapacity = 10;
        int numSize = 0;
        int extendRatio = 2;

    public:
        MyList(){
            nums = new int[numsCapacity];
        }

        ~MyList(){
            delete[] nums;
        }

        int size(){
            return numsSize;
        }

        int capacity(){
            return numsCapacity;
        }

        int get(int index){
            if(index < 0 || index >= size())
                throw out_of_range("inde error");
            return nums[index];
        }

        void set(int index, int num){
            if(index<0||index>=size())
                throw out_of_range("index error");
            nums[index] = num;
        }

        void add(int num){
            if(size() == capacity())
                extendCapacity();
            nums[size()] = num;
            numsSize++;
        }

        void insert(int index, int num){
            if(index<0||index>=size())
                throw out_of_range("index error");
            if(size()==capacity())
                extendCapacity();
            for(int j = size() -1;j>=index;j--){
                nums[j+1]=nums[j];
            }
            nums[index] = num;
            numsSize++;
        }

        int remove(int index){
            if(index<0||index>=size())
                throw out_of_range("index error");
                int num = nums[index];
                for(int j = index;j<size()-1;j++){
                    nums[j] = nums[j+1];
                }
            numsSize--;
            return num;
        }

        void extendCapacity(){
            int newCapacity = capacity() * extendRatio;
            int *tmp = nums;
            nums = new int[newCapacity];
            for(int i = 0;i<size();i++){
                nums[i] = tmp[i];
            }
            delete[] tmp;
            numsCapacity = newCapacity;
        }

        vector<int> toVector(){
            vector<int> vec(size());
            for (int i = 0; i < size(); i++) {
                vec[i] = nums[i];
            }
            return vec;
        }
}
```
