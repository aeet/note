---
title: "Summary of 《Hello, Algorithm》- 04"
date: "2023-12-12"
categories: 
  - "algorithm"
  - "hello-algorithm"
tags: 
  - "algorithm"
coverImage: "05671daab7d04086aaa594abb85e99ca.jpg"
---

A# stack

- the stack is a linear data structure that follows first-in, last-out logic.
- common stack operations
    - push: push elements onto stack `` `O(1)` ``
    - pop: pop the top element from the stack `` `O(1)` ``
    - peek: access the top element of the stack `` `O(1)` ``
- implementation based on linked list
    
    ```cpp
    class LinkedListStack{
    private:
        ListNode *stackTop;
        int stkSize;
    
    public:
        LinkedListStack(){
            stackTop = nullptr;
            stkSize = 0;
        }
    
        ~LinkedListStack(){
            // traverse the linked list to delete nodes and release memory.
            freeMemoryLinkedList(stackTop);
        }
    
        int size(){
            return stkSize;
        }
    
        bool isEmpty(){
            return stkSize == 0;
        }
    
        void push(int num){
            ListNode *node = new ListNode(num);
            node->next = stackTop;
            stackTop = node;
            stkSize ++;
        }
    
        void pop(){
            int num = top();
            ListNode *tmp = stackTop;
            stackTop = stackTop->next;
            // free memory
            delete tmp;
            stkSize --;
        }
    
        int top(){
            if(isEmpty())
                throw out_of_range("the stack is null!");
            return stackTop->val;
        }
    
        vector<int> toVector(){
            ListNode *node = stackTop;
            vector<int> res(size());
            for(int i = res.size() -1 ;i>=0;i--){
                res[i] = node->val;
                node = node->next;
            }
            return res;
        }
    }
    ```
    
- implementation based on array

```cpp
class ArrayStack{
    private:
        vector<int> stack;

    public:
        int size(){
            return stack.size();
        }

        bool isEmpty(){
            return stack.size() == 0;
        }

        void pop(){
            int oldTop = top();
            stack.pop_bakc();
        }

        int top(){
            if(isEmpty())
                throw out_of_range("stack is null!");
            return stack.back();
        }

        vector<int> toVector(){
            return stack;
        }
}
```

- comparison of two implementations
    - time efficiency
        - the efficiency of stack implemented based on arrays will decrease when expansion is triggered, but since expansion is a low-frequency operation, the average efficiency is higher.
        - stack implemented based on linked lists can provide more stable efficiency performance.
    - space efficiency
        - the stack implemented based on arrays cause a certain waste of space.
        - linked list nodes require additional storage pointers. so linked list nodes take up relatively large space.

# queue

- first in first out
    
- common operations
    
    - push `` `O(1)` ``
    - pop `` `O(1)` ``
    - peek `` `O(1)` ``
- implementation based on linked list
    

```cpp
class LinkedQueue{
    private:
        ListNode *front, *rear;
        int queSize;
    public:
        LinkedQueue(){
            front = nullptr;
            rear = nullptr;
            queSize = 0;
        }

        ~LinkedQueue(){
            freeMemoryLinkedList(front);
        }

         int size() {
            return queSize;
     }

     bool isEmpty() {
        return queSize == 0;
    }

    void push(int num){
        ListNode *noed = new ListNode(num);
        if(front == nullptr){
            front = node;
            rear = node;
        }
        else{
            rear -> next = node;
            rear = node;
        }
        queSize ++;
    }

    void pop(){
        int num = peek();
        ListNode *tmp = front;
        front = front -> next;
        delete tmp;
        queSize --;
    }

    int peek(){
        if(size() ==0)
            throw out_of_range("error");
        return front->next;
    }

    vector<int> toVector(){
        ListNode *node = front;
        vector<int> res(size());
        for(int i = 0;i<res.size();i++){
            res[i] = node->val;
            node = node->next;
        }
        return res;
    }
}
```

- implementation based on array

```cpp
class ArrayQueue{
    private:
        int *nums;
        int front;
        int queSize;
        int queCapacity;
    public:
        ArrayQueue(int capacity){
            nums = new int[capacity];
            queCapacity = capacity;
            front = queSize = 0;
        }

        ~ArrayQueue(){
            delete [] nums;
        }

        int capacity(){
            return queCapacity;
        }

        bool isEmpty(){
            return size() == 0;
        }

        int size(){
            return queSize;
        }

        void push(int num){
            if(queSize == queCapacity){
                count << "the queue is full" << endl;
                return;
            }
            // through the remainder operation, rear returns to the head after crossing the tail of the array.
            int rear = (front+queSize) % queCapacity;
            nums[rear] = num;
            queSize++;
        }

        void pop(){
            int num = peek();
            front = (front + 1) % queueCapacity;
            queSize --;
        }

        int peek(){
            if(isEmpty())
                throw out_of_range("queue is empty");
            return nums[front];
        }

        vector<int> toVector(){
            vector<int> arr(queSize);
            for (int i = 0, j = front; i < queSize; i++, j++) {
                arr[i] = nums[j % queCapacity];
            }
            return arr;
        }
}
```

- the comparison conclusion between the two implementations is consistent with the stack.

# bidirectional queue

- common operation
    
    - pushFirst() `` `O(1)` ``
    - pushLast() `` `O(1)` `` LinkedListQueue(): front(nullptr), rear(nullptr){}
    - popFirst() `` `O(1)` ``
    - popLast() `` `O(1)` ``
    - peekFirst() `` `O(1)` ``
    - peekLast() `` `O(1)` ``
- implementation based on doubly linked list
    

```cpp
struct DoublyListNode{
    int val;
    DoublyListNode *next;
    DoublyListNode *prev;
    DoublyListNode(int val): val(val), prev(nullptr), next(nullptr){}
}

class LinkedListQueue{
    private:
        DoublyListNode *front, *rear;
        int queSize = 0;
    public:
        LinkedListQueue(): front(nullptr), rear(nullptr){}
        ~LinkedListQueue(){
            DoublyListNode *pre, *cur = front;
            while(cur != nullptr){
                pre = cur;
                cur = cur -> next;
                delete pre;
            }
        }

        int size(){
            return queSize;
        }

        bool  isEmpty(){
            return size() == 0;
        }

        void push(int num, bool isFront){
            DoublyListNode *node = new DoublyListNode(num);
            if(isEmpty())
                front = rear = node;
            else if(isFront){
                front -> prev = node;
                node -> next = front;
                front = node;
            }else{
                rear -> next = node;
                node -> prev = rear;
                rear = node;
            }
            queSize ++;
        }

        void pushFirst(int num){
            push(num,true);
        }

        void pushLast(int num){
            push(num,false)
        }

        int pop(bool isFront){
            if(isEmpty())
                throw out_of_range("queue is empty!");
            int val;
            if(isFront){
                val = front->val;
                DoublyListNode *fNext  = front -> next;
                if(fNext != nullptr){
                    fNext -> prev = nullptr;
                    fNext -> next = nullptr;
                    delete front;
                }
                front  = fNext;
            }else{
                val = rear -> val;
                DoublyListNode *rPrev = rear -> prev;
                if(rPrev != nullptr){
                    rPrev -> next = nullptr;
                    rear -> prev = nullptr;
                    delete rear;
                }
                rear = rPrev;
            }
            queSize --;
            return val;
        }

        int popFirst(){
            return pop(true);
        }

        int popLast(){
            return pop(false);
        }

        int peekFirst(){
            if (isEmpty())
                throw out_of_range("queue is empty");
            return front->val;
        }

        int peekLast(){
            if (isEmpty())
                throw out_of_range("queue is empty");
            return rear->val;
        }

        vector<int> toVector(){
            DoublyListNode *node = front;
            vector<int> res(size());
            for (int i = 0; i < res.size(); i++) {
                res[i] = node->val;
                node = node->next;
            }
            return res;
        }
}
```

- implementation based on array

```cpp
class ArrayDeque {
  private:
    vector<int> nums; 
    int front;        
    int queSize;     

  public:
    /* 构造方法 */
    ArrayDeque(int capacity) {
        nums.resize(capacity);
        front = queSize = 0;
    }

    int capacity() {
        return nums.size();
    }

    int size() {
        return queSize;
    }

    bool isEmpty() {
        return queSize == 0;
    }

    int index(int i) {
        return (i + capacity()) % capacity();
    }

    void pushFirst(int num) {
        if (queSize == capacity()) {
            cout << "双向队列已满" << endl;
            return;
        }
        front = index(front - 1);
        nums[front] = num;
        queSize++;
    }

    void pushLast(int num) {
        if (queSize == capacity()) {
            cout << "双向队列已满" << endl;
            return;
        }
        int rear = index(front + queSize);
        nums[rear] = num;
        queSize++;
    }

    int popFirst() {
        int num = peekFirst();
        front = index(front + 1);
        queSize--;
        return num;
    }

    int popLast() {
        int num = peekLast();
        queSize--;
        return num;
    }

    int peekFirst() {
        if (isEmpty())
            throw out_of_range("双向队列为空");
        return nums[front];
    }

    int peekLast() {
        if (isEmpty())
            throw out_of_range("双向队列为空");
        int last = index(front + queSize - 1);
        return nums[last];
    }

    vector<int> toVector() {
        vector<int> res(queSize);
        for (int i = 0, j = front; i < queSize; i++, j++) {
            res[i] = nums[index(j)];
        }
        return res;
    }
};
```
