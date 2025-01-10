# 운영체제(Operating System)

### **운영체제 개요**

### **운영체제의 역할과 목적**

운영체제(OS, Operating System)는 컴퓨터 하드웨어와 소프트웨어 간의 중재자로서, 시스템 리소스를 효율적으로 관리하고 사용자 및 응용 프로그램에 편리한 환경을 제공합니다. 주요 역할은 다음과 같습니다:

1. **자원 관리(Resource Management)**: CPU, 메모리, 디스크, I/O 장치 등 시스템 리소스를 관리하고 최적화합니다.
2. **사용자 인터페이스 제공(User Interface)**: 사용자와 시스템 간 상호작용을 위한 인터페이스(명령줄 인터페이스 또는 GUI)를 제공합니다.
3. **프로세스 관리(Process Management)**: 여러 프로그램이 동시에 실행되도록 프로세스와 스레드를 생성, 관리합니다.
4. **파일 관리(File Management)**: 파일 생성, 삭제, 읽기/쓰기, 디렉토리 관리 등을 처리합니다.
5. **보안 및 보호(Security and Protection)**: 데이터 무결성과 시스템의 접근 제어를 통해 보안을 제공합니다.
6. **에러 탐지 및 복구(Error Detection and Recovery)**: 하드웨어 및 소프트웨어 오류를 탐지하고 시스템을 안정적으로 유지합니다.

### **운영체제의 구조 (Structure of Operating Systems)**

1. **커널(Kernel)**
    - 운영체제의 핵심 구성 요소로, 하드웨어와 직접 상호작용하며 시스템 리소스를 관리합니다.
    - 커널의 주요 기능:
        - 프로세스 관리
        - 메모리 관리
        - 파일 시스템 관리
        - 디바이스 드라이버 인터페이스
        - 네트워킹 관리
2. **사용자 모드(User Mode) vs 커널 모드(Kernel Mode)**
    - **사용자 모드**: 응용 프로그램이 실행되는 모드로, 하드웨어에 직접 접근할 수 없습니다. 시스템 호출(System Call)을 통해 커널 기능을 요청합니다.
    - **커널 모드**: 운영체제가 실행되는 모드로, 하드웨어와 직접 통신하며 모든 시스템 리소스에 완전한 접근 권한을 가집니다.
    - **전환 이유**: 사용자 프로그램의 실수나 악성 코드로 인한 시스템 손상을 방지하고 안정성을 유지하기 위함입니다.

### **운영체제의 종류 (Types of Operating Systems)**

1. **단일 사용자/다중 사용자 (Single-user/Multitasking)**
    - **단일 사용자 OS**: 한 번에 한 사용자가 시스템을 사용할 수 있습니다. (예: MS-DOS)
    - **다중 사용자 OS**: 여러 사용자가 동시에 시스템을 사용할 수 있습니다. (예: UNIX, Windows Server)
2. **단일 작업/다중 작업 (Single-tasking/Multitasking)**
    - **단일 작업 OS**: 한 번에 하나의 작업만 실행합니다. (예: 초기 DOS)
    - **다중 작업 OS**: 여러 작업을 동시에 실행하며, CPU 스케줄링을 통해 작업을 전환합니다. (예: Windows, macOS)
3. **분산 OS (Distributed Operating Systems)**
    - 여러 컴퓨터가 네트워크로 연결되어 하나의 시스템처럼 동작합니다. 자원을 공유하고 작업을 분산 처리합니다. (예: Apache Hadoop)
4. **실시간 OS (Real-Time Operating Systems)**
    - 특정 작업이 정해진 시간 안에 수행되도록 보장합니다. 주로 임베디드 시스템에서 사용됩니다. (예: VxWorks, FreeRTOS)

### **프로세스 관리 (Process Management)**

### **프로세스와 스레드 (Processes and Threads)**

1. **프로세스(Process)**
    - 실행 중인 프로그램의 인스턴스를 의미합니다.
    - 주요 구성 요소:
        - **프로세스 제어 블록(PCB)**: 프로세스의 상태, ID, CPU 레지스터 정보, 메모리 할당 정보 등을 포함합니다.
        - **코드 섹션(Code Section)**: 실행할 명령어의 집합.
        - **데이터 섹션(Data Section)**: 전역 변수와 데이터.
        - **스택(Stack)**: 함수 호출과 로컬 변수 저장.
        - **힙(Heap)**: 동적 메모리 할당 공간.
2. **프로세스 상태 (Process States)**
    - **생성(New)**: 프로세스가 생성된 상태.
    - **준비(Ready)**: CPU에서 실행되기를 기다리는 상태.
    - **실행(Running)**: CPU에서 실행 중인 상태.
    - **대기(Waiting)**: I/O 작업 등으로 인해 대기하는 상태.
    - **종료(Terminated)**: 실행이 완료된 상태.
3. **스레드(Thread)**
    - 프로세스 내의 실행 단위로, 동일한 메모리 공간을 공유합니다.
    - *멀티스레딩(Multithreading)**의 장점:
        - 병렬 처리를 통해 성능 향상.
        - 자원 공유로 메모리 오버헤드 감소.
        - 응답성 개선.
```c
#include <stdio.h>
#include <pthread.h>

void* thread_function(void* arg) {
    printf("Thread %d is running.\n", *(int*)arg);
    return NULL;
}

int main() {
    pthread_t threads[2];
    int thread_args[2] = {1, 2};

    for (int i = 0; i < 2; i++) {
        pthread_create(&threads[i], NULL, thread_function, &thread_args[i]);
    }

    for (int i = 0; i < 2; i++) {
        pthread_join(threads[i], NULL);
    }

    return 0;
}
```
### **CPU 스케줄링 (CPU Scheduling)**

1. **선점형 스케줄링 (Preemptive Scheduling)**
    - 프로세스가 실행 중이어도 다른 프로세스가 CPU를 강제로 차지할 수 있는 스케줄링 방식.
    - 알고리즘:
        - **SJF (Shortest Job First)**: 실행 시간이 가장 짧은 프로세스 우선.
        - **Priority Scheduling**: 우선순위가 높은 프로세스 우선.
        - **Round Robin**: 프로세스마다 동일한 시간(Time Quantum)을 할당.
2. **비선점형 스케줄링 (Non-preemptive Scheduling)**
    - 프로세스가 실행되면 CPU를 반환할 때까지 다른 프로세스가 차지할 수 없음.
    - 알고리즘:
        - **FCFS (First-Come-First-Served)**: 도착한 순서대로 실행.
        - **Priority Scheduling**: 우선순위 기반 실행.
3. **스케줄링 성능 평가**
    - **응답 시간(Response Time)**: 요청 후 첫 응답까지의 시간.
    - **대기 시간(Waiting Time)**: 준비 큐에서 대기한 시간.
    - **처리량(Throughput)**: 단위 시간당 완료된 프로세스 수.

### **동기화 (Synchronization)**

1. **임계 구역 문제 (Critical Section Problem)**
    - 여러 프로세스가 동시에 공유 자원에 접근할 때 데이터의 무결성을 보장해야 하는 문제.
    - 해결 조건: 상호 배제(Mutual Exclusion), 진행(Progress), 유한 대기(Bounded Waiting).
```c
#include <stdio.h>
#include <pthread.h>

pthread_mutex_t mutex;
int counter = 0;

void* increment(void* arg) {
    pthread_mutex_lock(&mutex);
    counter++;
    printf("Counter: %d\n", counter);
    pthread_mutex_unlock(&mutex);
    return NULL;
}

int main() {
    pthread_t threads[3];
    pthread_mutex_init(&mutex, NULL);

    for (int i = 0; i < 3; i++) {
        pthread_create(&threads[i], NULL, increment, NULL);
    }

    for (int i = 0; i < 3; i++) {
        pthread_join(threads[i], NULL);
    }

    pthread_mutex_destroy(&mutex);
    return 0;
}
```
2. **세마포어(Semaphore)와 모니터(Monitor)**
    - **세마포어**: 공유 자원의 접근을 제어하기 위한 변수.
        - **카운팅 세마포어**: 공유 자원의 개수를 추적.
        - **이진 세마포어**: 0과 1만 가지는 뮤텍스와 유사.
    - **모니터**: 공유 자원을 안전하게 관리하는 고수준 동기화 도구.
3. **뮤텍스(Mutex)와 조건 변수(Condition Variables)**
    - **뮤텍스**: 하나의 스레드만 자원을 사용하도록 보장.
    - **조건 변수**: 특정 조건이 충족될 때까지 대기하도록 하는 동기화 도구.

### **교착상태 (Deadlock)**

1. **교착상태의 조건 (Conditions for Deadlock)**
    - **상호 배제(Mutual Exclusion)**: 한 번에 한 프로세스만 자원 사용 가능.
    - **점유 및 대기(Hold and Wait)**: 자원을 보유한 상태에서 추가 자원을 대기.
    - **비선점(No Preemption)**: 프로세스가 자원을 자발적으로 반납해야 함.
    - **순환 대기(Circular Wait)**: 자원 대기가 순환 구조를 형성.
2. **교착상태 해결 방법 (Deadlock Handling)**
    - **예방(Prevention)**: 교착상태 조건 중 하나를 제거.
    - **회피(Avoidance)**: 교착상태를 피할 수 있는 상태에서만 자원 할당.
    - **탐지(Detection)**: 교착상태를 탐지하고 해결.
    - **복구(Recovery)**: 교착상태를 해결하기 위해 프로세스를 종료하거나 자원을 회수.

---

다음은 **메모리 관리 (Memory Management)** 항목을 이어서 설명하겠습니다.

### **메모리 관리 (Memory Management)**

### **메모리 계층 구조 (Memory Hierarchy)**

메모리는 속도와 비용, 용량의 균형에 따라 계층적으로 구성됩니다.

1. **레지스터(Register)**: CPU 내부에 있는 가장 빠른 메모리. 용량이 작고 비용이 높음.
2. **캐시(Cache)**: CPU와 메인 메모리 사이에 위치하며, 자주 사용하는 데이터를 저장.
3. **주기억장치(Main Memory)**: 실행 중인 프로그램과 데이터를 저장하며, DRAM을 사용.
4. **보조기억장치(Secondary Storage)**: HDD, SSD 등 대용량 데이터 저장.
5. **아카이브/백업(Storage Archive/Backup)**: 속도는 느리지만 데이터 장기 저장에 사용.

### **주기억장치 관리 (Main Memory Management)**

1. **단순 관리 (Simple Management)**
    - **고정 분할(Fixed Partition)**: 메모리를 고정된 크기의 블록으로 나눔.
        - 장점: 관리가 간단.
        - 단점: 내부 단편화(Internal Fragmentation).
    - **가변 분할(Variable Partition)**: 프로세스 크기에 따라 메모리를 동적으로 할당.
        - 장점: 단편화 감소.
        - 단점: 외부 단편화(External Fragmentation) 발생 가능.
2. **페이징(Paging)**
    - 메모리를 같은 크기의 페이지로 나누고, 프로세스도 동일 크기의 페이지로 분할하여 관리.
    - 외부 단편화가 제거되며, 주소 변환에 **페이지 테이블(Page Table)** 사용.
3. **세그멘테이션(Segmentation)**
    - 메모리를 논리적인 세그먼트(코드, 데이터 등)로 나누는 방식.
    - 사용자가 논리적으로 프로그램을 구성하기에 적합.
4. **페이징과 세그멘테이션의 조합**
    - 세그먼트를 다시 페이지로 나누는 방식으로, 세그멘테이션과 페이징의 장점을 결합.

### **가상 메모리 (Virtual Memory)**

1. **가상 메모리의 개념**
    - 물리 메모리보다 큰 메모리를 사용할 수 있도록 지원하며, 실제 메모리와 스왑 공간을 활용.
2. **페이지 교체 알고리즘 (Page Replacement Algorithms)**
    - **FIFO (First-In-First-Out)**: 가장 오래된 페이지 교체.
    - **LRU (Least Recently Used)**: 가장 오랫동안 사용되지 않은 페이지 교체.
    - **Optimal**: 미래에 가장 오래 사용되지 않을 페이지를 교체(이론적인 최적 해법).
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
3. **스왑 공간 관리 (Swap Space Management)**
    - 디스크 공간을 가상 메모리로 사용하여 프로세스의 일시적인 데이터를 저장.

---

다음은 **파일 시스템 (File System)** 항목을 이어서 설명하겠습니다.

### **파일 시스템 (File System)**

### **파일의 개념과 구조 (Concept and Structure of Files)**

- **파일(File)**: 데이터를 저장하는 논리적 단위.
    - 파일은 텍스트 파일, 바이너리 파일, 실행 파일 등으로 구분됩니다.
- **파일 속성(File Attributes)**: 이름, 식별자, 유형, 위치, 크기, 생성 시간, 권한 등이 포함됩니다.

### **디렉토리 구조 (Directory Structure)**

디렉토리는 파일을 조직화하고 관리하기 위한 구조를 제공합니다.

1. **단일 레벨(Single Level)**
    - 모든 파일이 하나의 디렉토리에 저장됩니다.
    - 단점: 파일 이름 충돌 발생 가능.
2. **다중 레벨(Multi-Level)**
    - 디렉토리 안에 서브 디렉토리를 포함하여 계층 구조를 형성.
    - 장점: 파일의 체계적인 관리 가능.
3. **트리 구조(Tree Structure)**
    - 다중 레벨 디렉토리 구조를 확장하여 계층적으로 트리 형태를 구성.
    - 장점: 파일 검색과 관리 용이.

### **파일 할당 방법 (File Allocation Methods)**

1. **연속 할당(Contiguous Allocation)**
    - 파일이 연속된 블록에 저장.
    - 장점: 빠른 접근 속도.
    - 단점: 외부 단편화 문제.
2. **연결 할당(Linked Allocation)**
    - 파일 블록을 연결 리스트 형태로 저장.
    - 장점: 단편화 문제 해결.
    - 단점: 블록 탐색 속도 저하.
3. **색인 할당(Indexed Allocation)**
    - 모든 블록의 주소를 색인 블록에 저장.
    - 장점: 빠른 접근 속도와 유연성.

### **파일 시스템 구현 (File System Implementation)**

1. **디스크 스케줄링 알고리즘 (Disk Scheduling Algorithms)**
    - **FCFS (First-Come-First-Served)**: 요청 순서대로 처리.
    - **SSTF (Shortest Seek Time First)**: 가장 가까운 요청 우선 처리.
    - **SCAN**: 디스크 헤드가 끝까지 이동하며 요청 처리.
    - **C-SCAN (Circular SCAN)**: 한쪽 방향으로만 스캔 후 다시 처음으로 돌아감.
```c
#include <stdio.h>
#include <stdlib.h>

void scan(int requests[], int n, int head) {
    int total = 0, direction = 1; // 1: Increasing, -1: Decreasing
    int max_cylinder = 200; // Assuming max cylinder is 200

    printf("SCAN Order: ");
    for (int i = 0; i < n; i++) {
        if ((direction == 1 && requests[i] >= head) || (direction == -1 && requests[i] <= head)) {
            printf("%d ", requests[i]);
            total += abs(requests[i] - head);
            head = requests[i];
        }
    }

    if (direction == 1) {
        printf("%d ", max_cylinder);
        total += abs(max_cylinder - head);
        head = max_cylinder;
        direction = -1;
    }

    printf("\nTotal Head Movement: %d\n", total);
}

int main() {
    int requests[] = {50, 80, 10, 90, 20};
    int n = sizeof(requests) / sizeof(requests[0]);
    int head = 40;

    scan(requests, n, head);
    return 0;
}
```
2. **파일 시스템 무결성 (File System Integrity)**
    - **저널링(Journaling)**: 메타데이터를 기록하여 시스템 충돌 시 복구 가능.
    - **RAID (Redundant Array of Independent Disks)**: 디스크 데이터를 중복 저장하여 성능 및 신뢰성 강화.

---

다음은 **입출력 관리 (I/O Management)** 항목을 이어서 설명하겠습니다.

### **입출력 관리 (I/O Management)**

### **I/O 하드웨어와 소프트웨어 (I/O Hardware and Software)**

1. **I/O 하드웨어**
    - **입력 장치(Input Devices)**: 키보드, 마우스, 스캐너 등.
    - **출력 장치(Output Devices)**: 모니터, 프린터 등.
    - **저장 장치(Storage Devices)**: HDD, SSD, USB 등.
    - **통신 장치(Communication Devices)**: 네트워크 카드, 모뎀 등.
2. **I/O 소프트웨어 계층**
    - **장치 드라이버(Device Driver)**: 하드웨어와 운영체제 간의 인터페이스를 제공.
    - **운영체제 I/O 관리**: I/O 요청 스케줄링, 버퍼링(Buffering) 등 처리.

### **장치 드라이버의 역할 (Role of Device Drivers)**

- 장치별 고유 명령과 프로토콜을 운영체제가 표준화된 방식으로 접근 가능하게 함.
- 주요 기능:
    - 장치 초기화 및 구성.
    - 데이터 읽기/쓰기 명령 처리.
    - 오류 처리 및 보고.

### **인터럽트와 폴링 (Interrupts and Polling)**

1. **인터럽트(Interrupt)**
    - 장치가 CPU의 주의를 필요로 할 때 신호를 보내는 메커니즘.
    - CPU는 요청을 처리하고 원래 작업으로 복귀.
    - 장점: CPU 효율성 증가.
2. **폴링(Polling)**
    - CPU가 주기적으로 장치 상태를 확인하여 작업을 처리.
    - 단점: 불필요한 CPU 자원 낭비.

### **DMA (Direct Memory Access)**

- CPU를 거치지 않고 I/O 장치와 메모리 간 직접 데이터 전송.
- 장점: CPU의 부하를 줄이고 데이터 전송 속도 증가.
```c
#include <stdio.h>

void dma_transfer(int* source, int* destination, int size) {
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
---

### **운영체제의 보안 (Security in Operating Systems)**

### **사용자 인증 (User Authentication)**

- 사용자 신원을 확인하기 위한 메커니즘.
- 일반적인 방법:
    - **패스워드(Password)**
    - **생체 인증(Biometrics)**: 지문, 얼굴 인식.
    - **이중 인증(Multi-Factor Authentication)**: 비밀번호와 인증 앱 결합.

### **접근 제어 (Access Control)**

1. **접근 제어 리스트(ACL)**
    - 각 리소스에 대해 접근 가능한 사용자와 권한을 정의한 목록.
2. **역할 기반 접근 제어(RBAC)**
    - 사용자 역할에 따라 접근 권한을 부여.

### **암호화 및 데이터 보호 (Encryption and Data Protection)**

- 데이터 암호화를 통해 외부 침입으로부터 보호.
    - **대칭 키 암호화(Symmetric Key Encryption)**
    - **비대칭 키 암호화(Asymmetric Key Encryption)**

### **보안 정책과 공격 방지 기법 (Security Policies and Attack Mitigation)**

1. **방화벽(Firewall)**: 네트워크 트래픽 필터링.
2. **IDS/IPS (Intrusion Detection/Prevention System)**: 침입 탐지 및 차단.
3. **악성코드 탐지**: 바이러스, 랜섬웨어 방지.

---

### **분산 및 병렬 처리 (Distributed and Parallel Processing)**

### **분산 시스템의 개념과 특성 (Concepts and Characteristics of Distributed Systems)**

- 여러 독립적인 컴퓨터가 네트워크를 통해 협력하여 하나의 시스템처럼 동작.
- 주요 특징:
    - **자원 공유(Resource Sharing)**
    - **확장성(Scalability)**
    - **장애 허용(Fault Tolerance)**

### **클러스터링 및 로드 밸런싱 (Clustering and Load Balancing)**

- **클러스터링**: 여러 컴퓨터를 결합해 하나의 시스템처럼 동작.
- **로드 밸런싱**: 작업 부하를 균등하게 분배하여 성능 최적화.

### **병렬 처리와 병렬 컴퓨팅 (Parallel Processing and Computing)**

- 여러 작업을 동시에 처리하여 성능을 향상.
- 예: 멀티코어 프로세서, GPGPU 기반 컴퓨팅.

### **동기화와 일관성 유지 (Synchronization and Consistency)**

- **동기화**: 여러 노드나 스레드 간의 작업을 조율.
- **일관성 유지**: 데이터의 정확성과 무결성을 보장.