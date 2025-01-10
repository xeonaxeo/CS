# 네트워크(Network)

## 네트워크 개요

### 1. 네트워크의 정의와 필요성

**네트워크**는 두 개 이상의 장치가 데이터를 교환하기 위해 연결된 구조를 의미합니다. 네트워크는 정보 공유, 자원 활용, 효율적인 데이터 관리 등을 가능하게 하며, 현대 사회에서 필수적인 기술 기반입니다.

**필요성**:

- **자원 공유**: 프린터, 저장 공간 등 공용 자원 사용.
- **커뮤니케이션**: 이메일, 화상 회의 등 정보 교환.
- **비즈니스**: 고객 관리, 데이터 분석 등 업무 효율성 증대.

---

### 2. 데이터 통신의 기본 구성 요소

1. **송신자(Sender)**: 데이터를 보내는 주체(예: 컴퓨터, 스마트폰).
2. **수신자(Receiver)**: 데이터를 받는 주체(예: 서버, 사용자 장치).
3. **메시지(Message)**: 송신자가 전달하려는 정보(텍스트, 이미지 등).
4. **전송 매체(Medium)**: 데이터를 전달하는 물리적/논리적 경로(유선, 무선).
5. **프로토콜(Protocol)**: 통신 규칙을 정의한 약속(TCP/IP, HTTP 등).

---

### 3. 네트워크 모델

### OSI 7계층 모델

1. **Physical Layer(물리 계층)**: 전기적, 기계적 신호 전송.
2. **Data Link Layer(데이터 링크 계층)**: MAC 주소, 오류 제어.
3. **Network Layer(네트워크 계층)**: IP 주소, 라우팅.
4. **Transport Layer(전송 계층)**: 데이터 전송 신뢰성(TCP/UDP).
5. **Session Layer(세션 계층)**: 연결 설정 및 관리.
6. **Presentation Layer(표현 계층)**: 데이터 변환, 암호화.
7. **Application Layer(응용 계층)**: 사용자 인터페이스 제공(HTTP, FTP).

### TCP/IP 모델

1. **Network Interface**: OSI 물리 + 데이터 링크 계층.
2. **Internet**: OSI 네트워크 계층.
3. **Transport**: OSI 전송 계층.
4. **Application**: OSI 세션, 표현, 응용 계층.
```c
//TCP서버
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 8080
#define BUFFER_SIZE 1024

int main() {
    int server_fd, client_fd;
    struct sockaddr_in address;
    int addr_len = sizeof(address);
    char buffer[BUFFER_SIZE] = {0};

    // 소켓 생성
    if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) == 0) {
        perror("Socket failed");
        exit(EXIT_FAILURE);
    }

    // 주소 설정
    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(PORT);

    // 소켓 바인딩
    if (bind(server_fd, (struct sockaddr*)&address, sizeof(address)) < 0) {
        perror("Bind failed");
        exit(EXIT_FAILURE);
    }

    // 대기 상태로 설정
    if (listen(server_fd, 3) < 0) {
        perror("Listen failed");
        exit(EXIT_FAILURE);
    }

    printf("Waiting for connection...\n");
    if ((client_fd = accept(server_fd, (struct sockaddr*)&address, (socklen_t*)&addr_len)) < 0) {
        perror("Accept failed");
        exit(EXIT_FAILURE);
    }

    read(client_fd, buffer, BUFFER_SIZE);
    printf("Message received: %s\n", buffer);

    char* message = "Hello from server!";
    send(client_fd, message, strlen(message), 0);

    close(client_fd);
    close(server_fd);
    return 0;
}
```
```c
///TCP클라이언트
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 8080
#define BUFFER_SIZE 1024

int main() {
    int sock;
    struct sockaddr_in server_address;
    char* message = "Hello from client!";
    char buffer[BUFFER_SIZE] = {0};

    // 소켓 생성
    if ((sock = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        perror("Socket creation failed");
        exit(EXIT_FAILURE);
    }

    // 서버 주소 설정
    server_address.sin_family = AF_INET;
    server_address.sin_port = htons(PORT);

    if (inet_pton(AF_INET, "127.0.0.1", &server_address.sin_addr) <= 0) {
        perror("Invalid address");
        exit(EXIT_FAILURE);
    }

    if (connect(sock, (struct sockaddr*)&server_address, sizeof(server_address)) < 0) {
        perror("Connection failed");
        exit(EXIT_FAILURE);
    }

    send(sock, message, strlen(message), 0);
    printf("Message sent to server.\n");

    read(sock, buffer, BUFFER_SIZE);
    printf("Message received: %s\n", buffer);

    close(sock);
    return 0;
}
```
---

### 4. 네트워크의 종류

1. **LAN(Local Area Network)**: 소규모 네트워크(가정, 사무실).
2. **WAN(Wide Area Network)**: 대규모 네트워크(인터넷).
3. **MAN(Metropolitan Area Network)**: 도시 규모 네트워크.
4. **PAN(Personal Area Network)**: 개인 장치 연결(Bluetooth).
5. **WLAN(Wireless LAN)**: 무선 LAN(Wi-Fi).
6. **SAN(Storage Area Network)**: 데이터 저장 네트워크.

---

### 5. 네트워크 토폴로지

1. **스타(Star)**: 중앙 허브에 연결, 설치 용이, 허브 고장 시 전체 중단.
2. **버스(Bus)**: 단일 케이블, 설치 비용 적음, 장애 시 문제 해결 어려움.
3. **링(Ring)**: 순환 구조, 데이터 충돌 방지, 단절 시 전체 중단.
4. **메시(Mesh)**: 모든 장치 연결, 높은 안정성, 설치 비용 높음.
5. **트리(Tree)**: 계층적 구조, 대규모 네트워크 적합, 관리 복잡.

---

## 데이터 통신 및 전송 기술

### 1. 데이터 표현과 신호

- **디지털 데이터**: 이진 신호(0과 1), 샘플링(디지털 변환).
- **아날로그 신호**: 주파수(Hz), 진폭(신호 크기), 위상(신호 시작점).

### 2. 부호화와 변조

1. **부호화**:
    - **라인 부호화**: 디지털 데이터를 전송 가능한 신호로 변환.
2. **변조**:
    - **주파수 변조(FM)**: 주파수 변경.
    - **진폭 변조(AM)**: 신호 크기 변경.
    - **위상 변조(PM)**: 위상 변화.

### 3. 다중화 기술

- **TDM(Time Division Multiplexing)**: 시간 분할.
- **FDM(Frequency Division Multiplexing)**: 주파수 분할.
- **CDM(Code Division Multiplexing)**: 코드 분할.

### 4. 전송 방식

1. **직렬 전송**: 데이터 순차 전송.
2. **병렬 전송**: 데이터 동시 전송.
3. **동기식 전송**: 일정한 클럭 신호.
4. **비동기식 전송**: 클럭 신호 없음, 스타트/스톱 비트 활용.

---

## 네트워크 프로토콜

### 1. 프로토콜의 개념과 역할

**프로토콜**은 데이터 통신을 위한 규칙 및 약속입니다. 데이터 송수신의 효율성과 신뢰성을 보장합니다.

### 2. 주요 계층별 프로토콜

- **데이터 링크 계층**: Ethernet, PPP, HDLC, MAC.
- **네트워크 계층**: IPv4, IPv6, ICMP, ARP.
- **전송 계층**: TCP(연결형), UDP(비연결형).
- **응용 계층**: HTTP/HTTPS, FTP, SMTP, DNS, DHCP.
```c
//ARP
#include <stdio.h>
#include <string.h>

typedef struct {
    char ip[16];
    char mac[18];
} ARPEntry;

int main() {
    ARPEntry arp_table[] = {
        {"192.168.1.1", "00:14:22:01:23:45"},
        {"192.168.1.2", "00:16:36:00:78:AB"},
        {"192.168.1.3", "00:18:62:00:78:CD"}
    };

    char query_ip[16];
    printf("Enter an IP address to resolve: ");
    scanf("%s", query_ip);

    for (int i = 0; i < 3; i++) {
        if (strcmp(query_ip, arp_table[i].ip) == 0) {
            printf("MAC Address: %s\n", arp_table[i].mac);
            return 0;
        }
    }

    printf("IP address not found in ARP table.\n");
    return 0;
}
```
```c
///FTP서버코드(파일송신)
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 8080
#define BUFFER_SIZE 1024

int main() {
    int server_fd, client_fd;
    struct sockaddr_in address;
    int addr_len = sizeof(address);
    char buffer[BUFFER_SIZE] = {0};
    FILE *file;

    // 소켓 생성
    if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) == 0) {
        perror("Socket failed");
        exit(EXIT_FAILURE);
    }

    // 주소 설정
    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(PORT);

    // 소켓 바인딩
    if (bind(server_fd, (struct sockaddr*)&address, sizeof(address)) < 0) {
        perror("Bind failed");
        exit(EXIT_FAILURE);
    }

    // 대기 상태로 설정
    if (listen(server_fd, 3) < 0) {
        perror("Listen failed");
        exit(EXIT_FAILURE);
    }

    printf("Waiting for connection...\n");
    if ((client_fd = accept(server_fd, (struct sockaddr*)&address, (socklen_t*)&addr_len)) < 0) {
        perror("Accept failed");
        exit(EXIT_FAILURE);
    }

    printf("Connection established. Sending file...\n");

    // 파일 열기
    file = fopen("file_to_send.txt", "r");
    if (file == NULL) {
        perror("File not found");
        close(client_fd);
        close(server_fd);
        exit(EXIT_FAILURE);
    }

    // 파일 읽기 및 전송
    size_t bytes_read;
    while ((bytes_read = fread(buffer, 1, BUFFER_SIZE, file)) > 0) {
        send(client_fd, buffer, bytes_read, 0);
    }

    printf("File sent successfully.\n");

    fclose(file);
    close(client_fd);
    close(server_fd);
    return 0;
}

```
```c
//FTP클라이언트코드(파일수신)
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 8080
#define BUFFER_SIZE 1024

int main() {
    int sock;
    struct sockaddr_in server_address;
    char buffer[BUFFER_SIZE] = {0};
    FILE *file;

    // 소켓 생성
    if ((sock = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        perror("Socket creation failed");
        exit(EXIT_FAILURE);
    }

    // 서버 주소 설정
    server_address.sin_family = AF_INET;
    server_address.sin_port = htons(PORT);

    if (inet_pton(AF_INET, "127.0.0.1", &server_address.sin_addr) <= 0) {
        perror("Invalid address");
        exit(EXIT_FAILURE);
    }

    // 서버에 연결
    if (connect(sock, (struct sockaddr*)&server_address, sizeof(server_address)) < 0) {
        perror("Connection failed");
        exit(EXIT_FAILURE);
    }

    printf("Connected to server. Receiving file...\n");

    // 파일 생성
    file = fopen("received_file.txt", "w");
    if (file == NULL) {
        perror("File creation failed");
        close(sock);
        exit(EXIT_FAILURE);
    }

    // 데이터 수신 및 파일 저장
    size_t bytes_received;
    while ((bytes_received = recv(sock, buffer, BUFFER_SIZE, 0)) > 0) {
        fwrite(buffer, 1, bytes_received, file);
    }

    printf("File received successfully.\n");

    fclose(file);
    close(sock);
    return 0;
}
```
---

## 네트워크 장비

1. **스위치(Switch)**: 데이터 전달 장비(MAC 주소 사용).
2. **라우터(Router)**: IP 주소 기반 데이터 라우팅.
3. **방화벽(Firewall)**: 네트워크 접근 제어.
4. **무선 액세스 포인트(WAP)**: Wi-Fi 제공.

---

## 네트워크 설계와 관리

### 1. 설계 원칙

- **확장성**: 증가하는 트래픽 처리 가능.
- **신뢰성**: 장애 복구 능력.
- **비용 효율성**: 최소 비용으로 설계.

### 2. IP 주소 체계

1. **IPv4**: 32비트, 서브넷팅.
2. **IPv6**: 128비트, 더 큰 주소 공간.

### 3. VLAN과 NAT

- **VLAN**: 네트워크 분리, 보안 향상.
- **NAT**: 공인 IP 절약, 내부 IP 숨김.

---

## 라우팅 및 스위치

### 1. 라우팅 프로토콜

- RIP, OSPF, EIGRP, BGP.

### 2. 스위치 관리

- **STP**: 루프 방지.
- **MAC 주소 테이블**: 데이터 전달 최적화.
```c
#include <stdio.h>
#include <string.h>

typedef struct {
    char destination[16];
    char next_hop[16];
    char interface[10];
} RoutingEntry;

int main() {
    RoutingEntry routing_table[] = {
        {"192.168.1.0", "192.168.1.1", "eth0"},
        {"10.0.0.0", "10.0.0.1", "eth1"},
        {"172.16.0.0", "172.16.0.1", "eth2"}
    };

    char query_ip[16];
    printf("Enter a destination IP address: ");
    scanf("%s", query_ip);

    for (int i = 0; i < 3; i++) {
        if (strcmp(query_ip, routing_table[i].destination) == 0) {
            printf("Next Hop: %s, Interface: %s\n", routing_table[i].next_hop, routing_table[i].interface);
            return 0;
        }
    }

    printf("No route found for the given IP address.\n");
    return 0;
}
```
---

## 네트워크 보안

### 1. 위협과 공격

- **DoS/DDoS**: 서비스 방해.
- **스니핑**: 데이터 도청.
- **피싱**: 사용자 기만.
- **MITM**: 중간 공격.

### 2. 보안 기술

- **암호화**: 대칭키, 비대칭키.
- **SSL/TLS, IPSec**: 안전한 데이터 전송.

---

## 심화 주제

### 1. SDN 및 NFV

- **SDN**: 네트워크 중앙 제어.
- **NFV**: 네트워크 기능 가상화.

### 2. MPLS

**MPLS**는 데이터 전달 경로를 최적화하여 효율성을 높이는 기술입니다.