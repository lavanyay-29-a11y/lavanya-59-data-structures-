# lavanya-59-data-structures-
question1.
Take a string as input
Push each character into stack
Pop characters one by one
Print them → reversed string
#include <stdio.h>
#include <string.h>

#define MAX 100

char stack[MAX];
int top = -1;

void push(char ch) {
    stack[++top] = ch;
}

char pop() {
    return stack[top--];
}

int main() {
    char str[100];
    printf("Enter string: ");
    scanf("%s", str);

    for(int i = 0; i < strlen(str); i++) {
        push(str[i]);
    }

    printf("Reversed string: ");
    while(top != -1) {
        printf("%c", pop());
    }
    return 0;
}

question2.
Read expression
Push '(' into stack
If ')' comes → pop
If stack empty at end → Balanced
Else → Not Balanced

#include <stdio.h>
#include <string.h>

char stack[100];
int top = -1;

void push(char ch) {
    stack[++top] = ch;
}

void pop() {
    top--;
}

int main() {
    char exp[100];
    printf("Enter expression: ");
    scanf("%s", exp);

    for(int i = 0; i < strlen(exp); i++) {
        if(exp[i] == '(')
            push(exp[i]);
        else if(exp[i] == ')') {
            if(top == -1) {
                printf("Not Balanced");
                return 0;
            }
            pop();
        }
    }

    if(top == -1)
        printf("Balanced Expression");
    else
        printf("Not Balanced");

    return 0;
}

question3.
Take array input
Compare each element with next elements
Print first greater element
If none → print -1

#include <stdio.h>

int main() {
    int arr[] = {4, 5, 2, 10, 8};
    int n = 5;

    for(int i = 0; i < n; i++) {
        int found = 0;
        for(int j = i + 1; j < n; j++) {
            if(arr[j] > arr[i]) {
                printf("%d -> %d\n", arr[i], arr[j]);
                found = 1;
                break;
            }
        }
        if(!found)
            printf("%d -> -1\n", arr[i]);
    }
    return 0;
}

question4.
Create queue
Add document (enqueue)
Print document (dequeue)
Display queue

#include <stdio.h>
#define MAX 5

int queue[MAX], front = -1, rear = -1;

void enqueue(int x) {
    if(rear == MAX - 1)
        printf("Queue Full\n");
    else {
        if(front == -1) front = 0;
        queue[++rear] = x;
    }
}

void dequeue() {
    if(front == -1)
        printf("Queue Empty\n");
    else {
        printf("Printed document: %d\n", queue[front]);
        front++;
        if(front > rear)
            front = rear = -1;
    }
}

void display() {
    if(front == -1)
        printf("No documents\n");
    else {
        for(int i = front; i <= rear; i++)
            printf("%d ", queue[i]);
    }
}

int main() {
    enqueue(1);
    enqueue(2);
    display();
    dequeue();
    display();
    return 0;
}

question5.
Initialize front & rear
Perform operations:
Enqueue
Dequeue
Peek
Display
Repeat using menu

#include <stdio.h>
#define MAX 5

int cq[MAX], front = -1, rear = -1;

void enqueue(int x) {
    if((rear + 1) % MAX == front)
        printf("Queue Full\n");
    else {
        if(front == -1) front = 0;
        rear = (rear + 1) % MAX;
        cq[rear] = x;
    }
}

void dequeue() {
    if(front == -1)
        printf("Queue Empty\n");
    else {
        printf("Deleted: %d\n", cq[front]);
        if(front == rear)
            front = rear = -1;
        else
            front = (front + 1) % MAX;
    }
}

void peek() {
    if(front != -1)
        printf("Front: %d\n", cq[front]);
}

void display() {
    if(front == -1)
        printf("Empty\n");
    else {
        int i = front;
        while(1) {
            printf("%d ", cq[i]);
            if(i == rear) break;
            i = (i + 1) % MAX;
        }
    }
}

int main() {
    int ch, x;
    while(1) {
        printf("\n1.Enqueue 2.Dequeue 3.Peek 4.Display 5.Exit\n");
        scanf("%d", &ch);

        switch(ch) {
            case 1:
                printf("Enter value: ");
                scanf("%d", &x);
                enqueue(x);
                break;
            case 2:
                dequeue();
                break;
            case 3:
                peek();
                break;
            case 4:
                display();
                break;
            case 5:
                return 0;
        }
    }
}
