# 컴퓨터구조(Computer Architecture)
### 컴퓨터 구조란 무엇인가?

컴퓨터 구조는 컴퓨터 시스템의 설계와 운영 원리를 다루는 학문입니다. 하드웨어와 소프트웨어 간의 상호작용을 최적화하는 방법을 연구하며, 컴퓨터 시스템의 구성 요소, 동작 방식, 데이터 처리 메커니즘의 이해와 설계에 중점을 둡니다.

### 컴퓨터 시스템의 발전과 역사

컴퓨터는 초기 기계식 계산기에서 시작하여 진공관, 트랜지스터, 집적 회로를 거쳐 현대의 초고속 프로세서와 병렬 처리 시스템으로 발전했습니다. 주요 발전 단계는 다음과 같습니다:

1. 1세대: 진공관 기반
2. 2세대: 트랜지스터 기반
3. 3세대: 집적 회로 기반
4. 4세대: 마이크로프로세서 기반
5. 현대: 인공지능 및 고성능 병렬 처리 시스템

### 컴퓨터의 구성 요소 (Components of a Computer System)

1. **중앙처리장치(CPU):** 데이터 처리와 명령어 실행을 담당하는 컴퓨터의 핵심 구성 요소
2. **메모리:** 프로그램과 데이터를 저장하는 장치로, RAM과 ROM 등이 포함됨
3. **입출력 장치(I/O Devices):** 키보드, 모니터, 프린터 등 사용자와 컴퓨터 간의 상호작용을 담당하는 장치

### 컴퓨터 설계의 기본 원리 (Fundamental Principles of Computer Design)

1. **무어의 법칙:** 반도체 칩의 트랜지스터 수가 18개월마다 2배로 증가
2. **병렬 처리:** 여러 프로세서를 동시에 사용하여 성능을 향상
3. **캐시 활용:** CPU와 메모리 간 속도 차이를 줄이기 위해 고속 메모리 사용

## 데이터 표현 및 연산 (Data Representation and Operations)

### 수의 체계 (Number Systems)

1. **이진수(Binary):** 0과 1로 표현되는 2진법 수 체계
2. **8진수(Octal):** 0부터 7까지의 숫자로 표현되는 8진법 수 체계
3. **16진수(Hexadecimal):** 0부터 9와 A부터 F까지의 문자로 표현되는 16진법 수 체계
```c
#include <stdio.h>

int main() {
    int decimal = 255;
    printf("Decimal: %d\n", decimal);
    printf("Binary: %b\n", decimal); // C는 직접적인 %b를 지원하지 않지만, 아래처럼 함수로 구현 가능
    printf("Octal: %o\n", decimal);
    printf("Hexadecimal: %x\n", decimal);
    return 0;
}
```

### 체계 간 변환

- 이진수와 8진수 간 변환: 3자리 이진수는 1자리 8진수와 대응
- 이진수와 16진수 간 변환: 4자리 이진수는 1자리 16진수와 대응

### 정수와 실수 표현 (Integer and Floating-Point Representation)

1. **고정소수점:** 소수점 위치가 고정된 수 표현 방식
2. **부동소수점:** 소수점 위치가 유동적인 수 표현 방식으로, 실수를 효율적으로 표현
3. **IEEE 754 표준:** 부동소수점 수의 표현, 정밀도, 반올림 규칙을 정의

```c
#include <stdio.h>
#include <float.h>

int main() {
    float f = 3.14;
    printf("Float: %.2f\n", f);
    printf("Precision: %d digits\n", FLT_DIG);
    return 0;
}
```

### 데이터 연산 (Data Operations)

1. **산술 연산:** 덧셈, 뺄셈, 곱셈, 나눗셈
```c
#include <stdio.h>

int main() {
    int a = 10, b = 5;
    printf("Addition: %d\n", a + b);
    printf("Subtraction: %d\n", a - b);
    printf("Multiplication: %d\n", a * b);
    printf("Division: %d\n", a / b);
    return 0;
}
```
2. **논리 연산:** AND, OR, NOT, XOR
```c
#include <stdio.h>

int main() {
    int a = 1, b = 0;
    printf("AND: %d\n", a && b);
    printf("OR: %d\n", a || b);
    printf("NOT: %d\n", !a);
    return 0;
}
```
3. **시프트 연산:** 데이터 비트를 좌우로 이동
```c
#include <stdio.h>

int main() {
    int num = 8; // Binary: 1000
    printf("Left Shift: %d\n", num << 1); // 10000 -> 16
    printf("Right Shift: %d\n", num >> 1); // 0100 -> 4
    return 0;
}
```
## 중앙처리장치 (CPU, Central Processing Unit)

### CPU의 구조와 구성 요소 (CPU Architecture and Components)

1. **산술 논리 장치(ALU):** 산술 및 논리 연산을 수행
2. **레지스터(Registers):** 데이터 및 명령어를 일시적으로 저장
3. **제어 유닛(Control Unit):** 명령어를 해독하고 실행을 제어

### 명령어 사이클 (Instruction Cycle)

1. **명령어 인출(Fetch):** 메모리에서 명령어를 가져옴
2. **명령어 해독(Decode):** 명령어를 해석
3. **명령어 실행(Execute):** 명령어를 수행
```c
#include <stdio.h>

void fetch() { printf("Fetching instruction...\n"); }
void decode() { printf("Decoding instruction...\n"); }
void execute() { printf("Executing instruction...\n"); }

int main() {
    fetch();
    decode();
    execute();
    return 0;
}
```
### 명령어 집합 구조(ISA, Instruction Set Architecture)

1. **CISC:** 복잡한 명령어 집합을 사용하여 고급 기능을 제공
2. **RISC:** 단순한 명령어 집합을 사용하여 빠른 실행을 목표

## 메모리 구조 (Memory Architecture)

### 메모리 계층 구조 (Memory Hierarchy)

- 고속 메모리에서 저속 메모리로: 레지스터, 캐시, 메인 메모리, 보조 저장장치

### 캐시 메모리 (Cache Memory)

1. **매핑 방식:**
    - 직접 매핑
    - 집합 연관
    - 완전 연관
2. **캐시 적중률:** CPU가 필요한 데이터를 캐시에서 찾는 비율
```c
#include <stdio.h>

#define CACHE_SIZE 4

int main() {
    int cache[CACHE_SIZE] = {-1, -1, -1, -1};
    int data[] = {3, 7, 3, 9, 2, 7};
    int n = sizeof(data) / sizeof(data[0]);

    for (int i = 0; i < n; i++) {
        int index = data[i] % CACHE_SIZE;
        cache[index] = data[i];
        printf("Accessing %d -> Cache: ", data[i]);
        for (int j = 0; j < CACHE_SIZE; j++) {
            printf("%d ", cache[j]);
        }
        printf("\n");
    }
    return 0;
}
```
### 가상 메모리 (Virtual Memory)

1. **페이징:** 메모리를 일정 크기의 페이지로 나눔
2. **세그멘테이션:** 논리적인 단위로 메모리를 분할
3. **페이지 교체 알고리즘:**
    - LRU: 가장 오랫동안 사용되지 않은 페이지 교체
    - FIFO: 가장 먼저 들어온 페이지 교체
    - 최적 교체: 앞으로 가장 적게 사용할 페이지 교체
```c
#include <stdio.h>

#define PAGE_COUNT 3

int main() {
    int pages[] = {1, 3, 0, 3, 5, 6};
    int n = sizeof(pages) / sizeof(pages[0]);
    int memory[PAGE_COUNT] = {-1, -1, -1};
    int front = 0;

    for (int i = 0; i < n; i++) {
        int found = 0;
        for (int j = 0; j < PAGE_COUNT; j++) {
            if (memory[j] == pages[i]) {
                found = 1;
                break;
            }
        }

        if (!found) {
            memory[front] = pages[i];
            front = (front + 1) % PAGE_COUNT;
        }

        printf("Accessing %d -> Memory: ", pages[i]);
        for (int j = 0; j < PAGE_COUNT; j++) {
            printf("%d ", memory[j]);
        }
        printf("\n");
    }
    return 0;
}
```
## 입출력 시스템 (I/O Systems)

### 입출력 장치와 동작 원리 (I/O Devices and Operations)

입출력 장치는 데이터를 입력받고 출력하는 역할을 수행하며, 각 장치는 고유한 동작 방식을 가집니다.

### 입출력 제어 방식 (I/O Control Mechanisms)

1. **프로그램 제어:** CPU가 I/O 작업을 직접 제어
2. **인터럽트 방식:** I/O 완료 시 CPU에 알림
3. **DMA:** CPU의 개입 없이 메모리와 I/O 장치 간 데이터 전송
```c
#include <stdio.h>

void dma_transfer(int *source, int *destination, int size) {
    for (int i = 0; i < size; i++) {
        destination[i] = source[i];
    }
}

int main() {
    int source[] = {1, 2, 3, 4, 5};
    int destination[5];

    dma_transfer(source, destination, 5);

    printf("Data transferred to destination: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", destination[i]);
    }
    return 0;
}
```
### 인터럽트 (Interrupts)

- 특정 이벤트 발생 시 CPU의 현재 작업을 중단하고 처리

### I/O 버스와 데이터 전송 (I/O Bus and Data Transfer)

- I/O 장치 간 데이터 이동을 위한 통신 경로

## 프로세서 설계 (Processor Design)

### 데이터 경로 설계 (Datapath Design)

1. **단일 사이클:** 모든 명령어가 한 클럭 주기 내에 실행
2. **멀티 사이클:** 명령어를 여러 클럭 주기로 나누어 실행

### 제어 유닛 설계 (Control Unit Design)

1. **하드와이어드 제어:** 논리 회로로 구현
2. **마이크로프로그램 제어:** 마이크로코드로 구현

### 파이프라인 처리 (Pipelining)

1. **개념:** 명령어 실행 단계를 분리하여 병렬 처리
2. **위험 요소:**
    - 데이터 위험: 명령어 간 데이터 의존성 문제
    - 제어 위험: 분기 예측 실패로 인한 문제
    - 구조적 위험: 자원 충돌로 인한 문제

## 성능 평가와 최적화 (Performance Evaluation and Optimization)

### 성능 측정 지표 (Performance Metrics)

1. **처리량:** 단위 시간당 처리되는 작업량
2. **응답 시간:** 작업 요청부터 완료까지 걸리는 시간
3. **클럭 주기:** CPU가 한 명령어를 실행하는 데 필요한 시간

### Amdahl의 법칙 (Amdahl's Law)

- 시스템 성능 개선이 병렬 처리에서의 제한 요소에 의해 결정

### 시스템 성능 최적화 (System Performance Optimization)

1. **캐시 최적화:** 데이터 접근 속도 향상
2. **분기 예측:** 분기 명령어 실행 속도 향상