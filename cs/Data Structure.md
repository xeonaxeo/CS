# 자료구조(Data Structure)
### **리스트 (List)**

![Image](./image%20(1).png)
### 1. **배열 (Array)**

- **고정 크기 배열 (Fixed-size Array)**
    - 초기 생성 시 크기를 지정해야 하는 고정 크기의 배열
    - 데이터가 연속된 메모리 공간에 저장됨
    - 접근 시간은 O(1), 삽입 및 삭제는 O(n)
    - O(1): 상수시간, 요소가 리스트의 위치에 상관없이 항상 일정한 시간에 접근가능
    - O(n): 선형시간, 리스트에서 특정 위치에 요소를 삽입하거나 삭제할 때 시간이 리스트의 길이(n)와 비례
```c
#include <stdio.h>

int main() {
    int arr[3] = {1, 2, 3}; // 크기 3의 고정크기기 배열
    for (int i = 0; i < 3; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

- **동적 배열 (Dynamic Array)**
    - 필요에 따라 크기를 동적으로 조정할 수 있는 배열
    - 메모리 초과 시 더 큰 배열로 복사하여 확장

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int n = 3;
    int* arr = (int*)malloc(n * sizeof(int)); // 크기 3의 동적 배열 생성

    for (int i = 0; i < n; i++) {
        arr[i] = i + 1; // 값 초기화
        printf("%d ", arr[i]);
    }

    free(arr); // 메모리 해제
    return 0;
}
```

### 2. **연결 리스트 (Linked List)**

:리스트의 항목들을 노드(데이터필드,링크필드)에 분산하여 저장하는 리스트

데이터 필드: 리스트의 원소, 데이터 값을 저장하는곳

링크 필드: 다른 노드의 주소값을 저장하는 장소(포인터)

![Image](./image%20(2).png)

- **단일 연결 리스트 (Singly-Linked List)**
    - 각 노드는 다음 노드를 가리키는 포인터를 포함
    - 삽입/삭제가 효율적이나, 임의 접근은 불가능
  
```c
#include <stdio.h>
#include <stdlib.h>

// 노드 구조체 정의
struct Node {
    int data;
    struct Node* next;
};

// 새 노드 생성 함수
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}

// 연결리스트 출력 함수
void printList(struct Node* head) {
    struct Node* temp = head;
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

int main() {
    struct Node* head = createNode(1);
    head->next = createNode(2);
    head->next->next = createNode(3);

    printList(head); // 출력: 1 -> 2 -> 3 -> NULL
    return 0;
}
```

- **이중 연결 리스트 (Doubly-Linked List)**
    - 각 노드가 이전 노드와 다음 노드의 포인터를 포함
    - 양방향 탐색이 가능하나, 메모리 사용량이 증가함
```c
#include <stdio.h>
#include <stdlib.h>

// 노드 구조체 정의
struct Node {
    int data;
    struct Node* prev;
    struct Node* next;
};

// 새 노드 생성 함수
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->prev = NULL;
    newNode->next = NULL;
    return newNode;
}

// 연결리스트 출력 함수
void printList(struct Node* head) {
    struct Node* temp = head;
    while (temp != NULL) {
        printf("%d <-> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

int main() {
    struct Node* head = createNode(1);
    head->next = createNode(2);
    head->next->prev = head;
    head->next->next = createNode(3);
    head->next->next->prev = head->next;

    printList(head); // 출력: 1 <-> 2 <-> 3 <-> NULL
    return 0;
}
```
- **원형 연결 리스트 (Circular-Linked List)**
    - 마지막 노드가 첫 번째 노드와 연결된 형태
    - 순환적인 데이터 구조에 적합
```c
#include <stdio.h>
#include <stdlib.h>

// 노드 구조체 정의
struct Node {
    int data;
    struct Node* next;
};

// 새 노드 생성 함수
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = newNode; // 자기 자신을 가리킴
    return newNode;
}

// 연결리스트 출력 함수 (원형 리스트의 특성상 첫 번째 노드까지 돌아야 종료)
void printList(struct Node* head) {
    struct Node* temp = head;
    do {
        printf("%d -> ", temp->data);
        temp = temp->next;
    } while (temp != head);
    printf("...\n");
}

int main() {
    struct Node* head = createNode(1);
    head->next = createNode(2);
    head->next->next = createNode(3);
    head->next->next->next = head; // 마지막 노드가 첫 번째 노드를 가리킴

    printList(head); // 출력: 1 -> 2 -> 3 -> ...
    return 0;
}
```
- **다중 연결 리스트 (Multi-Linked List)**
    - 각 노드가 여러 포인터를 가질 수 있는 연결 리스트
    - 복잡한 관계를 표현하는 데 사용
```c
#include <stdio.h>
#include <stdlib.h>

// 노드 구조체 정의
struct Node {
    int data;
    struct Node* next;
    struct Node* down; // 추가적인 연결
};

// 새 노드 생성 함수
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = NULL;
    newNode->down = NULL;
    return newNode;
}

// 연결리스트 출력 함수
void printList(struct Node* head) {
    struct Node* temp = head;
    while (temp != NULL) {
        printf("%d ", temp->data);
        if (temp->down != NULL) {
            printf("[down: %d] ", temp->down->data);
        }
        temp = temp->next;
    }
    printf("\n");
}

int main() {
    struct Node* head = createNode(1);
    head->next = createNode(2);
    head->next->down = createNode(3);
    head->next->next = createNode(4);

    printList(head); // 출력: 1 2 [down: 3] 4 
    return 0;
}
```
---

### **스택 (Stack)**
:LIFO(Last In First Out)방식으로 작업이 수행되어야할 떄 사용
- **배열 기반 스택 (Array-based Stack)**
![image](./image%20(3).png)

    - 배열을 이용하여 구현된 스택
    - 크기가 고정되어 있어 초과 시 재할당이 필요
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 5 // 스택 크기

// 스택 구조체
struct Stack {
    int arr[MAX];
    int top;
};

// 스택 초기화 함수
void initStack(struct Stack* stack) {
    stack->top = -1;
}

// 스택이 비었는지 확인하는 함수
int isEmpty(struct Stack* stack) {
    return stack->top == -1;
}

// 스택이 꽉 찼는지 확인하는 함수
int isFull(struct Stack* stack) {
    return stack->top == MAX - 1;
}

// 스택에 요소 추가
void push(struct Stack* stack, int value) {
    if (isFull(stack)) {
        printf("Stack Overflow\n");
        return;
    }
    stack->arr[++(stack->top)] = value;
    printf("%d pushed to stack\n", value);
}

// 스택에서 요소 제거
int pop(struct Stack* stack) {
    if (isEmpty(stack)) {
        printf("Stack Underflow\n");
        return -1;
    }
    return stack->arr[(stack->top)--];
}

// 스택의 top 요소 확인
int peek(struct Stack* stack) {
    if (isEmpty(stack)) {
        printf("Stack is empty\n");
        return -1;
    }
    return stack->arr[stack->top];
}

int main() {
    struct Stack stack;
    initStack(&stack);
    
    push(&stack, 10);
    push(&stack, 20);
    push(&stack, 30);

    printf("%d popped from stack\n", pop(&stack));
    
    return 0;
}
```
- **연결 리스트 기반 스택 (Linked List-based Stack)**
![image](./image%20(8).png)
    - 연결 리스트로 구현된 스택
    - 동적 크기로 인해 삽입/삭제가 효율적
```c
#include <stdio.h>
#include <stdlib.h>

// 노드 구조체 정의
struct Node {
    int data;
    struct Node* next;
};

// 스택에 노드 추가
void push(struct Node** top, int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->next = *top;
    *top = newNode;
    printf("%d pushed to stack\n", value);
}

// 스택에서 노드 제거
int pop(struct Node** top) {
    if (*top == NULL) {
        printf("Stack Underflow\n");
        return -1;
    }
    struct Node* temp = *top;
    int popped = temp->data;
    *top = (*top)->next;
    free(temp);
    return popped;
}

// 스택의 top 요소 확인
int peek(struct Node* top) {
    if (top == NULL) {
        printf("Stack is empty\n");
        return -1;
    }
    return top->data;
}

int main() {
    struct Node* top = NULL;

    push(&top, 10);
    push(&top, 20);
    push(&top, 30);

    printf("%d popped from stack\n", pop(&top));

    return 0;
}
#include <stdio.h>
#include <stdlib.h>

// 노드 구조체 정의
struct Node {
    int data;
    struct Node* next;
};

// 스택에 노드 추가
void push(struct Node** top, int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->next = *top;
    *top = newNode;
    printf("%d pushed to stack\n", value);
}

// 스택에서 노드 제거
int pop(struct Node** top) {
    if (*top == NULL) {
        printf("Stack Underflow\n");
        return -1;
    }
    struct Node* temp = *top;
    int popped = temp->data;
    *top = (*top)->next;
    free(temp);
    return popped;
}

// 스택의 top 요소 확인
int peek(struct Node* top) {
    if (top == NULL) {
        printf("Stack is empty\n");
        return -1;
    }
    return top->data;
}

int main() {
    struct Node* top = NULL;

    push(&top, 10);
    push(&top, 20);
    push(&top, 30);

    printf("%d popped from stack\n", pop(&top));

    return 0;
}
```
- **최소값/최대값 추적 스택 (Min/Max Stack)**
    - 스택의 최소값 또는 최대값을 O(1)로 반환
    - 추가 공간을 활용하여 구현됨
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 5

// 스택 구조체 정의
struct Stack {
    int arr[MAX];
    int minArr[MAX];  // 최소값 추적용 배열
    int maxArr[MAX];  // 최대값 추적용 배열
    int top;
};

// 스택 초기화
void initStack(struct Stack* stack) {
    stack->top = -1;
}

// 스택이 비었는지 확인
int isEmpty(struct Stack* stack) {
    return stack->top == -1;
}

// 스택이 꽉 찼는지 확인
int isFull(struct Stack* stack) {
    return stack->top == MAX - 1;
}

// 최소값/최대값 추적 스택에 값 추가
void push(struct Stack* stack, int value) {
    if (isFull(stack)) {
        printf("Stack Overflow\n");
        return;
    }
    stack->arr[++(stack->top)] = value;

    // 최소값 추적
    if (stack->top == 0 || value < stack->minArr[stack->top - 1]) {
        stack->minArr[stack->top] = value;
    } else {
        stack->minArr[stack->top] = stack->minArr[stack->top - 1];
    }

    // 최대값 추적
    if (stack->top == 0 || value > stack->maxArr[stack->top - 1]) {
        stack->maxArr[stack->top] = value;
    } else {
        stack->maxArr[stack->top] = stack->maxArr[stack->top - 1];
    }

    printf("%d pushed to stack\n", value);
}

// 최소값 추적 스택에서 값 제거
int pop(struct Stack* stack) {
    if (isEmpty(stack)) {
        printf("Stack Underflow\n");
        return -1;
    }
    int popped = stack->arr[(stack->top)--];
    return popped;
}

// 스택의 최소값 반환
int getMin(struct Stack* stack) {
    if (isEmpty(stack)) {
        printf("Stack is empty\n");
        return -1;
    }
    return stack->minArr[stack->top];
}

// 스택의 최대값 반환
int getMax(struct Stack* stack) {
    if (isEmpty(stack)) {
        printf("Stack is empty\n");
        return -1;
    }
    return stack->maxArr[stack->top];
}

int main() {
    struct Stack stack;
    initStack(&stack);

    push(&stack, 10);
    push(&stack, 20);
    push(&stack, 5);
    push(&stack, 30);

    printf("Min: %d\n", getMin(&stack));  // 출력: Min: 5
    printf("Max: %d\n", getMax(&stack));  // 출력: Max: 30

    pop(&stack);

    printf("Min: %d\n", getMin(&stack));  // 출력: Min: 5
    printf("Max: %d\n", getMax(&stack));  // 출력: Max: 20

    return 0;
}
```
---

### **큐 (Queue)**
:FIFO(First In First Out)방식으로 작업을 처리해야할 때 사용
- **배열 기반 큐 (Array-based Queue)**

    - 배열로 구현되며 크기가 제한적
    - 데이터 이동시에 인덱스를 증가만 하여 사용하는 방식이므로 앞부분에 데이터가 없을 때도 비어있는 공간을 활용할 수 없기 때문에 비효율이 발생할 수 있음
  
  ![image](./image%20(4).png)
    - 삽입을 하기위해서는 요소들을 이동시켜야함
```c
  #include <stdio.h>
#include <stdlib.h>

#define MAX 100

typedef struct Stack {
    int data[MAX];
    int top;
} Stack;

void init(Stack* s) {
    s->top = -1;
}

void push(Stack* s, int value) {
    if (s->top == MAX - 1) {
        printf("Stack overflow\n");
        return;
    }
    s->data[++(s->top)] = value;
}

int pop(Stack* s) {
    if (s->top == -1) {
        printf("Stack underflow\n");
        return -1;
    }
    return s->data[(s->top)--];
}

int peek(Stack* s) {
    if (s->top == -1) {
        printf("Stack is empty\n");
        return -1;
    }
    return s->data[s->top];
}

int main() {
    Stack stack;
    init(&stack);

    push(&stack, 1);
    push(&stack, 2);
    push(&stack, 3);

    printf("%d\n", pop(&stack));  // 출력: 3
    printf("%d\n", peek(&stack));  // 출력: 2
    return 0;
}
```
- **순환 큐 (Circular Queue)**
    - 마지막 인덱스가 첫 인덱스와 연결됨
    - 공간 활용이 효율적
    
    ![image.png](./image%20(5).png)
    
    공백상태는 front == rear 인 상태이며 포화상태는 front == (rear+1) % MAX_QUEUE_SIZE 의 값으로 판단함함
    
    위 그림에서 큐의 맥스 크기는 8, 만약 front가 2에 있을 때 포화상태라면 rear가 1에 있어야 함함 그 값을 우변에서 계산하면 (1+1) % 8 = 2가 되므로 front와 rear값이 같아 포화상태인 것을 알림 공백상태와 포화상태를 구별하기 위하여 하나의 공간은 항상 비워둔다
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 5

// 큐 구조체 정의
struct Queue {
    int arr[MAX];
    int front, rear;
};

// 큐 초기화
void initQueue(struct Queue* q) {
    q->front = q->rear = -1;
}

// 큐가 비었는지 확인
int isEmpty(struct Queue* q) {
    return (q->front == -1);
}

// 큐가 꽉 찼는지 확인
int isFull(struct Queue* q) {
    return ((q->rear + 1) % MAX == q->front);
}

// 큐에 요소 추가 (enqueue)
void enqueue(struct Queue* q, int value) {
    if (isFull(q)) {
        printf("Queue is Full\n");
        return;
    }
    
    if (q->front == -1) { // 첫 번째 요소를 추가하는 경우
        q->front = 0;
    }
    q->rear = (q->rear + 1) % MAX;
    q->arr[q->rear] = value;
    printf("%d enqueued to queue\n", value);
}

// 큐에서 요소 제거 (dequeue)
int dequeue(struct Queue* q) {
    if (isEmpty(q)) {
        printf("Queue is Empty\n");
        return -1;
    }
    
    int value = q->arr[q->front];
    
    if (q->front == q->rear) { // 큐에 하나만 남은 경우
        q->front = q->rear = -1;
    } else {
        q->front = (q->front + 1) % MAX;
    }
    
    return value;
}

// 큐의 첫 번째 요소 확인
int front(struct Queue* q) {
    if (isEmpty(q)) {
        printf("Queue is Empty\n");
        return -1;
    }
    return q->arr[q->front];
}

int main() {
    struct Queue q;
    initQueue(&q);

    enqueue(&q, 10);
    enqueue(&q, 20);
    enqueue(&q, 30);
    enqueue(&q, 40);
    enqueue(&q, 50);

    printf("%d dequeued from queue\n", dequeue(&q));
    enqueue(&q, 60);

    printf("Front element is %d\n", front(&q));

    return 0;
}
```
- **연결 리스트 기반 큐 (Linked List-based Queue)**
    - 동적 크기를 지원하며 메모리 효율적
![image](./image%20(9).png)
- tail에 큐의 마지막 노드를 저장하고 tail이 next로 큐의 첫번째 값을 참조 
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int data;
    struct Node* next;
} Node;

typedef struct Stack {
    Node* top;
} Stack;

void init(Stack* stack) {
    stack->top = NULL;
}

void push(Stack* stack, int data) {
    Node* new_node = (Node*)malloc(sizeof(Node));
    new_node->data = data;
    new_node->next = stack->top;
    stack->top = new_node;
}

int pop(Stack* stack) {
    if (stack->top == NULL) {
        printf("Stack is empty\n");
        return -1;
    }
    Node* temp = stack->top;
    int popped_data = temp->data;
    stack->top = temp->next;
    free(temp);
    return popped_data;
}

int peek(Stack* stack) {
    if (stack->top == NULL) {
        printf("Stack is empty\n");
        return -1;
    }
    return stack->top->data;
}

int main() {
    Stack stack;
    init(&stack);

    push(&stack, 1);
    push(&stack, 2);
    push(&stack, 3);

    printf("%d\n", pop(&stack));  // 출력: 3
    printf("%d\n", peek(&stack));  // 출력: 2
    return 0;
}
```
- **우선순위 큐 (Priority Queue)**
    - 요소가 우선순위에 따라 처리
    - **배열 기반 우선순위 큐**: 삽입 O(1), 삭제 O(n)
    ![image](./image%20(10).png)

        ```c
        #include <stdio.h>
        #include <stdlib.h>
        #define MAX 100

        typedef struct Queue {
            int data[MAX];
            int front, rear;
        } Queue;

        void init(Queue* q) {
            q->front = 0;
            q->rear = -1;
        }

        void enqueue(Queue* q, int value) {
            if (q->rear == MAX - 1) {
                printf("Queue overflow\n");
                return;
            }
            q->data[++(q->rear)] = value;
        }

        int dequeue(Queue* q) {
            if (q->front > q->rear) {
                printf("Queue underflow\n");
                return -1;
            }
            return q->data[(q->front)++];
        }

        int peek(Queue* q) {
            if (q->front > q->rear) {
                printf("Queue is empty\n");
                return -1;
            }
            return q->data[q->front];
        }

        int main() {
            Queue q;
            init(&q);

            enqueue(&q, 1);
            enqueue(&q, 2);
            enqueue(&q, 3);

            printf("%d\n", dequeue(&q));  // 출력: 1
            printf("%d\n", peek(&q));    // 출력: 2
            return 0;
        }
        ```

    - **힙 기반 우선순위 큐**: 삽입/삭제 O(log n)
    ![image](./image%20(11).png)

        ```c
        #include <stdio.h>
        #include <stdlib.h>
        #define MAX 10

        // 힙 구조체 정의
        typedef struct {
            int arr[MAX];
            int size;
        } MaxHeap;

        // 힙 초기화
        void initHeap(MaxHeap* heap) {
            heap->size = 0;
        }

        // 부모 인덱스 반환
        int parent(int i) {
            return (i - 1) / 2;
        }

        // 왼쪽 자식 인덱스 반환
        int leftChild(int i) {
            return 2 * i + 1;
        }

        // 오른쪽 자식 인덱스 반환
        int rightChild(int i) {
            return 2 * i + 2;
        }

        // 힙 구조에서 인덱스 i의 위치에서 위로 올라가며 힙 정렬
        void heapifyUp(MaxHeap* heap, int i) {
            while (i > 0 && heap->arr[parent(i)] < heap->arr[i]) {
                int temp = heap->arr[parent(i)];
                heap->arr[parent(i)] = heap->arr[i];
                heap->arr[i] = temp;
                i = parent(i);
            }
        }

        // 힙에 요소 삽입
        void insert(MaxHeap* heap, int value) {
            if (heap->size == MAX) {
                printf("Heap is full!\n");
                return;
            }
            heap->arr[heap->size] = value;
            heapifyUp(heap, heap->size);
            heap->size++;
        }

        // 힙 구조에서 인덱스 i의 위치에서 아래로 내려가며 힙 정렬
        void heapifyDown(MaxHeap* heap, int i) {
            int largest = i;
            int left = leftChild(i);
            int right = rightChild(i);

            if (left < heap->size && heap->arr[left] > heap->arr[largest]) {
                largest = left;
            }

            if (right < heap->size && heap->arr[right] > heap->arr[largest]) {
                largest = right;
            }

            if (largest != i) {
                int temp = heap->arr[i];
                heap->arr[i] = heap->arr[largest];
                heap->arr[largest] = temp;
                heapifyDown(heap, largest);
            }
        }

        // 힙에서 최대값을 제거하고 반환
        int extractMax(MaxHeap* heap) {
            if (heap->size == 0) {
                printf("Heap is empty!\n");
                return -1;
            }
            int max = heap->arr[0];
            heap->arr[0] = heap->arr[heap->size - 1];
            heap->size--;
            heapifyDown(heap, 0);
            return max;
        }

        // 힙 출력
        void printHeap(MaxHeap* heap) {
            for (int i = 0; i < heap->size; i++) {
                printf("%d ", heap->arr[i]);
            }
            printf("\n");
        }

        int main() {
            MaxHeap heap;
            initHeap(&heap);

            insert(&heap, 10);
            insert(&heap, 20);
            insert(&heap, 5);
            insert(&heap, 30);
            insert(&heap, 15);

            printf("Max Heap: ");
            printHeap(&heap);

            printf("Extracted max: %d\n", extractMax(&heap));
            printf("Max Heap after extraction: ");
            printHeap(&heap);

            return 0;
        }
        ```

---

### **데크 (Deque)**

![image.png](./image%20(6).png)

후단으로만 데이터를 삽입했던 선형큐,원형큐와 달리 양방향 삽입삭제 가능

![image.png](./image%20(7).png)

삽입 연산시 front는 감소하고 rear은 증가하며 삭제 연산시 foront는 증가하고 rear은 감소

- **배열 기반 데크 (Array-based Deque)**
    - 배열로 양방향 삽입/삭제를 지원함
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 100

typedef struct {
    int data[MAX];
    int front, rear;
} ArrayDeque;

void init(ArrayDeque* deque) {
    deque->front = deque->rear = -1;
}

int is_empty(ArrayDeque* deque) {
    return deque->front == -1;
}

int is_full(ArrayDeque* deque) {
    return (deque->rear + 1) % MAX == deque->front;
}

void add_front(ArrayDeque* deque, int value) {
    if (is_full(deque)) {
        printf("Deque is full\n");
        return;
    }
    if (is_empty(deque)) {
        deque->front = deque->rear = 0;
    } else {
        deque->front = (deque->front - 1 + MAX) % MAX;
    }
    deque->data[deque->front] = value;
}

void add_rear(ArrayDeque* deque, int value) {
    if (is_full(deque)) {
        printf("Deque is full\n");
        return;
    }
    if (is_empty(deque)) {
        deque->front = deque->rear = 0;
    } else {
        deque->rear = (deque->rear + 1) % MAX;
    }
    deque->data[deque->rear] = value;
}

int remove_front(ArrayDeque* deque) {
    if (is_empty(deque)) {
        printf("Deque is empty\n");
        return -1;
    }
    int value = deque->data[deque->front];
    if (deque->front == deque->rear) {
        deque->front = deque->rear = -1;
    } else {
        deque->front = (deque->front + 1) % MAX;
    }
    return value;
}

int remove_rear(ArrayDeque* deque) {
    if (is_empty(deque)) {
        printf("Deque is empty\n");
        return -1;
    }
    int value = deque->data[deque->rear];
    if (deque->front == deque->rear) {
        deque->front = deque->rear = -1;
    } else {
        deque->rear = (deque->rear - 1 + MAX) % MAX;
    }
    return value;
}

int main() {
    ArrayDeque deque;
    init(&deque);

    add_front(&deque, 1);
    add_rear(&deque, 2);

    printf("%d\n", remove_front(&deque)); // 출력: 1
    printf("%d\n", remove_rear(&deque));  // 출력: 2

    return 0;
}
```
- **연결 리스트 기반 데크 (Linked List-based Deque)**
    - 연결 리스트로 구현되어 양방향 접근이 가능
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int data;
    struct Node* prev;
    struct Node* next;
} Node;

typedef struct {
    Node* front;
    Node* rear;
} LinkedListDeque;

void init(LinkedListDeque* deque) {
    deque->front = deque->rear = NULL;
}

void add_front(LinkedListDeque* deque, int value) {
    Node* new_node = (Node*)malloc(sizeof(Node));
    new_node->data = value;
    new_node->prev = NULL;
    new_node->next = deque->front;

    if (deque->front) {
        deque->front->prev = new_node;
    } else {
        deque->rear = new_node;
    }
    deque->front = new_node;
}

void add_rear(LinkedListDeque* deque, int value) {
    Node* new_node = (Node*)malloc(sizeof(Node));
    new_node->data = value;
    new_node->next = NULL;
    new_node->prev = deque->rear;

    if (deque->rear) {
        deque->rear->next = new_node;
    } else {
        deque->front = new_node;
    }
    deque->rear = new_node;
}

int remove_front(LinkedListDeque* deque) {
    if (!deque->front) {
        printf("Deque is empty\n");
        return -1;
    }
    Node* temp = deque->front;
    int value = temp->data;
    deque->front = deque->front->next;
    if (deque->front) {
        deque->front->prev = NULL;
    } else {
        deque->rear = NULL;
    }
    free(temp);
    return value;
}

int remove_rear(LinkedListDeque* deque) {
    if (!deque->rear) {
        printf("Deque is empty\n");
        return -1;
    }
    Node* temp = deque->rear;
    int value = temp->data;
    deque->rear = deque->rear->prev;
    if (deque->rear) {
        deque->rear->next = NULL;
    } else {
        deque->front = NULL;
    }
    free(temp);
    return value;
}

int main() {
    LinkedListDeque deque;
    init(&deque);

    add_front(&deque, 1);
    add_rear(&deque, 2);

    printf("%d\n", remove_front(&deque)); // 출력: 1
    printf("%d\n", remove_rear(&deque));  // 출력: 2

    return 0;
}
```
---

### **트리 (Tree)**

### 1. **트리 (Tree)**

- **일반 트리**: 각 노드가 여러 자식을 가질 수 있습니다.
![image](image%20(12).png)

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode {
    int data;
    struct TreeNode** children;
    int child_count;
} TreeNode;

TreeNode* create_node(int data) {
    TreeNode* new_node = (TreeNode*)malloc(sizeof(TreeNode));
    new_node->data = data;
    new_node->children = NULL;
    new_node->child_count = 0;
    return new_node;
}

void add_child(TreeNode* parent, TreeNode* child) {
    parent->child_count++;
    parent->children = (TreeNode**)realloc(parent->children, parent->child_count * sizeof(TreeNode*));
    parent->children[parent->child_count - 1] = child;
}

// Example usage
int main() {
    TreeNode* root = create_node(1);
    TreeNode* child1 = create_node(2);
    TreeNode* child2 = create_node(3);
    add_child(root, child1);
    add_child(root, child2);
    return 0;
}
```
- **Left-child-right-sibling 트리**: 일반 트리를 표현하는 구조로, 왼쪽 자식과 오른쪽 형제를 연결
![image](./image%20(13).png)
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct LCRSTreeNode {
    int data;
    struct LCRSTreeNode* left_child;
    struct LCRSTreeNode* right_sibling;
} LCRSTreeNode;

LCRSTreeNode* create_node(int data) {
    LCRSTreeNode* new_node = (LCRSTreeNode*)malloc(sizeof(LCRSTreeNode));
    new_node->data = data;
    new_node->left_child = NULL;
    new_node->right_sibling = NULL;
    return new_node;
}

// Example usage
int main() {
    LCRSTreeNode* root = create_node(1);
    LCRSTreeNode* child1 = create_node(2);
    LCRSTreeNode* child2 = create_node(3);
    root->left_child = child1;
    child1->right_sibling = child2;
    return 0;
}
```

### 2. **트리 순회**

- **전위 순회 (Pre-order Traversal)**: 노드 → 왼쪽 자식 → 오른쪽 자식
![image](./image%20(14).png)
**CBAEDFG**
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode {
    int data;
    struct TreeNode* left;
    struct TreeNode* right;
} TreeNode;

TreeNode* create_node(int data) {
    TreeNode* new_node = (TreeNode*)malloc(sizeof(TreeNode));
    new_node->data = data;
    new_node->left = new_node->right = NULL;
    return new_node;
}

void preorder_traversal(TreeNode* root) {
    if (root) {
        printf("%d ", root->data);
        preorder_traversal(root->left);
        preorder_traversal(root->right);
    }
}

int main() {
    TreeNode* root = create_node(1);
    root->left = create_node(2);
    root->right = create_node(3);
    root->left->left = create_node(4);
    root->left->right = create_node(5);

    preorder_traversal(root);  // Output: 1 2 4 5 3
    return 0;
}
```
- **중위 순회 (In-order Traversal)**: 왼쪽 자식 → 노드 → 오른쪽 자식.
![image](./image%20(14).png)
**ABCDEFG**
```c
void inorder_traversal(TreeNode* root) {
    if (root) {
        inorder_traversal(root->left);
        printf("%d ", root->data);
        inorder_traversal(root->right);
    }
}

int main() {
    inorder_traversal(root);  // Output: 4 2 5 1 3
    return 0;
}
```
- **후위 순회 (Post-order Traversal)**: 왼쪽 자식 → 오른쪽 자식 → 노드
![image](./image%20(14).png)
**ABDGFEC**
```c
void postorder_traversal(TreeNode* root) {
    if (root) {
        postorder_traversal(root->left);
        postorder_traversal(root->right);
        printf("%d ", root->data);
    }
}

int main() {
    postorder_traversal(root);  // Output: 4 5 2 3 1
    return 0;
}
```
- **레벨 순회 (Level-order Traversal)**: BFS(너비 우선 탐색) 방식으로 순회
![image](./image%20(15).png)
**ABCDEFG**
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode {
    int data;
    struct TreeNode* left;
    struct TreeNode* right;
} TreeNode;

typedef struct Queue {
    TreeNode* data;
    struct Queue* next;
} Queue;

Queue* create_queue_node(TreeNode* node) {
    Queue* new_node = (Queue*)malloc(sizeof(Queue));
    new_node->data = node;
    new_node->next = NULL;
    return new_node;
}

void enqueue(Queue** front, Queue** rear, TreeNode* node) {
    Queue* new_node = create_queue_node(node);
    if (*rear == NULL) {
        *front = *rear = new_node;
        return;
    }
    (*rear)->next = new_node;
    *rear = new_node;
}

TreeNode* dequeue(Queue** front) {
    if (*front == NULL) return NULL;
    Queue* temp = *front;
    TreeNode* node = temp->data;
    *front = (*front)->next;
    free(temp);
    return node;
}

void level_order_traversal(TreeNode* root) {
    if (!root) return;
    Queue* front = NULL;
    Queue* rear = NULL;
    enqueue(&front, &rear, root);
    while (front != NULL) {
        TreeNode* node = dequeue(&front);
        printf("%d ", node->data);
        if (node->left) enqueue(&front, &rear, node->left);
        if (node->right) enqueue(&front, &rear, node->right);
    }
}

int main() {
    level_order_traversal(root);  // Output: 1 2 3 4 5
    return 0;
}
```
### 3. **이진 트리 (Binary Tree)**

- **포화 이진 트리**: 모든 노드가 0개 또는 2개의 자식을 가짐
![image](./image%20(16).png)
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct FullBinaryTreeNode {
    int data;
    struct FullBinaryTreeNode* left;
    struct FullBinaryTreeNode* right;
} FullBinaryTreeNode;

FullBinaryTreeNode* create_node(int data) {
    FullBinaryTreeNode* new_node = (FullBinaryTreeNode*)malloc(sizeof(FullBinaryTreeNode));
    new_node->data = data;
    new_node->left = new_node->right = NULL;
    return new_node;
}

int main() {
    FullBinaryTreeNode* root = create_node(1);
    root->left = create_node(2);
    root->right = create_node(3);
    root->left->left = create_node(4);
    root->left->right = create_node(5);
    root->right->left = create_node(6);
    root->right->right = create_node(7);
    return 0;
}
```
- **완전 이진 트리**: 마지막 레벨을 제외한 모든 레벨이 채워져 있고, 노드가 왼쪽부터 채워짐
![image](./image%20(17).png)
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct CompleteBinaryTreeNode {
    int data;
    struct CompleteBinaryTreeNode* left;
    struct CompleteBinaryTreeNode* right;
} CompleteBinaryTreeNode;

CompleteBinaryTreeNode* create_node(int data) {
    CompleteBinaryTreeNode* new_node = (CompleteBinaryTreeNode*)malloc(sizeof(CompleteBinaryTreeNode));
    new_node->data = data;
    new_node->left = new_node->right = NULL;
    return new_node;
}

int main() {
    CompleteBinaryTreeNode* root = create_node(1);
    root->left = create_node(2);
    root->right = create_node(3);
    root->left->left = create_node(4);
    root->left->right = create_node(5);
    root->right->left = create_node(6);
    return 0;
}
```
- **경사 트리**: 모든 노드가 한쪽으로만 치우친 트리
![image](./image%20(18).png)
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct SkewedTreeNode {
    int data;
    struct SkewedTreeNode* left;
    struct SkewedTreeNode* right;
} SkewedTreeNode;

SkewedTreeNode* create_node(int data) {
    SkewedTreeNode* new_node = (SkewedTreeNode*)malloc(sizeof(SkewedTreeNode));
    new_node->data = data;
    new_node->left = new_node->right = NULL;
    return new_node;
}

int main() {
    SkewedTreeNode* root = create_node(1);
    root->left = create_node(2);
    root->left->left = create_node(3);
    root->left->left->left = create_node(4);
    return 0;
}
```
- **수식 트리**: 연산자와 피연산자를 노드로 표현하는 트리
![image](./image%20(19).png)
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct ExpressionTreeNode {
    char data;
    struct ExpressionTreeNode* left;
    struct ExpressionTreeNode* right;
} ExpressionTreeNode;

ExpressionTreeNode* create_node(char data) {
    ExpressionTreeNode* new_node = (ExpressionTreeNode*)malloc(sizeof(ExpressionTreeNode));
    new_node->data = data;
    new_node->left = new_node->right = NULL;
    return new_node;
}

void inorder_traversal(ExpressionTreeNode* root) {
    if (root) {
        inorder_traversal(root->left);
        printf("%c ", root->data);
        inorder_traversal(root->right);
    }
}

int main() {
    ExpressionTreeNode* root = create_node('*');
    root->left = create_node('+');
    root->right = create_node('-');

    root->left->left = create_node('a');
    root->left->right = create_node('b');
    root->right->left = create_node('c');
    root->right->right = create_node('d');

    inorder_traversal(root);  // Output: a + b * c - d
    return 0;
}
```
### 4. **이진 탐색 트리 (Binary Search Tree)**

- 모든 왼쪽 서브트리 값 < 루트 값 < 오른쪽 서브트리 값
![image](./image%20(20).png)
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct BSTNode {
    int key;
    struct BSTNode* left;
    struct BSTNode* right;
} BSTNode;

BSTNode* insert(BSTNode* root, int key) {
    if (root == NULL) {
        BSTNode* new_node = (BSTNode*)malloc(sizeof(BSTNode));
        new_node->key = key;
        new_node->left = new_node->right = NULL;
        return new_node;
    }
    
    if (key < root->key)
        root->left = insert(root->left, key);
    else
        root->right = insert(root->right, key);
    
    return root;
}

void inorder_traversal(BSTNode* root) {
    if (root != NULL) {
        inorder_traversal(root->left);
        printf("%d ", root->key);
        inorder_traversal(root->right);
    }
}

int main() {
    BSTNode* root = NULL;
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 70);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 60);
    root = insert(root, 80);

    inorder_traversal(root);  // Output: 20 30 40 50 60 70 80
    return 0;
}
```
- **균형 이진 탐색 트리 (Balanced BST)**
    - **AVL 트리** :모든 노드에서 왼쪽 서브트리와 오른쪽 서브트리의 높이 차이가 최대 1이 되도록 유지하는 트리
    ```c
    #include <stdio.h>
    #include <stdlib.h>

    typedef struct Node {
        int key;
        struct Node *left, *right;
        int height;
    } Node;

    // 헬퍼 함수: 노드의 높이 계산
    int height(Node *n) {
        return n ? n->height : 0;
    }

    // 헬퍼 함수: 최대값 계산
    int max(int a, int b) {
        return (a > b) ? a : b;
    }

    // 새 노드 생성
    Node *createNode(int key) {
        Node *node = (Node *)malloc(sizeof(Node));
        node->key = key;
        node->left = node->right = NULL;
        node->height = 1;
        return node;
    }

    // 오른쪽 회전
    Node *rightRotate(Node *y) {
        Node *x = y->left;
        Node *T2 = x->right;

        x->right = y;
        y->left = T2;

        y->height = max(height(y->left), height(y->right)) + 1;
        x->height = max(height(x->left), height(x->right)) + 1;

        return x;
    }

    // 왼쪽 회전
    Node *leftRotate(Node *x) {
        Node *y = x->right;
        Node *T2 = y->left;

        y->left = x;
        x->right = T2;

        x->height = max(height(x->left), height(x->right)) + 1;
        y->height = max(height(y->left), height(y->right)) + 1;

        return y;
    }

    // 균형 팩터 계산
    int getBalance(Node *n) {
        return n ? height(n->left) - height(n->right) : 0;
    }

    // 노드 삽입
    Node *insert(Node *node, int key) {
        if (!node)
            return createNode(key);

        if (key < node->key)
            node->left = insert(node->left, key);
        else if (key > node->key)
            node->right = insert(node->right, key);
        else
            return node;

        node->height = 1 + max(height(node->left), height(node->right));
        int balance = getBalance(node);

        // LL Case
        if (balance > 1 && key < node->left->key)
            return rightRotate(node);
        // RR Case
        if (balance < -1 && key > node->right->key)
            return leftRotate(node);
        // LR Case
        if (balance > 1 && key > node->left->key) {
            node->left = leftRotate(node->left);
            return rightRotate(node);
        }
        // RL Case
        if (balance < -1 && key < node->right->key) {
            node->right = rightRotate(node->right);
            return leftRotate(node);
        }

        return node;
    }

    // 트리 출력
    void preOrder(Node *root) {
        if (root) {
            printf("%d ", root->key);
            preOrder(root->left);
            preOrder(root->right);
        }
    }

    int main() {
        Node *root = NULL;

        root = insert(root, 10);
        root = insert(root, 20);
        root = insert(root, 30);
        root = insert(root, 40);
        root = insert(root, 50);
        root = insert(root, 25);

        printf("Pre-order traversal of the AVL tree is:\n");
        preOrder(root);

        return 0;
    }
    ```
    - **레드-블랙 트리**:노드에 색상(빨강 또는 검정)을 지정하여 트리의 균형을 유지
    ```c
    #include <stdio.h>
    #include <stdlib.h>

    typedef enum { RED, BLACK } Color;

    typedef struct Node {
        int data;
        Color color;
        struct Node *left, *right, *parent;
    } Node;

    // 새 노드 생성
    Node* createNode(int data) {
        Node* node = (Node*)malloc(sizeof(Node));
        node->data = data;
        node->color = RED;  // 새 노드는 항상 빨강
        node->left = node->right = node->parent = NULL;
        return node;
    }

    // 왼쪽 회전
    Node* leftRotate(Node* root, Node* x) {
        Node* y = x->right;
        x->right = y->left;

        if (y->left != NULL)
            y->left->parent = x;

        y->parent = x->parent;

        if (x->parent == NULL)
            root = y;
        else if (x == x->parent->left)
            x->parent->left = y;
        else
            x->parent->right = y;

        y->left = x;
        x->parent = y;

        return root;
    }

    // 오른쪽 회전
    Node* rightRotate(Node* root, Node* y) {
        Node* x = y->left;
        y->left = x->right;

        if (x->right != NULL)
            x->right->parent = y;

        x->parent = y->parent;

        if (y->parent == NULL)
            root = x;
        else if (y == y->parent->left)
            y->parent->left = x;
        else
            y->parent->right = x;

        x->right = y;
        y->parent = x;

        return root;
    }

    // 색상 및 구조 조정
    Node* fixViolation(Node* root, Node* z) {
        while (z->parent != NULL && z->parent->color == RED) {
            if (z->parent == z->parent->parent->left) {
                Node* y = z->parent->parent->right;  // 삼촌 노드
                if (y != NULL && y->color == RED) {  // Case 1: 삼촌이 빨강
                    z->parent->color = BLACK;
                    y->color = BLACK;
                    z->parent->parent->color = RED;
                    z = z->parent->parent;
                } else {  // 삼촌이 검정
                    if (z == z->parent->right) {  // Case 2: z가 오른쪽 자식
                        z = z->parent;
                        root = leftRotate(root, z);
                    }
                    // Case 3: z가 왼쪽 자식
                    z->parent->color = BLACK;
                    z->parent->parent->color = RED;
                    root = rightRotate(root, z->parent->parent);
                }
            } else {  // 부모가 오른쪽 자식인 경우 (대칭)
                Node* y = z->parent->parent->left;
                if (y != NULL && y->color == RED) {
                    z->parent->color = BLACK;
                    y->color = BLACK;
                    z->parent->parent->color = RED;
                    z = z->parent->parent;
                } else {
                    if (z == z->parent->left) {
                        z = z->parent;
                        root = rightRotate(root, z);
                    }
                    z->parent->color = BLACK;
                    z->parent->parent->color = RED;
                    root = leftRotate(root, z->parent->parent);
                }
            }
        }
        root->color = BLACK;
        return root;
    }

    // 삽입
    Node* insert(Node* root, int data) {
        Node* z = createNode(data);
        Node* y = NULL;
        Node* x = root;

        while (x != NULL) {
            y = x;
            if (z->data < x->data)
                x = x->left;
            else
                x = x->right;
        }

        z->parent = y;
        if (y == NULL)
            root = z;
        else if (z->data < y->data)
            y->left = z;
        else
            y->right = z;

        return fixViolation(root, z);
    }

    // 트리 출력
    void inorder(Node* root) {
        if (root != NULL) {
            inorder(root->left);
            printf("%d (%s) ", root->data, root->color == RED ? "RED" : "BLACK");
            inorder(root->right);
        }
    }

    int main() {
        Node* root = NULL;

        root = insert(root, 10);
        root = insert(root, 20);
        root = insert(root, 30);
        root = insert(root, 15);
        root = insert(root, 25);

        printf("Inorder traversal of the Red-Black Tree:\n");
        inorder(root);

        return 0;
    }
    ```
    - **Splay 트리**:최근에 접근한 노드를 루트로 이동시켜 이후 연산의 효율성을 높임
    ```c
    #include <stdio.h>
    #include <stdlib.h>

    typedef struct Node {
        int key;
        struct Node *left, *right;
    } Node;

    // 새 노드 생성
    Node *createNode(int key) {
        Node *node = (Node *)malloc(sizeof(Node));
        node->key = key;
        node->left = node->right = NULL;
        return node;
    }

    // 오른쪽 회전
    Node *rightRotate(Node *x) {
        Node *y = x->left;
        x->left = y->right;
        y->right = x;
        return y;
    }

    // 왼쪽 회전
    Node *leftRotate(Node *x) {
        Node *y = x->right;
        x->right = y->left;
        y->left = x;
        return y;
    }

    // 스플레이 연산
    Node *splay(Node *root, int key) {
        if (!root || root->key == key)
            return root;

        if (key < root->key) {
            if (!root->left)
                return root;

            if (key < root->left->key) {
                root->left->left = splay(root->left->left, key);
                root = rightRotate(root);
            } else if (key > root->left->key) {
                root->left->right = splay(root->left->right, key);
                if (root->left->right)
                    root->left = leftRotate(root->left);
            }

            return root->left ? rightRotate(root) : root;
        } else {
            if (!root->right)
                return root;

            if (key > root->right->key) {
                root->right->right = splay(root->right->right, key);
                root = leftRotate(root);
            } else if (key < root->right->key) {
                root->right->left = splay(root->right->left, key);
                if (root->right->left)
                    root->right = rightRotate(root->right);
            }

            return root->right ? leftRotate(root) : root;
        }
    }

    // 삽입
    Node *insert(Node *root, int key) {
        if (!root)
            return createNode(key);

        root = splay(root, key);

        if (root->key == key)
            return root;

        Node *newNode = createNode(key);

        if (key < root->key) {
            newNode->right = root;
            newNode->left = root->left;
            root->left = NULL;
        } else {
            newNode->left = root;
            newNode->right = root->right;
            root->right = NULL;
        }

        return newNode;
    }

    // 출력
    void preOrder(Node *root) {
        if (root) {
            printf("%d ", root->key);
            preOrder(root->left);
            preOrder(root->right);
        }
    }

    int main() {
        Node *root = NULL;

        root = insert(root, 10);
        root = insert(root, 20);
        root = insert(root, 30);
        root = splay(root, 20);

        printf("Pre-order traversal after splay operation:\n");
        preOrder(root);

        return 0;
    }
    ```
- **B 트리 계열**
    - **B 트리**: 모든 노드가 정렬된 키를 가지고 있으며, 키와 자식 노드 간의 관계는 이진 탐색 규칙을 따른다 또한 각 노드는 최소 t-1개에서 최대 2t-1개의 키를 가짐
    - **B+ 트리**: 리프 노드만 데이터(키)를 저장하며, 내부 노드는 탐색을 위한 키만 포함
  - **B* 트리**: B 트리의 노드 분할 전략을 개선한 구조, 노드의 2/3 이상이 채워지도록 설계됨

### 5. **힙 (Heap)**

- **최대 힙 (Max-Heap)**: 부모가 자식보다 큼
![image](./image%20(21).png)
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

void heapify(int arr[], int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < n && arr[left] > arr[largest]) {
        largest = left;
    }

    if (right < n && arr[right] > arr[largest]) {
        largest = right;
    }

    if (largest != i) {
        int temp = arr[i];
        arr[i] = arr[largest];
        arr[largest] = temp;

        heapify(arr, n, largest);
    }
}

void insert(int arr[], int* n, int key) {
    arr[*n] = key;
    (*n)++;
    
    for (int i = (*n) / 2 - 1; i >= 0; i--) {
        heapify(arr, *n, i);
    }
}

int main() {
    int heap[MAX_SIZE];
    int n = 0;

    insert(heap, &n, 10);
    insert(heap, &n, 20);
    insert(heap, &n, 5);

    // 최대 힙의 루트 출력
    printf("Max value: %d\n", heap[0]);  // Output: 20
    return 0;
}
```
- **최소 힙 (Min-Heap)**: 부모가 자식보다 작습니다.
![image](./image%20(22).png)
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

void heapify(int arr[], int n, int i) {
    int smallest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < n && arr[left] < arr[smallest]) {
        smallest = left;
    }

    if (right < n && arr[right] < arr[smallest]) {
        smallest = right;
    }

    if (smallest != i) {
        int temp = arr[i];
        arr[i] = arr[smallest];
        arr[smallest] = temp;

        heapify(arr, n, smallest);
    }
}

void insert(int arr[], int* n, int key) {
    arr[*n] = key;
    (*n)++;
    
    for (int i = (*n) / 2 - 1; i >= 0; i--) {
        heapify(arr, *n, i);
    }
}

int main() {
    int heap[MAX_SIZE];
    int n = 0;

    insert(heap, &n, 10);
    insert(heap, &n, 20);
    insert(heap, &n, 5);

    // 최소 힙의 루트 출력
    printf("Min value: %d\n", heap[0]);  // Output: 5
    return 0;
}
```
- **피보나치 힙**: 삽입/삭제가 매우 효율적

### 6. **분리 집합 (Disjoint Set)**

- **Union-Find 알고리즘**: 서로소 집합을 관리하는 자료구조
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 100

int parent[MAX];
int rank[MAX];

void make_set(int n) {
    for (int i = 0; i < n; i++) {
        parent[i] = i;
        rank[i] = 0;
    }
}

int find(int x) {
    if (parent[x] != x) {
        parent[x] = find(parent[x]);  // 경로 압축
    }
    return parent[x];
}

void union_sets(int x, int y) {
    int rootX = find(x);
    int rootY = find(y);

    if (rootX != rootY) {
        // 크기 조정: 작은 트리를 큰 트리 아래에 둠
        if (rank[rootX] > rank[rootY]) {
            parent[rootY] = rootX;
        } else if (rank[rootX] < rank[rootY]) {
            parent[rootX] = rootY;
        } else {
            parent[rootY] = rootX;
            rank[rootX]++;
        }
    }
}

int main() {
    make_set(5);
    union_sets(0, 1);
    union_sets(1, 2);
    printf("Find(0): %d\n", find(0));  // Output: 0
    printf("Find(2): %d\n", find(2));  // Output: 0
    return 0;
}
```
- **경로 압축 및 크기 조정**: 경로 압축과 집합 병합으로 효율성을 높임

---

### **그래프 (Graph)**
:데이터 간의 관게를 표현해야할 때 사용용
### 1. **그래프 (Graph)**

- **방향 그래프**: 간선에 방향이 있음
![image](./image%20(23).png)
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 10

struct Graph {
    int adj[MAX][MAX];
    int vertices;
};

void initGraph(struct Graph* g, int vertices) {
    g->vertices = vertices;
    for (int i = 0; i < vertices; i++) {
        for (int j = 0; j < vertices; j++) {
            g->adj[i][j] = 0;
        }
    }
}

void addEdge(struct Graph* g, int u, int v) {
    g->adj[u][v] = 1;  // 방향성 있는 간선
}

void display(struct Graph* g) {
    for (int i = 0; i < g->vertices; i++) {
        printf("%d -> ", i);
        for (int j = 0; j < g->vertices; j++) {
            if (g->adj[i][j]) {
                printf("%d ", j);
            }
        }
        printf("\n");
    }
}

int main() {
    struct Graph g;
    initGraph(&g, 3);
    addEdge(&g, 0, 1);
    addEdge(&g, 0, 2);
    addEdge(&g, 1, 2);
    display(&g);
    return 0;
}
```
- **무방향 그래프**: 간선에 방향이 없음
![image](./image%20(24).png)
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 10

struct Graph {
    int adj[MAX][MAX];
    int vertices;
};

void initGraph(struct Graph* g, int vertices) {
    g->vertices = vertices;
    for (int i = 0; i < vertices; i++) {
        for (int j = 0; j < vertices; j++) {
            g->adj[i][j] = 0;
        }
    }
}

void addEdge(struct Graph* g, int u, int v) {
    g->adj[u][v] = 1;  // 양방향 간선
    g->adj[v][u] = 1;
}

void display(struct Graph* g) {
    for (int i = 0; i < g->vertices; i++) {
        printf("%d <-> ", i);
        for (int j = 0; j < g->vertices; j++) {
            if (g->adj[i][j]) {
                printf("%d ", j);
            }
        }
        printf("\n");
    }
}

int main() {
    struct Graph g;
    initGraph(&g, 3);
    addEdge(&g, 0, 1);
    addEdge(&g, 0, 2);
    addEdge(&g, 1, 2);
    display(&g);
    return 0;
}
```
- **가중 그래프**: 간선에 가중치가 있음
![image](./image%20(25).png)
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 10

struct WeightedGraph {
    int adj[MAX][MAX];
    int vertices;
};

void initGraph(struct WeightedGraph* g, int vertices) {
    g->vertices = vertices;
    for (int i = 0; i < vertices; i++) {
        for (int j = 0; j < vertices; j++) {
            g->adj[i][j] = -1;  // -1은 간선이 없음을 의미
        }
    }
}

void addEdge(struct WeightedGraph* g, int u, int v, int weight) {
    g->adj[u][v] = weight;  // 가중치 있는 간선
}

void display(struct WeightedGraph* g) {
    for (int i = 0; i < g->vertices; i++) {
        printf("%d -> ", i);
        for (int j = 0; j < g->vertices; j++) {
            if (g->adj[i][j] != -1) {
                printf("%d(%d) ", j, g->adj[i][j]);
            }
        }
        printf("\n");
    }
}

int main() {
    struct WeightedGraph g;
    initGraph(&g, 3);
    addEdge(&g, 0, 1, 10);
    addEdge(&g, 0, 2, 5);
    addEdge(&g, 1, 2, 2);
    display(&g);
    return 0;
}
```
- **비가중 그래프**: 간선에 가중치가 없음음
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 10

struct Graph {
    int adj[MAX][MAX];
    int vertices;
};

void initGraph(struct Graph* g, int vertices) {
    g->vertices = vertices;
    for (int i = 0; i < vertices; i++) {
        for (int j = 0; j < vertices; j++) {
            g->adj[i][j] = 0;
        }
    }
}

void addEdge(struct Graph* g, int u, int v) {
    g->adj[u][v] = 1;  // 간선 추가
}

void display(struct Graph* g) {
    for (int i = 0; i < g->vertices; i++) {
        printf("%d -> ", i);
        for (int j = 0; j < g->vertices; j++) {
            if (g->adj[i][j]) {
                printf("%d ", j);
            }
        }
        printf("\n");
    }
}

int main() {
    struct Graph g;
    initGraph(&g, 3);
    addEdge(&g, 0, 1);
    addEdge(&g, 0, 2);
    addEdge(&g, 1, 2);
    display(&g);
    return 0;
}
```
### 2. **그래프 표현 방식**

- **인접 행렬**: 2차원 배열로 표현
![image](./image%20(26).png)
- **인접 리스트**: 리스트로 효율적으로 표현
![image](./image%20(27).png)

### 3. **그래프 순회**
![image](./image%20(28).png)
- **너비 우선 탐색 (BFS)**: 큐를 사용
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 10

struct Graph {
    int adj[MAX][MAX];
    int vertices;
};

void initGraph(struct Graph* g, int vertices) {
    g->vertices = vertices;
    for (int i = 0; i < vertices; i++) {
        for (int j = 0; j < vertices; j++) {
            g->adj[i][j] = 0;
        }
    }
}

void addEdge(struct Graph* g, int u, int v) {
    g->adj[u][v] = 1;
    g->adj[v][u] = 1;  // 무방향 그래프
}

void bfs(struct Graph* g, int start) {
    int visited[MAX] = {0};
    int queue[MAX];
    int front = 0, rear = 0;

    visited[start] = 1;
    queue[rear++] = start;

    while (front < rear) {
        int node = queue[front++];
        printf("%d ", node);

        for (int i = 0; i < g->vertices; i++) {
            if (g->adj[node][i] == 1 && !visited[i]) {
                visited[i] = 1;
                queue[rear++] = i;
            }
        }
    }
}

int main() {
    struct Graph g;
    initGraph(&g, 4);
    addEdge(&g, 0, 1);
    addEdge(&g, 0, 2);
    addEdge(&g, 1, 3);

    printf("BFS starting from vertex 0:\n");
    bfs(&g, 0);

    return 0;
}
```
- **깊이 우선 탐색 (DFS)**: 스택이나 재귀를 사용
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 10

struct Graph {
    int adj[MAX][MAX];
    int vertices;
};

void initGraph(struct Graph* g, int vertices) {
    g->vertices = vertices;
    for (int i = 0; i < vertices; i++) {
        for (int j = 0; j < vertices; j++) {
            g->adj[i][j] = 0;
        }
    }
}

void addEdge(struct Graph* g, int u, int v) {
    g->adj[u][v] = 1;
    g->adj[v][u] = 1;  // 무방향 그래프
}

void dfs(struct Graph* g, int start, int visited[MAX]) {
    visited[start] = 1;
    printf("%d ", start);

    for (int i = 0; i < g->vertices; i++) {
        if (g->adj[start][i] == 1 && !visited[i]) {
            dfs(g, i, visited);
        }
    }
}

int main() {
    struct Graph g;
    initGraph(&g, 4);
    addEdge(&g, 0, 1);
    addEdge(&g, 0, 2);
    addEdge(&g, 1, 3);

    int visited[MAX] = {0};

    printf("DFS starting from vertex 0:\n");
    dfs(&g, 0, visited);

    return 0;
}
```
### 4. **최단 경로 알고리즘**

- **다익스트라 알고리즘**: 양의 가중치 그래프의 최단 경로를 찾음
```c
#include <stdio.h>
#include <limits.h>

#define MAX 10
#define INF INT_MAX

void dijkstra(int graph[MAX][MAX], int n, int start) {
    int dist[MAX];
    int visited[MAX] = {0};

    for (int i = 0; i < n; i++) {
        dist[i] = INF;
    }
    dist[start] = 0;

    for (int count = 0; count < n - 1; count++) {
        int min = INF, u = -1;
        
        // 가장 작은 거리를 가진 정점 선택
        for (int v = 0; v < n; v++) {
            if (!visited[v] && dist[v] < min) {
                min = dist[v];
                u = v;
            }
        }

        visited[u] = 1;

        // u를 거쳐가는 더 짧은 경로가 있으면 업데이트
        for (int v = 0; v < n; v++) {
            if (!visited[v] && graph[u][v] != INF && dist[u] + graph[u][v] < dist[v]) {
                dist[v] = dist[u] + graph[u][v];
            }
        }
    }

    printf("Shortest distances from node %d:\n", start);
    for (int i = 0; i < n; i++) {
        printf("%d -> %d: %d\n", start, i, dist[i]);
    }
}

int main() {
    int graph[MAX][MAX] = {
        {0, 4, 1, INF},
        {4, 0, 2, 5},
        {1, 2, 0, 1},
        {INF, 5, 1, 0}
    };

    int n = 4; // 노드 개수
    int start = 0;

    dijkstra(graph, n, start);

    return 0;
}
```
- **벨만-포드 알고리즘**: 음의 가중치도 처리할 수 있음
```c
#include <stdio.h>
#include <limits.h>

#define MAX 10
#define INF INT_MAX

void bellman_ford(int graph[MAX][MAX], int vertices, int start) {
    int dist[MAX];
    
    for (int i = 0; i < vertices; i++) {
        dist[i] = INF;
    }
    dist[start] = 0;

    for (int i = 1; i < vertices; i++) {
        for (int u = 0; u < vertices; u++) {
            for (int v = 0; v < vertices; v++) {
                if (graph[u][v] != INF && dist[u] != INF && dist[u] + graph[u][v] < dist[v]) {
                    dist[v] = dist[u] + graph[u][v];
                }
            }
        }
    }

    // Negative weight cycle check
    for (int u = 0; u < vertices; u++) {
        for (int v = 0; v < vertices; v++) {
            if (graph[u][v] != INF && dist[u] != INF && dist[u] + graph[u][v] < dist[v]) {
                printf("Graph contains negative weight cycle\n");
                return;
            }
        }
    }

    printf("Shortest distances from node %d:\n", start);
    for (int i = 0; i < vertices; i++) {
        printf("%d -> %d: %d\n", start, i, dist[i]);
    }
}

int main() {
    int graph[MAX][MAX] = {
        {0, -1, 4, INF, INF},
        {INF, 0, 3, 2, 2},
        {INF, INF, 0, 5, INF},
        {INF, INF, INF, 0, -3},
        {INF, INF, INF, INF, 0}
    };
    int vertices = 5;
    int start = 0;

    bellman_ford(graph, vertices, start);

    return 0;
}
```
- **플로이드-워셜 알고리즘**: 모든 노드 쌍의 최단 경로를 찾음
```c
#include <stdio.h>
#include <limits.h>

#define MAX 10
#define INF INT_MAX

void floyd_warshall(int graph[MAX][MAX], int vertices) {
    int dist[MAX][MAX];

    for (int i = 0; i < vertices; i++) {
        for (int j = 0; j < vertices; j++) {
            dist[i][j] = graph[i][j];
        }
    }

    for (int k = 0; k < vertices; k++) {
        for (int i = 0; i < vertices; i++) {
            for (int j = 0; j < vertices; j++) {
                if (dist[i][j] > dist[i][k] + dist[k][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }

    printf("Floyd-Warshall shortest paths:\n");
    for (int i = 0; i < vertices; i++) {
        for (int j = 0; j < vertices; j++) {
            if (dist[i][j] == INF) {
                printf("INF ");
            } else {
                printf("%d ", dist[i][j]);
            }
        }
        printf("\n");
    }
}

int main() {
    int graph[MAX][MAX] = {
        {0, 4, 1, INF},
        {4, 0, 3, 5},
        {1, 3, 0, 1},
        {INF, 5, 1, 0}
    };
    int vertices = 4;

    floyd_warshall(graph, vertices);

    return 0;
}
```
### 5. **최소 신장 트리 (MST)**

- **크루스칼 알고리즘**: 간선을 정렬하여 MST를 생성
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 10
#define INF 999999

typedef struct {
    int u, v, weight;
} Edge;

typedef struct {
    int parent[MAX];
    int rank[MAX];
} DisjointSet;

void init_ds(DisjointSet* ds, int n) {
    for (int i = 0; i < n; i++) {
        ds->parent[i] = i;
        ds->rank[i] = 0;
    }
}

int find(DisjointSet* ds, int u) {
    if (ds->parent[u] != u)
        ds->parent[u] = find(ds, ds->parent[u]);
    return ds->parent[u];
}

void union_sets(DisjointSet* ds, int u, int v) {
    int root_u = find(ds, u);
    int root_v = find(ds, v);
    
    if (root_u != root_v) {
        if (ds->rank[root_u] > ds->rank[root_v]) {
            ds->parent[root_v] = root_u;
        } else if (ds->rank[root_u] < ds->rank[root_v]) {
            ds->parent[root_u] = root_v;
        } else {
            ds->parent[root_v] = root_u;
            ds->rank[root_u]++;
        }
    }
}

int compare_edges(const void* a, const void* b) {
    return ((Edge*)a)->weight - ((Edge*)b)->weight;
}

void kruskal(int n, Edge edges[], int e) {
    DisjointSet ds;
    init_ds(&ds, n);
    qsort(edges, e, sizeof(Edge), compare_edges);

    printf("Kruskal's MST:\n");
    for (int i = 0; i < e; i++) {
        int u = edges[i].u;
        int v = edges[i].v;
        int weight = edges[i].weight;
        
        if (find(&ds, u) != find(&ds, v)) {
            printf("Edge (%d, %d) with weight %d\n", u, v, weight);
            union_sets(&ds, u, v);
        }
    }
}

int main() {
    Edge edges[] = {
        {0, 1, 10}, {0, 2, 6}, {0, 3, 5}, {1, 3, 15}, {2, 3, 4}
    };
    int n = 4; // 노드의 개수
    int e = sizeof(edges) / sizeof(edges[0]); // 간선의 개수

    kruskal(n, edges, e);
    return 0;
}
```
- **프림 알고리즘**: 연결된 정점에서 확장
```c
#include <stdio.h>
#include <limits.h>

#define MAX 10
#define INF INT_MAX

void prim(int n, int graph[MAX][MAX]) {
    int key[MAX], parent[MAX], visited[MAX];
    
    for (int i = 0; i < n; i++) {
        key[i] = INF;
        visited[i] = 0;
    }
    key[0] = 0;  // 시작 노드는 0으로 설정
    parent[0] = -1;

    for (int count = 0; count < n - 1; count++) {
        int u = -1;
        
        // key 값이 최소인 노드 선택
        for (int v = 0; v < n; v++) {
            if (!visited[v] && (u == -1 || key[v] < key[u])) {
                u = v;
            }
        }

        visited[u] = 1;

        // u를 거쳐가는 경로가 더 짧으면 갱신
        for (int v = 0; v < n; v++) {
            if (graph[u][v] != INF && !visited[v] && graph[u][v] < key[v]) {
                key[v] = graph[u][v];
                parent[v] = u;
            }
        }
    }

    printf("Prim's MST:\n");
    for (int i = 1; i < n; i++) {
        printf("Edge (%d, %d) with weight %d\n", parent[i], i, graph[parent[i]][i]);
    }
}

int main() {
    int graph[MAX][MAX] = {
        {INF, 10, 6, 5},
        {10, INF, INF, 15},
        {6, INF, INF, 4},
        {5, 15, 4, INF}
    };
    int n = 4; // 노드의 개수

    prim(n, graph);
    return 0;
}
```
### 6. **기타**

- **위상 정렬**: DAG의 정점 순서를 결정
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 10

void topological_sort(int n, int graph[MAX][MAX]) {
    int in_degree[MAX] = {0};
    for (int u = 0; u < n; u++) {
        for (int v = 0; v < n; v++) {
            if (graph[u][v] == 1) {
                in_degree[v]++;
            }
        }
    }

    int queue[MAX], front = 0, rear = -1;
    for (int i = 0; i < n; i++) {
        if (in_degree[i] == 0) {
            queue[++rear] = i;
        }
    }

    int result[MAX];
    int index = 0;
    
    while (front <= rear) {
        int u = queue[front++];
        result[index++] = u;

        for (int v = 0; v < n; v++) {
            if (graph[u][v] == 1) {
                in_degree[v]--;
                if (in_degree[v] == 0) {
                    queue[++rear] = v;
                }
            }
        }
    }

    if (index == n) {
        printf("Topological Sort: ");
        for (int i = 0; i < n; i++) {
            printf("%d ", result[i]);
        }
        printf("\n");
    } else {
        printf("Cycle detected, no topological sort possible.\n");
    }
}

int main() {
    int graph[MAX][MAX] = {
        {0, 1, 1, 0},
        {0, 0, 0, 1},
        {0, 0, 0, 1},
        {0, 0, 0, 0}
    };
    int n = 4; // 노드의 개수

    topological_sort(n, graph);
    return 0;
}
```
- **강결합 요소 탐색**: SCC를 찾음
- **이분 그래프 탐색**: 그래프가 두 그룹으로 나뉠 수 있는지 확인 

---

### **해시 (Hash)**
:빠른 검색과 삽입이 필요할 때 사용 
### 1. **해시 테이블**

- 키-값 쌍을 저장하며, 평균 O(1)의 접근 시간을 가짐 
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define TABLE_SIZE 10

typedef struct Entry {
    char key[100];
    int value;
    struct Entry* next;
} Entry;

Entry* hash_table[TABLE_SIZE];

// 해시 함수
unsigned int hash(char* key) {
    unsigned int hash_value = 0;
    for (int i = 0; key[i] != '\0'; i++) {
        hash_value = (hash_value << 5) + key[i];
    }
    return hash_value % TABLE_SIZE;
}

// 삽입
void insert(char* key, int value) {
    unsigned int index = hash(key);
    Entry* new_entry = (Entry*)malloc(sizeof(Entry));
    strcpy(new_entry->key, key);
    new_entry->value = value;
    new_entry->next = hash_table[index];
    hash_table[index] = new_entry;
}

// 조회
int search(char* key) {
    unsigned int index = hash(key);
    Entry* entry = hash_table[index];
    while (entry != NULL) {
        if (strcmp(entry->key, key) == 0) {
            return entry->value;
        }
        entry = entry->next;
    }
    return -1;  // 키가 없는 경우
}

int main() {
    insert("apple", 10);
    insert("banana", 20);

    printf("apple: %d\n", search("apple"));
    printf("banana: %d\n", search("banana"));
    
    return 0;
}
```
### 2. **충돌 처리**

- **개방 주소법**: 충돌 시 다른 빈 슬롯을 찾는다다
- **체이닝**: 연결 리스트로 충돌을 처리 

### 3. **블룸 필터 (Bloom Filter)**

- 확률적 자료구조로, 원소의 존재 여부를 빠르게 확인 