# 인공지능(Artificial Intelligence)

### 정렬 (Sorting)

### 기본 정렬 알고리즘

- **버블 정렬 (Bubble Sort)**
    
    인접한 두 요소를 비교하여 교환하며 정렬하는 알고리즘으로, 매 반복마다 가장 큰 값을 맨 뒤로 보냅니다.
    
    - 특징: 간단하지만 비효율적.
    - 시간 복잡도: O(n^2) (평균 및 최악의 경우)
    - 공간 복잡도: O(1)
    - 안정 정렬.
```c
#include <stdio.h>

void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr) / sizeof(arr[0]);
    bubbleSort(arr, n);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    return 0;
}
```
- **선택 정렬 (Selection Sort)**
    
    매번 남은 부분 중 가장 작은 값을 선택하여 현재 위치의 값과 교환하는 방식.
    
    - 특징: 교환 횟수가 적음.
    - 시간 복잡도: O(n^2)
    - 공간 복잡도: O(1)
    - 비안정 정렬.
```c
#include <stdio.h>

void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int min_idx = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[min_idx])
                min_idx = j;
        }
        int temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
    }
}

int main() {
    int arr[] = {64, 25, 12, 22, 11};
    int n = sizeof(arr) / sizeof(arr[0]);
    selectionSort(arr, n);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    return 0;
}
```
- **삽입 정렬 (Insertion Sort)**
    
    배열을 순회하며 현재 요소를 이미 정렬된 부분에 삽입하는 방식.
    
    - 특징: 데이터가 거의 정렬된 경우 효율적.
    - 시간 복잡도: O(n^2) (평균 및 최악의 경우), O(n) (최선의 경우)
    - 공간 복잡도: O(1)
    - 안정 정렬.
```c
#include <stdio.h>

void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]);
    insertionSort(arr, n);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    return 0;
}
```
### 고급 정렬 알고리즘

- **병합 정렬 (Merge Sort)**
    
    배열을 반으로 나눈 후 각각을 정렬하고 병합하여 정렬을 완성하는 재귀적 알고리즘.
    
    - 특징: 안정 정렬, 대량의 데이터 처리에 적합.
    - 시간 복잡도: O(n log n)
    - 공간 복잡도: O(n)
```c
#include <stdio.h>

void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    int L[n1], R[n2];

    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];

    int i = 0, j = 0, k = left;

    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);
    mergeSort(arr, 0, n - 1);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    return 0;
}
```
- **퀵 정렬 (Quick Sort)**
    
    피벗을 기준으로 작은 값과 큰 값으로 나누고 이를 재귀적으로 정렬하는 방식.
    
    - 특징: 평균적으로 빠르지만 최악의 경우 성능 저하.
    - 시간 복잡도: O(n log n) (평균), O(n^2) (최악)
    - 공간 복잡도: O(log n) (재귀 호출 스택)
    - 비안정 정렬.
```c
#include <stdio.h>

void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return (i + 1);
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int main() {
    int arr[] = {10, 7, 8, 9, 1, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    quickSort(arr, 0, n - 1);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    return 0;
}
```
- **힙 정렬 (Heap Sort)**
    
    힙 자료구조를 사용하여 최대값 또는 최소값을 반복적으로 제거하며 정렬.
    
    - 특징: 비재귀적으로 구현 가능.
    - 시간 복잡도: O(n log n)
    - 공간 복잡도: O(1)
    - 비안정 정렬.
```c
#include <stdio.h>

void heapify(int arr[], int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < n && arr[left] > arr[largest])
        largest = left;
    if (right < n && arr[right] > arr[largest])
        largest = right;

    if (largest != i) {
        int temp = arr[i];
        arr[i] = arr[largest];
        arr[largest] = temp;
        heapify(arr, n, largest);
    }
}

void heapSort(int arr[], int n) {
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    for (int i = n - 1; i >= 0; i--) {
        int temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;
        heapify(arr, i, 0);
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);
    heapSort(arr, n);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    return 0;
}
```
- **기수 정렬 (Radix Sort)**
    
    자릿수별로 정렬을 반복하여 숫자를 정렬. 비교 연산을 사용하지 않음.
    
    - 특징: 정렬 기준이 명확한 경우 효율적.
    - 시간 복잡도: O(nk) (k: 최대 자릿수)
    - 공간 복잡도: O(n + k)
    - 안정 정렬.
```c
#include <stdio.h>

void countingSort(int arr[], int n, int exp) {
    int output[n];
    int count[10] = {0};

    for (int i = 0; i < n; i++)
        count[(arr[i] / exp) % 10]++;

    for (int i = 1; i < 10; i++)
        count[i] += count[i - 1];

    for (int i = n - 1; i >= 0; i--) {
        output[count[(arr[i] / exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--;
    }

    for (int i = 0; i < n; i++)
        arr[i] = output[i];
}

void radixSort(int arr[], int n) {
    int max = arr[0];
    for (int i = 1; i < n; i++)
        if (arr[i] > max)
            max = arr[i];

    for (int exp = 1; max / exp > 0; exp *= 10)
        countingSort(arr, n, exp);
}

int main() {
    int arr[] = {170, 45, 75, 90, 802, 24, 2, 66};
    int n = sizeof(arr) / sizeof(arr[0]);
    radixSort(arr, n);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    return 0;
}
```
- **계수 정렬 (Counting Sort)**
    
    값의 빈도를 세어 정렬하는 방식. 데이터의 범위가 좁을수록 효율적.
    
    - 특징: 비교를 사용하지 않음.
    - 시간 복잡도: O(n + k) (k: 최대값 범위)
    - 공간 복잡도: O(k)
    - 안정 정렬.
```c
#include <stdio.h>
#include <string.h>

void countingSort(int arr[], int n) {
    int max = arr[0], min = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max) max = arr[i];
        if (arr[i] < min) min = arr[i];
    }

    int range = max - min + 1;
    int count[range];
    int output[n];

    memset(count, 0, sizeof(count));

    for (int i = 0; i < n; i++)
        count[arr[i] - min]++;

    for (int i = 1; i < range; i++)
        count[i] += count[i - 1];

    for (int i = n - 1; i >= 0; i--) {
        output[count[arr[i] - min] - 1] = arr[i];
        count[arr[i] - min]--;
    }

    for (int i = 0; i < n; i++)
        arr[i] = output[i];
}

int main() {
    int arr[] = {4, 2, 2, 8, 3, 3, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    countingSort(arr, n);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    return 0;
}
```
- **셸 정렬 (Shell Sort)**
    
    삽입 정렬의 확장으로, 특정 간격만큼 떨어진 요소를 정렬한 후 간격을 줄이며 정렬 완성.
    
    - 특징: 간단하고 구현 용이.
    - 시간 복잡도: O(n^(3/2)) (평균)
    - 공간 복잡도: O(1)
    - 비안정 정렬.
```c
#include <stdio.h>

void shellSort(int arr[], int n) {
    for (int gap = n / 2; gap > 0; gap /= 2) {
        for (int i = gap; i < n; i++) {
            int temp = arr[i];
            int j;
            for (j = i; j >= gap && arr[j - gap] > temp; j -= gap)
                arr[j] = arr[j - gap];
            arr[j] = temp;
        }
    }
}

int main() {
    int arr[] = {12, 34, 54, 2, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    shellSort(arr, n);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    return 0;
}
```
### 비교 기반 정렬과 비비교 기반 정렬의 차이

- **비교 기반 정렬**: 두 요소를 비교하여 순서를 결정. (예: 퀵 정렬, 병합 정렬, 힙 정렬)
    - 하한 시간 복잡도: O(n log n)
```c
#include <stdio.h>

void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);

    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return (i + 1);
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int main() {
    int arr[] = {10, 7, 8, 9, 1, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    quickSort(arr, 0, n - 1);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    return 0;
}
```
- **비비교 기반 정렬**: 비교 없이 다른 기법(빈도 계산 등)으로 정렬. (예: 계수 정렬, 기수 정렬)
    - 특정 조건에서 O(n) 시간 복잡도 가능.
```c
#include <stdio.h>
#include <string.h>

void countingSort(int arr[], int n, int max) {
    int count[max + 1];
    memset(count, 0, sizeof(count));

    for (int i = 0; i < n; i++)
        count[arr[i]]++;

    for (int i = 1; i <= max; i++)
        count[i] += count[i - 1];

    int output[n];
    for (int i = n - 1; i >= 0; i--) {
        output[count[arr[i]] - 1] = arr[i];
        count[arr[i]]--;
    }

    for (int i = 0; i < n; i++)
        arr[i] = output[i];
}

int main() {
    int arr[] = {4, 2, 2, 8, 3, 3, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    int max = 8;
    countingSort(arr, n, max);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    return 0;
}
```
---

### 탐색 (Search)

### 선형 탐색 (Linear Search)

- 배열의 처음부터 끝까지 순차적으로 탐색하며 값을 찾는 알고리즘.
    - 특징: 데이터가 정렬되지 않은 경우에도 사용 가능.
    - 시간 복잡도: O(n)
```c
#include <stdio.h>

int linear_search(int arr[], int size, int target) {
    for (int i = 0; i < size; i++) {
        if (arr[i] == target)
            return i;  // 값이 발견되면 인덱스 반환
    }
    return -1;  // 값이 없으면 -1 반환
}

int main() {
    int arr[] = {5, 3, 7, 1, 9};
    int target = 7;
    int size = sizeof(arr) / sizeof(arr[0]);
    printf("%d\n", linear_search(arr, size, target));  // 출력: 2
    return 0;
}
```
### 이진 탐색 (Binary Search)

- 정렬된 배열에서 중간값을 기준으로 탐색 범위를 반씩 줄이는 알고리즘.
    - 특징: 정렬된 데이터에서 매우 효율적.
    - 시간 복잡도: O(log n)
```c
#include <stdio.h>

int binary_search(int arr[], int size, int target) {
    int left = 0, right = size - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target)
            return mid;  // 값이 발견되면 인덱스 반환
        else if (arr[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return -1;  // 값이 없으면 -1 반환
}

int main() {
    int arr[] = {1, 3, 5, 7, 9};
    int target = 7;
    int size = sizeof(arr) / sizeof(arr[0]);
    printf("%d\n", binary_search(arr, size, target));  // 출력: 3
    return 0;
}
```
### 이진 탐색 변형

- Lower bound: 특정 값 이상의 첫 번째 위치를 찾음.
- Upper bound: 특정 값보다 큰 첫 번째 위치를 찾음.
    - 시간 복잡도: O(log n)
```c
#include <stdio.h>
#include <stdlib.h>

int lower_bound(int arr[], int size, int target) {
    int left = 0, right = size;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] < target)
            left = mid + 1;
        else
            right = mid;
    }
    return left;  // target보다 크거나 같은 첫 번째 인덱스 반환
}

int main() {
    int arr[] = {1, 3, 5, 7, 9};
    int target = 6;
    int size = sizeof(arr) / sizeof(arr[0]);
    printf("%d\n", lower_bound(arr, size, target));  // 출력: 3
    return 0;
}
```
### 탐색 알고리즘의 시간 복잡도 분석

- 데이터 크기와 정렬 여부가 시간 복잡도에 영향을 줌.

---

### 재귀 및 분할 정복

### 재귀 (Recursion)

- 함수가 자기 자신을 호출하여 문제를 해결하는 방식.
    - 예: 피보나치 수열 계산, 하노이 탑 문제.
```c
#include <stdio.h>

// 재귀를 사용한 팩토리얼 계산
int factorial(int n) {
    if (n == 0 || n == 1)
        return 1;
    else
        return n * factorial(n - 1);
}

int main() {
    int result = factorial(5);
    printf("%d\n", result);  // 출력: 120
    return 0;
}
```
### 분할 정복 (Divide and Conquer)

- 문제를 더 작은 문제로 나눈 뒤 해결하고 결과를 합쳐서 원래 문제를 해결.
```c
#include <stdio.h>

void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    int L[n1], R[n2];

    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];

    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }

    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void merge_sort(int arr[], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        merge_sort(arr, left, mid);
        merge_sort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

int main() {
    int arr[] = {3, 1, 4, 1, 5, 9, 2, 6};
    int n = sizeof(arr) / sizeof(arr[0]);
    merge_sort(arr, 0, n - 1);

    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    return 0;  // 출력: 1 1 2 3 4 5 6 9
}
```
### 백트래킹 (Backtracking)

- 모든 가능한 경우를 시도하되, 조건에 맞지 않으면 돌아가 다른 경우를 시도.
    - 예: N-Queen 문제, 미로 탐색.
```c
#include <stdio.h>
#include <stdbool.h>

bool is_safe(int board[], int row, int col) {
    for (int i = 0; i < row; i++) {
        if (board[i] == col || board[i] - i == col - row || board[i] + i == col + row)
            return false;
    }
    return true;
}

bool solve_n_queens(int board[], int row, int n) {
    if (row == n) {
        for (int i = 0; i < n; i++) {
            printf("%d ", board[i]);
        }
        printf("\n");
        return true;
    }
    bool res = false;
    for (int col = 0; col < n; col++) {
        if (is_safe(board, row, col)) {
            board[row] = col;
            res = solve_n_queens(board, row + 1, n) || res;
            board[row] = -1;  // 백트래킹
        }
    }
    return res;
}

void n_queens(int n) {
    int board[n];
    for (int i = 0; i < n; i++) {
        board[i] = -1;
    }
    solve_n_queens(board, 0, n);
}

int main() {
    n_queens(4);  // 출력: 1 3 0 2 (가능한 한 가지 배치)
    return 0;
}
```
---

### 그리디 알고리즘 (Greedy Algorithm)

### 개념 및 특징

- 현재 단계에서 가장 좋은 선택을 하여 최적해를 구하는 알고리즘.
    - 특징: 최적 부분 구조와 탐욕스러운 선택 속성이 필요.

### 대표 문제

- 동전 거슬러 주기: 가장 큰 단위의 동전을 먼저 선택.
```c
#include <stdio.h>

int coin_change(int coins[], int num_coins, int amount) {
    int count = 0;
    for (int i = 0; i < num_coins; i++) {
        if (amount >= coins[i]) {
            count += amount / coins[i];
            amount %= coins[i];
        }
    }
    return amount == 0 ? count : -1;
}

int main() {
    int coins[] = {1, 5, 10, 25};
    int amount = 63;
    printf("%d\n", coin_change(coins, 4, amount));  // 출력: 6
    return 0;
}
```
- 활동 선택 문제: 시작 시간이 빠르고 종료 시간이 빠른 활동을 선택.
```c
#include <stdio.h>
#include <stdlib.h>

// 활동을 끝나는 시간을 기준으로 정렬
int compare(const void *a, const void *b) {
    return ((*(int**)a)[1] - (*(int**)b)[1]);
}

void activity_selection(int activities[][2], int n) {
    qsort(activities, n, sizeof(activities[0]), compare);

    printf("선택된 활동: \n");
    int last_end_time = 0;
    for (int i = 0; i < n; i++) {
        if (activities[i][0] >= last_end_time) {
            printf("(%d, %d) ", activities[i][0], activities[i][1]);
            last_end_time = activities[i][1];
        }
    }
    printf("\n");
}

int main() {
    int activities[5][2] = {{1, 4}, {2, 6}, {5, 8}, {7, 9}, {3, 5}};
    activity_selection(activities, 5);  // 출력: (1, 4) (5, 8) (7, 9)
    return 0;
}
```
### 최소 신장 트리 (MST)

- **크루스칼 알고리즘**: 간선을 정렬하여 최소 비용으로 그래프를 연결.
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int u, v, weight;
} Edge;

int find(int parent[], int i) {
    if (parent[i] != i)
        parent[i] = find(parent, parent[i]);
    return parent[i];
}

void union_set(int parent[], int rank[], int x, int y) {
    int xroot = find(parent, x);
    int yroot = find(parent, y);
    if (rank[xroot] < rank[yroot])
        parent[xroot] = yroot;
    else if (rank[xroot] > rank[yroot])
        parent[yroot] = xroot;
    else {
        parent[yroot] = xroot;
        rank[xroot]++;
    }
}

int compare(const void *a, const void *b) {
    return ((Edge*)a)->weight - ((Edge*)b)->weight;
}

void kruskal(Edge edges[], int n, int m) {
    qsort(edges, m, sizeof(Edge), compare);

    int parent[n], rank[n];
    for (int i = 0; i < n; i++) {
        parent[i] = i;
        rank[i] = 0;
    }

    for (int i = 0; i < m; i++) {
        int u = edges[i].u;
        int v = edges[i].v;
        if (find(parent, u) != find(parent, v)) {
            printf("(%d, %d) - %d\n", u, v, edges[i].weight);
            union_set(parent, rank, u, v);
        }
    }
}

int main() {
    Edge edges[] = {{0, 1, 10}, {0, 2, 6}, {0, 3, 5}, {1, 3, 15}, {2, 3, 4}};
    int n = 4;  // 정점 수
    int m = 5;  // 간선 수
    kruskal(edges, n, m);  // 출력: (2, 3) - 4, (0, 3) - 5, (0, 1) - 10
    return 0;
}
```
- **프림 알고리즘**: 시작점에서 점차 영역을 확장하며 최소 비용 연결.
```c
#include <stdio.h>
#include <limits.h>

#define INF INT_MAX
#define N 5  // 정점 수

int minKey(int key[], int visited[]) {
    int min = INF, min_index;
    for (int v = 0; v < N; v++) {
        if (!visited[v] && key[v] < min) {
            min = key[v];
            min_index = v;
        }
    }
    return min_index;
}

void prim(int graph[N][N]) {
    int parent[N];
    int key[N];
    int visited[N];
    
    for (int i = 0; i < N; i++) {
        key[i] = INF;
        visited[i] = 0;
    }

    key[0] = 0;
    parent[0] = -1;

    for (int count = 0; count < N - 1; count++) {
        int u = minKey(key, visited);
        visited[u] = 1;

        for (int v = 0; v < N; v++) {
            if (graph[u][v] && !visited[v] && graph[u][v] < key[v]) {
                key[v] = graph[u][v];
                parent[v] = u;
            }
        }
    }

    printf("MST 구성: \n");
    int total_weight = 0;
    for (int i = 1; i < N; i++) {
        printf("(%d, %d) - %d\n", parent[i], i, graph[i][parent[i]]);
        total_weight += graph[i][parent[i]];
    }
    printf("Total weight: %d\n", total_weight);
}

int main() {
    int graph[N][N] = {
        {0, 1, 3, 2, 0},
        {1, 0, 0, 4, 5},
        {3, 0, 0, 5, 6},
        {2, 4, 5, 0, 7},
        {0, 5, 6, 7, 0}
    };
    
    prim(graph);
    return 0;
}
```
---

### 동적 계획법 (Dynamic Programming)

### 메모이제이션과 타뷸레이션

- **메모이제이션**: 재귀 호출 중 계산 결과를 저장.
- **타뷸레이션**: 작은 문제부터 해결해 저장된 값을 이용.

### 대표 문제

- 피보나치 수열: 중복 계산 제거.
```c
#include <stdio.h>

#define MAX 100
int memo[MAX];

// 메모이제이션
int fibonacci_memo(int n) {
    if (n <= 1) return n;
    if (memo[n] != -1) return memo[n];
    memo[n] = fibonacci_memo(n - 1) + fibonacci_memo(n - 2);
    return memo[n];
}

// 타뷸레이션
int fibonacci_tab(int n) {
    int fib[n + 1];
    fib[0] = 0;
    fib[1] = 1;
    for (int i = 2; i <= n; i++) {
        fib[i] = fib[i - 1] + fib[i - 2];
    }
    return fib[n];
}

int main() {
    for (int i = 0; i < MAX; i++) memo[i] = -1;  // 메모이제이션 배열 초기화
    int n = 10;
    printf("%d\n", fibonacci_memo(n));  // 메모이제이션 방식
    printf("%d\n", fibonacci_tab(n));   // 타뷸레이션 방식
    return 0;
}
```
- 배낭 문제 (Knapsack Problem): 물건의 가치와 무게를 고려한 최적 선택.
```c
#include <stdio.h>

#define MAX 100
int dp[MAX][MAX];

int knapsack(int weights[], int values[], int n, int capacity) {
    for (int i = 0; i <= n; i++) {
        for (int w = 0; w <= capacity; w++) {
            if (i == 0 || w == 0)
                dp[i][w] = 0;
            else if (weights[i - 1] <= w)
                dp[i][w] = (dp[i - 1][w] > values[i - 1] + dp[i - 1][w - weights[i - 1]]) ? dp[i - 1][w] : values[i - 1] + dp[i - 1][w - weights[i - 1]];
            else
                dp[i][w] = dp[i - 1][w];
        }
    }
    return dp[n][capacity];
}

int main() {
    int weights[] = {1, 2, 3, 8, 4, 5};
    int values[] = {20, 5, 10, 40, 15, 25};
    int n = 6, capacity = 10;
    printf("%d\n", knapsack(weights, values, n, capacity));
    return 0;
}
```
- 최장 공통 부분 수열 (LCS): 두 문자열의 가장 긴 공통 부분 시퀀스 찾기.
```c
#include <stdio.h>
#include <string.h>

int lcs(char *str1, char *str2) {
    int m = strlen(str1);
    int n = strlen(str2);
    int dp[m + 1][n + 1];

    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {
            if (i == 0 || j == 0)
                dp[i][j] = 0;
            else if (str1[i - 1] == str2[j - 1])
                dp[i][j] = dp[i - 1][j - 1] + 1;
            else
                dp[i][j] = (dp[i - 1][j] > dp[i][j - 1]) ? dp[i - 1][j] : dp[i][j - 1];
        }
    }

    return dp[m][n];
}

int main() {
    char str1[] = "AGGTAB";
    char str2[] = "GXTXAYB";
    printf("%d\n", lcs(str1, str2));
    return 0;
}
```
- 최단 경로 알고리즘: 플로이드-워셜 알고리즘으로 모든 쌍 최단 거리 계산.
```c
#include <stdio.h>
#include <limits.h>

#define INF INT_MAX
#define N 5  // 정점 수

void floydWarshall(int graph[N][N]) {
    int dist[N][N];
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            dist[i][j] = graph[i][j];
        }
    }

    for (int k = 0; k < N; k++) {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (dist[i][j] > dist[i][k] + dist[k][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }

    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            if (dist[i][j] == INF)
                printf("INF ");
            else
                printf("%d ", dist[i][j]);
        }
        printf("\n");
    }
}

int main() {
    int graph[N][N] = {
        {0, 3, INF, INF, INF},
        {2, 0, INF, INF, INF},
        {INF, 7, 0, 1, INF},
        {6, INF, INF, 0, 2},
        {INF, INF, INF, 3, 0}
    };
    floydWarshall(graph);
    return 0;
}
```
---

### 그래프 알고리즘

### 탐색

- **깊이 우선 탐색 (DFS)**: 한 방향으로 깊게 탐색 후 되돌아옴. (스택 기반)
```c
#include <stdio.h>
#include <stdbool.h>

#define MAX 5

void dfs(int graph[MAX][MAX], int visited[MAX], int node) {
    visited[node] = 1;
    printf("%d ", node);

    for (int i = 0; i < MAX; i++) {
        if (graph[node][i] == 1 && !visited[i]) {
            dfs(graph, visited, i);
        }
    }
}

int main() {
    int graph[MAX][MAX] = {
        {0, 1, 1, 0, 0},
        {1, 0, 0, 1, 1},
        {1, 0, 0, 0, 0},
        {0, 1, 0, 0, 0},
        {0, 1, 0, 0, 0}
    };
    int visited[MAX] = {0};

    printf("DFS traversal: ");
    dfs(graph, visited, 0);

    return 0;
}
```
- **너비 우선 탐색 (BFS)**: 모든 인접 노드를 탐색 후 다음 단계로. (큐 기반)
```c
#include <stdio.h>
#include <stdbool.h>
#include <queue>

#define MAX 5

void bfs(int graph[MAX][MAX], int start) {
    bool visited[MAX] = {false};
    std::queue<int> q;

    visited[start] = true;
    q.push(start);

    while (!q.empty()) {
        int node = q.front();
        q.pop();
        printf("%d ", node);

        for (int i = 0; i < MAX; i++) {
            if (graph[node][i] == 1 && !visited[i]) {
                visited[i] = true;
                q.push(i);
            }
        }
    }
}

int main() {
    int graph[MAX][MAX] = {
        {0, 1, 1, 0, 0},
        {1, 0, 0, 1, 1},
        {1, 0, 0, 0, 0},
        {0, 1, 0, 0, 0},
        {0, 1, 0, 0, 0}
    };

    printf("BFS traversal: ");
    bfs(graph, 0);

    return 0;
}
```
### 최단 경로

- **다익스트라 알고리즘**: 가중치가 양수일 때 최단 경로.
```c
#include <stdio.h>
#include <limits.h>
#include <stdbool.h>

#define V 4 // 그래프의 정점 수

int minDistance(int dist[], bool sptSet[]) {
    int min = INT_MAX, min_index;

    for (int v = 0; v < V; v++) {
        if (!sptSet[v] && dist[v] <= min) {
            min = dist[v];
            min_index = v;
        }
    }

    return min_index;
}

void dijkstra(int graph[V][V], int src) {
    int dist[V];
    bool sptSet[V];

    for (int i = 0; i < V; i++) {
        dist[i] = INT_MAX;
        sptSet[i] = false;
    }

    dist[src] = 0;

    for (int count = 0; count < V - 1; count++) {
        int u = minDistance(dist, sptSet);
        sptSet[u] = true;

        for (int v = 0; v < V; v++) {
            if (!sptSet[v] && graph[u][v] && dist[u] != INT_MAX && dist[u] + graph[u][v] < dist[v]) {
                dist[v] = dist[u] + graph[u][v];
            }
        }
    }

    printf("Vertex Distance from Source %d\n", src);
    for (int i = 0; i < V; i++) {
        printf("%d \t\t %d\n", i, dist[i]);
    }
}

int main() {
    int graph[V][V] = {
        {0, 10, 0, 0},
        {10, 0, 20, 50},
        {0, 20, 0, 10},
        {0, 50, 10, 0}
    };

    dijkstra(graph, 0);

    return 0;
}
```
- **벨만-포드 알고리즘**: 가중치가 음수일 수도 있는 경우 사용 가능.
```c
#include <stdio.h>
#include <limits.h>

#define V 5
#define E 8

struct Edge {
    int src, dest, weight;
};

void bellman_ford(struct Edge edges[], int V, int E, int start) {
    int dist[V];
    for (int i = 0; i < V; i++) {
        dist[i] = INT_MAX;
    }
    dist[start] = 0;

    for (int i = 1; i <= V - 1; i++) {
        for (int j = 0; j < E; j++) {
            int u = edges[j].src;
            int v = edges[j].dest;
            int weight = edges[j].weight;
            if (dist[u] != INT_MAX && dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
            }
        }
    }

    for (int i = 0; i < E; i++) {
        int u = edges[i].src;
        int v = edges[i].dest;
        int weight = edges[i].weight;
        if (dist[u] != INT_MAX && dist[u] + weight < dist[v]) {
            printf("Graph contains negative weight cycle\n");
            return;
        }
    }

    printf("Vertex   Distance from Source\n");
    for (int i = 0; i < V; i++) {
        printf("%d \t\t %d\n", i, dist[i]);
    }
}

int main() {
    struct Edge edges[] = {
        {0, 1, -1},
        {0, 2, 4},
        {1, 2, 3},
        {1, 3, 2},
        {1, 4, 2},
        {3, 2, 5},
        {3, 1, 1},
        {4, 3, -3}
    };
    bellman_ford(edges, V, E, 0);
    return 0;
}
```
- **플로이드-워셜 알고리즘**: 모든 쌍 간 최단 거리 계산.
```c
#include <stdio.h>
#include <limits.h>

#define V 4

void floyd_warshall(int graph[V][V]) {
    int dist[V][V];

    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            dist[i][j] = graph[i][j];
        }
    }

    for (int k = 0; k < V; k++) {
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                if (dist[i][j] > dist[i][k] + dist[k][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }

    printf("Shortest distances between every pair of vertices:\n");
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            if (dist[i][j] == INT_MAX) {
                printf("INF ");
            } else {
                printf("%d ", dist[i][j]);
            }
        }
        printf("\n");
    }
}

int main() {
    int graph[V][V] = {
        {0, 5, INT_MAX, 10},
        {INT_MAX, 0, 3, INT_MAX},
        {INT_MAX, INT_MAX, 0, 1},
        {INT_MAX, INT_MAX, INT_MAX, 0}
    };

    floyd_warshall(graph);
    return 0;
}
```
### 최소 신장 트리

- **크루스칼 알고리즘**: 간선 기반.
```c
#include <stdio.h>
#include <stdlib.h>

#define V 4

struct Edge {
    int src, dest, weight;
};

int find(int parent[], int i) {
    if (parent[i] == i) {
        return i;
    }
    return find(parent, parent[i]);
}

void unionSets(int parent[], int rank[], int x, int y) {
    int rootX = find(parent, x);
    int rootY = find(parent, y);
    if (rank[rootX] > rank[rootY]) {
        parent[rootY] = rootX;
    } else {
        parent[rootX] = rootY;
        if (rank[rootX] == rank[rootY]) {
            rank[rootY]++;
        }
    }
}

int compareEdges(const void *a, const void *b) {
    return ((struct Edge *)a)->weight - ((struct Edge *)b)->weight;
}

void kruskal(struct Edge edges[], int E) {
    struct Edge result[V];
    int parent[V], rank[V];
    for (int i = 0; i < V; i++) {
        parent[i] = i;
        rank[i] = 0;
    }

    qsort(edges, E, sizeof(struct Edge), compareEdges);

    int e = 0;
    int i = 0;
    while (e < V - 1) {
        struct Edge next_edge = edges[i++];
        int x = find(parent, next_edge.src);
        int y = find(parent, next_edge.dest);

        if (x != y) {
            result[e++] = next_edge;
            unionSets(parent, rank, x, y);
        }
    }

    printf("Edges in MST\n");
    for (int i = 0; i < e; i++) {
        printf("%d - %d: %d\n", result[i].src, result[i].dest, result[i].weight);
    }
}

int main() {
    struct Edge edges[] = {
        {0, 1, 10}, {0, 2, 6}, {0, 3, 5},
        {1, 3, 15}, {2, 3, 4}
    };
    kruskal(edges, 5);
    return 0;
}
```
- **프림 알고리즘**: 정점 기반.
```c
#include <stdio.h>
#include <limits.h>

#define V 4

int minKey(int key[], bool mstSet[]) {
    int min = INT_MAX, minIndex;
    for (int v = 0; v < V; v++) {
        if (mstSet[v] == false && key[v] < min) {
            min = key[v], minIndex = v;
        }
    }
    return minIndex;
}

void prim(int graph[V][V]) {
    int parent[V];
    int key[V];
    bool mstSet[V];

    for (int i = 0; i < V; i++) {
        key[i] = INT_MAX;
        mstSet[i] = false;
    }

    key[0] = 0;
    parent[0] = -1;

    for (int count = 0; count < V - 1; count++) {
        int u = minKey(key, mstSet);
        mstSet[u] = true;

        for (int v = 0; v < V; v++) {
            if (graph[u][v] && mstSet[v] == false && graph[u][v] < key[v]) {
                parent[v] = u;
                key[v] = graph[u][v];
            }
        }
    }

    printf("Edge \tWeight\n");
    for (int i = 1; i < V; i++) {
        printf("%d - %d \t%d \n", parent[i], i, graph[i][parent[i]]);
    }
}

int main() {
    int graph[V][V] = {
        {0, 1, 2, 3},
        {1, 0, 3, 2},
        {2, 3, 0, 1},
        {3, 2, 1, 0}
    };
    prim(graph);
    return 0;
}
```
### 위상 정렬 (Topological Sorting)

- 방향성이 있는 비순환 그래프(DAG)의 정렬.
```c
#include <stdio.h>
#include <stdlib.h>

#define V 4

void topologicalSortUtil(int graph[V][V], int v, int visited[], int stack[]) {
    visited[v] = 1;

    for (int i = 0; i < V; i++) {
        if (graph[v][i] && !visited[i]) {
            topologicalSortUtil(graph, i, visited, stack);
        }
    }

    stack[--V] = v;
}

void topologicalSort(int graph[V][V]) {
    int visited[V] = {0};
    int stack[V];

    for (int i = 0; i < V; i++) {
        if (!visited[i]) {
            topologicalSortUtil(graph, i, visited, stack);
        }
    }

    printf("Topological Sort: ");
    for (int i = 0; i < V; i++) {
        printf("%d ", stack[i]);
    }
}

int main() {
    int graph[V][V] = {
        {0, 1, 1, 0},
        {0, 0, 0, 1},
        {0, 0, 0, 1},
        {0, 0, 0, 0}
    };
    topologicalSort(graph);
    return 0;
}
```
### 네트워크 플로우

- **에드몬드-카프 알고리즘**: 최대 유량 계산.
```c
#include <stdio.h>
#include <limits.h>
#include <stdbool.h>

#define V 6

bool bfs(int capacity[V][V], int flow[V][V], int source, int sink, int parent[]) {
    bool visited[V] = {false};
    int queue[V], front = 0, rear = 0;
    visited[source] = true;
    queue[rear++] = source;

    while (front != rear) {
        int u = queue[front++];
        for (int v = 0; v < V; v++) {
            if (!visited[v] && capacity[u][v] - flow[u][v] > 0) {
                visited[v] = true;
                parent[v] = u;
                if (v == sink) return true;
                queue[rear++] = v;
            }
        }
    }
    return false;
}

int edmondsKarp(int capacity[V][V], int source, int sink) {
    int flow[V][V] = {0};
    int parent[V];
    int max_flow = 0;

    while (bfs(capacity, flow, source, sink, parent)) {
        int path_flow = INT_MAX;
        for (int v = sink; v != source; v = parent[v]) {
            path_flow = (path_flow < capacity[parent[v]][v] - flow[parent[v]][v]) ?
                        path_flow : capacity[parent[v]][v] - flow[parent[v]][v];
        }
        max_flow += path_flow;

        for (int v = sink; v != source; v = parent[v]) {
            flow[parent[v]][v] += path_flow;
            flow[v][parent[v]] -= path_flow;
        }
    }
    return max_flow;
}

int main() {
    int capacity[V][V] = {
        {0, 16, 13, 0, 0, 0},
        {0, 0, 10, 12, 0, 0},
        {0, 4, 0, 0, 14, 0},
        {0, 0, 9, 0, 0, 20},
        {0, 0, 0, 7, 0, 4},
        {0, 0, 0, 0, 0, 0}
    };
    printf("Max flow: %d\n", edmondsKarp(capacity, 0, 5));
    return 0;
}
```
- **푸시-재명칭 알고리즘**: 유량 문제 해결.
```c
#include <stdio.h>
#include <limits.h>

#define V 6

// 푸시 연산
void push(int u, int v, int capacity[V][V], int flow[V][V], int excess[V]) {
    int delta = (excess[u] < capacity[u][v] - flow[u][v]) ? excess[u] : capacity[u][v] - flow[u][v];
    flow[u][v] += delta;
    flow[v][u] -= delta;
    excess[u] -= delta;
    excess[v] += delta;
}

// 재명칭 연산
void relabel(int u, int V, int capacity[V][V], int flow[V][V], int height[V]) {
    int min_height = INT_MAX;
    for (int v = 0; v < V; v++) {
        if (capacity[u][v] - flow[u][v] > 0) {
            min_height = (height[v] < min_height) ? height[v] : min_height;
        }
    }
    height[u] = min_height + 1;
}

// 디스차지 연산
void discharge(int u, int V, int capacity[V][V], int flow[V][V], int excess[V], int height[V]) {
    while (excess[u] > 0) {
        for (int v = 0; v < V; v++) {
            if (capacity[u][v] - flow[u][v] > 0 && height[u] == height[v] + 1) {
                push(u, v, capacity, flow, excess);
                if (excess[u] == 0) break;
            }
        }
        if (excess[u] > 0) {
            relabel(u, V, capacity, flow, height);
        }
    }
}

// 최대 유량 계산
int max_flow(int source, int sink, int V, int capacity[V][V]) {
    int flow[V][V] = {0};  // 흐름 배열
    int excess[V] = {0};    // 초과 유량 배열
    int height[V] = {0};    // 높이 배열

    height[source] = V;     // 출발점 높이는 V로 설정
    excess[source] = INT_MAX;

    // 출발점에서 연결된 간선으로 푸시
    for (int v = 0; v < V; v++) {
        push(source, v, capacity, flow, excess);
    }

    // 나머지 노드들에 대해 디스차지 연산 수행
    for (int u = 0; u < V; u++) {
        if (u != source && u != sink) {
            discharge(u, V, capacity, flow, excess, height);
        }
    }

    return excess[sink];
}

int main() {
    int capacity[V][V] = {
        {0, 16, 13, 0, 0, 0},
        {0, 0, 10, 12, 0, 0},
        {0, 4, 0, 0, 14, 0},
        {0, 0, 9, 0, 0, 20},
        {0, 0, 0, 7, 0, 4},
        {0, 0, 0, 0, 0, 0}
    };

    printf("Maximum Flow: %d\n", max_flow(0, 5, V, capacity));
    return 0;
}
```
---

### 문자열 알고리즘

### 문자열 검색

- **KMP 알고리즘**: 접두사와 접미사를 이용한 효율적 검색.
```c
#include <stdio.h>
#include <string.h>

void compute_lps(char *pattern, int m, int *lps) {
    int length = 0;
    int i = 1;
    while (i < m) {
        if (pattern[i] == pattern[length]) {
            length++;
            lps[i] = length;
            i++;
        } else {
            if (length != 0) {
                length = lps[length-1];
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }
}

void kmp_search(char *text, char *pattern) {
    int n = strlen(text);
    int m = strlen(pattern);
    int lps[m];
    compute_lps(pattern, m, lps);

    int i = 0, j = 0;
    while (i < n) {
        if (pattern[j] == text[i]) {
            i++;
            j++;
        }
        if (j == m) {
            printf("Pattern found at index %d\n", i - j);
            j = lps[j-1];
        } else if (i < n && pattern[j] != text[i]) {
            if (j != 0) {
                j = lps[j-1];
            } else {
                i++;
            }
        }
    }
}

int main() {
    char text[] = "ABABDABACDABABCABAB";
    char pattern[] = "ABABCABAB";
    kmp_search(text, pattern);
    return 0;
}
```
- **라빈-카프 알고리즘**: 해시를 사용한 문자열 검색.
```c#include <stdio.h>
#include <string.h>

#define D 256
#define Q 101

void rabin_karp_search(char *text, char *pattern) {
    int m = strlen(pattern);
    int n = strlen(text);
    int p_hash = 0, t_hash = 0, h = 1;

    // h = (d^(m-1)) % q
    for (int i = 0; i < m - 1; i++) {
        h = (h * D) % Q;
    }

    // 패턴과 텍스트의 첫 번째 윈도우 해시 계산
    for (int i = 0; i < m; i++) {
        p_hash = (D * p_hash + pattern[i]) % Q;
        t_hash = (D * t_hash + text[i]) % Q;
    }

    // 문자열 검색
    for (int i = 0; i <= n - m; i++) {
        if (p_hash == t_hash) {
            if (strncmp(text + i, pattern, m) == 0) {
                printf("Pattern found at index %d\n", i);
            }
        }
        if (i < n - m) {
            t_hash = (D * (t_hash - text[i] * h) + text[i + m]) % Q;
            if (t_hash < 0) t_hash += Q;
        }
    }
}

int main() {
    char text[] = "ABABDABACDABABCABAB";
    char pattern[] = "ABABCABAB";
    rabin_karp_search(text, pattern);
    return 0;
}
```
### 접미사 배열 및 트라이

- 접미사 배열: 문자열의 모든 접미사의 정렬된 배열.
- 접미사 트리: 문자열의 모든 접미사를 포함하는 트리.
```c
#include <stdio.h>
#include <string.h>

void suffix_array(char *s) {
    int n = strlen(s);
    int suffixes[n];
    for (int i = 0; i < n; i++) suffixes[i] = i;

    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if (strcmp(s + suffixes[i], s + suffixes[j]) > 0) {
                int temp = suffixes[i];
                suffixes[i] = suffixes[j];
                suffixes[j] = temp;
            }
        }
    }

    for (int i = 0; i < n; i++) {
        printf("%d ", suffixes[i]);
    }
    printf("\n");
}

int main() {
    char s[] = "banana";
    suffix_array(s);
    return 0;
}
```
### 롤링 해시 및 Z-알고리즘

- 문자열 비교에 효율적인 방법 제공.
```c
#include <stdio.h>
#include <string.h>

#define D 256
#define Q 101

void rolling_hash(char *text, char *pattern) {
    int m = strlen(pattern);
    int n = strlen(text);
    int p_hash = 0, t_hash = 0, h = 1;

    // h = (d^(m-1)) % q
    for (int i = 0; i < m - 1; i++) {
        h = (h * D) % Q;
    }

    // 패턴과 텍스트의 첫 번째 윈도우 해시 계산
    for (int i = 0; i < m; i++) {
        p_hash = (D * p_hash + pattern[i]) % Q;
        t_hash = (D * t_hash + text[i]) % Q;
    }

    // 문자열 검색
    for (int i = 0; i <= n - m; i++) {
        if (p_hash == t_hash) {
            if (strncmp(text + i, pattern, m) == 0) {
                printf("Pattern found at index %d\n", i);
            }
        }
        if (i < n - m) {
            t_hash = (D * (t_hash - text[i] * h) + text[i + m]) % Q;
            if (t_hash < 0) t_hash += Q;
        }
    }
}

int main() {
    char text[] = "ABABDABACDABABCABAB";
    char pattern[] = "ABABCABAB";
    rolling_hash(text, pattern);
    return 0;
}
```
---

### 수학 및 수치 알고리즘

- **유클리드 호제법**: 최대 공약수 계산.
```c
#include <stdio.h>
#include <math.h>

int is_prime(int n) {
    if (n <= 1) return 0;
    for (int i = 2; i <= sqrt(n); i++) {
        if (n % i == 0) return 0;
    }
    return 1;
}

int main() {
    printf("%d\n", is_prime(29));  // Output: 1 (True)
    printf("%d\n", is_prime(15));  // Output: 0 (False)
    return 0;
}
```
- **소수 판별**: 소수인지 확인.
- **에라토스테네스의 체**: 범위 내 모든 소수 찾기.
```c
#include <stdio.h>
#include <stdbool.h>

void sieve_of_eratosthenes(int limit) {
    bool sieve[limit + 1];
    for (int i = 0; i <= limit; i++) sieve[i] = true;
    sieve[0] = sieve[1] = false;

    for (int i = 2; i * i <= limit; i++) {
        if (sieve[i]) {
            for (int j = i * i; j <= limit; j += i) {
                sieve[j] = false;
            }
        }
    }

    for (int i = 2; i <= limit; i++) {
        if (sieve[i]) {
            printf("%d ", i);
        }
    }
    printf("\n");
}

int main() {
    sieve_of_eratosthenes(30);  // Output: 2 3 5 7 11 13 17 19 23 29
    return 0;
}
```
- **빠른 거듭제곱**: O(log n)으로 계산.
```c
#include <stdio.h>

long long fast_exponentiation(long long base, long long exp, long long mod) {
    long long result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

int main() {
    printf("%lld\n", fast_exponentiation(2, 10, 1000));  // Output: 1024
    return 0;
}
```
- **행렬 연산**: 행렬 곱셈, 역행렬 계산 등.
```c
#include <stdio.h>

void multiply_matrices(int rows_A, int cols_A, int cols_B, int A[rows_A][cols_A], int B[cols_A][cols_B], int result[rows_A][cols_B]) {
    for (int i = 0; i < rows_A; i++) {
        for (int j = 0; j < cols_B; j++) {
            result[i][j] = 0;
            for (int k = 0; k < cols_A; k++) {
                result[i][j] += A[i][k] * B[k][j];
            }
        }
    }
}

int main() {
    int A[2][2] = {{1, 2}, {3, 4}};
    int B[2][2] = {{5, 6}, {7, 8}};
    int result[2][2];

    multiply_matrices(2, 2, 2, A, B, result);

    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 2; j++) {
            printf("%d ", result[i][j]);
        }
        printf("\n");
    }
    // Output: 19 22
    //         43 50
    return 0;
}
```
- **모듈러 연산 및 중국인의 나머지 정리 (CRT)**: 동시 합동식 풀이.
```c
#include <stdio.h>

int mod_inverse(int a, int m) {
    a = a % m;
    for (int x = 1; x < m; x++) {
        if ((a * x) % m == 1) return x;
    }
    return -1;
}

int crt(int n[], int a[], int k) {
    int prod = 1, result = 0;
    for (int i = 0; i < k; i++) prod *= n[i];

    for (int i = 0; i < k; i++) {
        int pp = prod / n[i];
        result += a[i] * mod_inverse(pp, n[i]) * pp;
    }

    return result % prod;
}

int main() {
    int n[] = {3, 5, 7};
    int a[] = {2, 3, 2};
    printf("%d\n", crt(n, a, 3));  // Output: 23
    return 0;
}
```
---

### 조합 및 확률

- **순열 및 조합**: 모든 경우의 수 계산.
```c
#include <stdio.h>

// Factorial function for permutation
int factorial(int n) {
    return (n <= 1) ? 1 : n * factorial(n - 1);
}

// Combination (nCr)
int combination(int n, int r) {
    return factorial(n) / (factorial(r) * factorial(n - r));
}

int main() {
    int n = 3, r = 2;

    // Permutation (nPr)
    printf("Permutation (nPr) of %dP%d: %d\n", n, r, factorial(n) / factorial(n - r));
    // Combination (nCr)
    printf("Combination (nCr) of %dC%d: %d\n", n, r, combination(n, r));

    return 0;
}
```
- **비트마스크**: 부분집합 생성.
```c
#include <stdio.h>

void generate_subsets(int data[], int n) {
    for (int i = 0; i < (1 << n); i++) {
        printf("{ ");
        for (int j = 0; j < n; j++) {
            if (i & (1 << j)) {
                printf("%d ", data[j]);
            }
        }
        printf("}\n");
    }
}

int main() {
    int data[] = {1, 2, 3};
    int n = sizeof(data) / sizeof(data[0]);

    printf("Subsets:\n");
    generate_subsets(data, n);
    return 0;
}
```
- **조합 최적화 문제**: 최적의 경우 탐색.
```c
#include <stdio.h>
#include <string.h>

int knapsack(int W, int weights[], int values[], int n) {
    int dp[n + 1][W + 1];
    memset(dp, 0, sizeof(dp));

    for (int i = 1; i <= n; i++) {
        for (int w = 0; w <= W; w++) {
            if (weights[i - 1] <= w) {
                dp[i][w] = (dp[i - 1][w] > dp[i - 1][w - weights[i - 1]] + values[i - 1]) ? dp[i - 1][w] : dp[i - 1][w - weights[i - 1]] + values[i - 1];
            } else {
                dp[i][w] = dp[i - 1][w];
            }
        }
    }
    return dp[n][W];
}

int main() {
    int weights[] = {1, 2, 3};
    int values[] = {10, 15, 40};
    int W = 5;
    int n = sizeof(weights) / sizeof(weights[0]);

    printf("Maximum Value: %d\n", knapsack(W, weights, values, n));
    return 0;
}
```
---

### 기타 알고리즘

- **슬라이딩 윈도우**: 고정 크기 창으로 문제 해결.
```c
#include <stdio.h>
#include <limits.h>

int max_sum_subarray(int arr[], int n, int k) {
    int max_sum = INT_MIN, window_sum = 0;

    for (int i = 0; i < n; i++) {
        window_sum += arr[i];
        if (i >= k - 1) {
            if (window_sum > max_sum) {
                max_sum = window_sum;
            }
            window_sum -= arr[i - (k - 1)];
        }
    }
    return max_sum;
}

int main() {
    int arr[] = {1, 3, 2, 5, 1, 1, 7, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;
    printf("%d\n", max_sum_subarray(arr, n, k));  // Output: 11
    return 0;
}
```
- **유니온-파인드**: 집합 간 연결 확인.
```c
#include <stdio.h>

#define MAX 100

int parent[MAX], rank[MAX];

void makeSet(int n) {
    for (int i = 0; i < n; i++) {
        parent[i] = i;
        rank[i] = 0;
    }
}

int find(int x) {
    if (parent[x] != x)
        parent[x] = find(parent[x]);  // Path compression
    return parent[x];
}

void unionSets(int x, int y) {
    int rootX = find(x);
    int rootY = find(y);
    if (rootX != rootY) {
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
    int n = 5;
    makeSet(n);
    unionSets(0, 1);
    unionSets(1, 2);
    printf("%d\n", find(2));  // Output: 0
    return 0;
}
```
- **두 포인터 기법**: 배열의 두 위치를 동시에 탐색.
```c
#include <stdio.h>

void twoPointerSum(int arr[], int n, int target) {
    int left = 0, right = n - 1;
    while (left < right) {
        int sum = arr[left] + arr[right];
        if (sum == target) {
            printf("Indices: %d, %d\n", left, right);
            return;
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }
    printf("No such pair found.\n");
}

int main() {
    int arr[] = {1, 2, 3, 4, 6};
    int n = sizeof(arr) / sizeof(arr[0]);
    int target = 6;
    twoPointerSum(arr, n, target);
    return 0;
}
```
- **스위핑 기법**: 정렬 후 선형 탐색.
```c
#include <stdio.h>

typedef struct {
    int x, y;
} Point;

int orientation(Point p, Point q, Point r) {
    int val = (q.y - p.y) * (r.x - q.x) - (q.x - p.x) * (r.y - q.y);
    if (val == 0) return 0;
    return (val > 0) ? 1 : 2;
}

int onSegment(Point p, Point q, Point r) {
    return (q.x <= (p.x > r.x ? p.x : r.x) && q.x >= (p.x < r.x ? p.x : r.x) &&
            q.y <= (p.y > r.y ? p.y : r.y) && q.y >= (p.y < r.y ? p.y : r.y));
}

int doSegmentsIntersect(Point p1, Point q1, Point p2, Point q2) {
    int o1 = orientation(p1, q1, p2);
    int o2 = orientation(p1, q1, q2);
    int o3 = orientation(p2, q2, p1);
    int o4 = orientation(p2, q2, q1);

    if (o1 != o2 && o3 != o4) return 1;

    if (o1 == 0 && onSegment(p1, p2, q1)) return 1;
    if (o2 == 0 && onSegment(p1, q2, q1)) return 1;
    if (o3 == 0 && onSegment(p2, p1, q2)) return 1;
    if (o4 == 0 && onSegment(p2, q1, q2)) return 1;

    return 0;
}

int main() {
    Point p1 = {1, 1}, q1 = {10, 1};
    Point p2 = {1, 2}, q2 = {10, 2};
    printf("%d\n", doSegmentsIntersect(p1, q1, p2, q2));  // Output: 0 (False)
    return 0;
}
```
- **랜덤화 알고리즘**: 무작위성을 활용한 알고리즘.
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void shuffleArray(int arr[], int n) {
    srand(time(NULL));
    for (int i = n - 1; i > 0; i--) {
        int j = rand() % (i + 1);
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    shuffleArray(arr, n);

    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```
---

### 알고리즘 분석

- **시간 복잡도**: 알고리즘이 실행되는 데 걸리는 시간을 입력 크기에 따라 수학적으로 표현한 것입니다.
주로 Big-O 표기법을 사용하여 최악의 경우 시간 증가율을 나타냅니다. O(1), O(log N), O(N), O(N log N), O(N^2) 등이 있습니다.
예시: 선형 탐색의 시간 복잡도는 O(N), 병합 정렬은 O(N log N)입니다.
- **공간 복잡도 (Space Complexity)**:
공간 복잡도는 알고리즘이 사용하는 메모리 양을 입력 크기에 따라 수학적으로 표현한 것입니다.
고정 크기의 메모리, 입력 크기에 따라 동적으로 증가하는 메모리 사용량 등을 고려합니다.
예시: 퀵 정렬의 공간 복잡도는 O(log N) (재귀 깊이), 병합 정렬은 O(N) (추가 배열 필요).
- ***최선, 평균, 최악의 경우 분석**

- 최선의 경우: 알고리즘이 가장 빠르게 동작하는 입력에서의 성능.
예: 버블 정렬에서 이미 정렬된 배열일 때 O(N).
- 평균의 경우: 모든 가능한 입력에서 평균적인 성능.
예: 퀵 정렬의 평균 시간 복잡도는 O(N log N).
- 최악의 경우: 가장 시간이 오래 걸리는 입력에서의 성능.
예: 퀵 정렬의 최악 시간 복잡도는 O(N^2) (피벗 선택이 비효율적일 때).