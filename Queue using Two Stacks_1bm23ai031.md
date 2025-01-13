# Enter your code here. Read input from STDIN. Print output to STDOUT
class QueueUsingTwoStacks:
    def __init__(self):
        self.stack1 = []
        self.stack2 = []

    def enqueue(self, x):
        # Add element to stack1
        self.stack1.append(x)

    def dequeue(self):
        # If stack2 is empty, transfer all elements from stack1 to stack2
        if not self.stack2:
            while self.stack1:
                self.stack2.append(self.stack1.pop())
        
        # If stack2 is still empty, the queue is empty, no element to dequeue
        if self.stack2:
            self.stack2.pop()

    def front(self):
        # If stack2 is empty, transfer elements from stack1 to stack2
        if not self.stack2:
            while self.stack1:
                self.stack2.append(self.stack1.pop())
        
        # If stack2 is not empty, return the top of stack2 (front of the queue)
        if self.stack2:
            return self.stack2[-1]
        return None  # Queue is empty


# Reading input
n = int(input())  # Number of operations
queue = QueueUsingTwoStacks()

for _ in range(n):
    operation = list(map(int, input().split()))
    
    if operation[0] == 1:
        # Enqueue operation
        queue.enqueue(operation[1])
    elif operation[0] == 2:
        # Dequeue operation
        queue.dequeue()
    elif operation[0] == 3:
        # Print front of queue
        print(queue.front())
