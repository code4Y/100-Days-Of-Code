## 622. Design Circular Queue  

Design your implementation of the circular queue. The circular queue is a linear data structure in which the operations 
are performed based on FIFO (First In First Out) principle, and the last position is connected back to the first position 
to make a circle. It is also called "Ring Buffer".  

One of the benefits of the circular queue is that we can make use of the spaces in front of the queue. In a normal queue, 
once the queue becomes full, we cannot insert the next element even if there is a space in front of the queue. But using 
the circular queue, we can use the space to store new values.  
  
Implement the ```MyCircularQueue``` class:  
  
* ```MyCircularQueue(k)``` Initializes the object with the size of the queue to be ```k```.  
* ```int Front()``` Gets the front item from the queue. If the queue is empty, return ```-1```.  
* ```int Rear()``` Gets the last item from the queue. If the queue is empty, return ```-1```.  
* ```boolean enQueue(int value)``` Inserts an element into the circular queue. Return ```true``` if the operation is successful.  
* ```boolean deQueue()``` Deletes an element from the circular queue. Return ```true``` if the operation is successful.  
* ```boolean isEmpty()``` Checks whether the circular queue is empty or not.  
* ```boolean isFull()``` Checks whether the circular queue is full or not.  

You must solve the problem without using the built-in queue data structure in your programming language.  
  
  
 
### Example:  
```
Input
["MyCircularQueue", "enQueue", "enQueue", "enQueue", "enQueue", "Rear", "isFull", "deQueue", "enQueue", "Rear"]
[[3], [1], [2], [3], [4], [], [], [], [4], []]
Output
[null, true, true, true, false, 3, true, true, true, 4]

Explanation
MyCircularQueue myCircularQueue = new MyCircularQueue(3);
myCircularQueue.enQueue(1); // return True
myCircularQueue.enQueue(2); // return True
myCircularQueue.enQueue(3); // return True
myCircularQueue.enQueue(4); // return False
myCircularQueue.Rear();     // return 3
myCircularQueue.isFull();   // return True
myCircularQueue.deQueue();  // return True
myCircularQueue.enQueue(4); // return True
myCircularQueue.Rear();     // return 4
```  
  
### Constraints:  
```
1 <= k <= 1000
0 <= value <= 1000
At most 3000 calls will be made to enQueue, deQueue, Front, Rear, isEmpty, and isFull.
```  
<br>  

## Approach:  

The MyCircularQueue class is a data structure that implements a queue using a circular array. It provides the following methods:

1. MyCircularQueue(int k): This is the constructor of the class. It initializes the data member variable to be a vector of size k, and sets the head, tail, and size member variables to their initial values.

2. enQueue(int value): This method adds a new element to the tail of the queue. It first checks if the queue is full, and returns false if it is. If the queue is not full, it adds the element to the tail of the queue, updates the tail member variable, and returns true.

3. deQueue(): This method removes the element at the head of the queue. It first checks if the queue is empty, and returns false if it is. If the queue is not empty, it removes the element at the head of the queue, updates the head member variable, and returns true.

4. Front(): This method returns the element at the head of the queue. If the queue is empty, it returns -1.

5. Rear(): This method returns the element at the tail of the queue. If the queue is empty, it returns -1.

6. isEmpty(): This method returns true if the queue is empty, or false if the queue is not empty.

7. isFull(): This method returns true if the queue is full, or false if the queue is not full.  
  
  
### Code:  
```
class MyCircularQueue {
    vector<int> data;
    int head;
    int tail;
    int size;
public:
    MyCircularQueue(int k) {
        data.resize(k);
        head = -1;
        tail = -1;
        size = k;
    }
    
    bool enQueue(int value) {
        if (isFull()) {
            return false;
        }
        if (isEmpty()) {
            head = 0;
        }
        tail = (tail + 1) % size;
        data[tail] = value;
        return true;
    }
    
    bool deQueue() {
        if (isEmpty()) {
            return false;
        }
        if (head == tail) {
            head = -1;
            tail = -1;
            return true;
        }
        head = (head + 1) % size;
        return true;
    }
    
    int Front() {
        if (isEmpty()) {
            return -1;
        }
        return data[head];
    }
    
    int Rear() {
        if (isEmpty()) {
            return -1;
        }
        return data[tail];
    }
    
    bool isEmpty() {
         return head == -1;
    }
    
    bool isFull() {
        return ((tail + 1) % size) == head;
    }
};
```  
  
  
### Complexity:  

The time complexity of each of the methods in the MyCircularQueue class is O(1), because they perform a constant number of operations.  

The space complexity of the MyCircularQueue class is O(k), where k is the size of the circular array. This is because the class stores 
the elements of the queue in the data member variable, which has a size of k.  
  
Therefore, the overall time and space complexity of the MyCircularQueue class is O(1) for each method, and O(k) for the entire class.  
