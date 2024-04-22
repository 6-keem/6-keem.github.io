---
title : "[운영체제/구현] Mutex, Spinlock, Semaphore 구현"
date : 2024-04-22 23:29:00 +0900
categories : [운영체제]
tags : [operating system] #소문자만 가능
toc: true
toc_sticky: true
published : true
---

### 1. Mutex 구현

```c
#include <stdio.h>
#include <pthread.h>

int sum = 0;
pthread_mutex_t lock;

void * worker(void * arg){
    printf("%s 시작\t %d\n", (char*)arg, sum);
    for(int i = 0 ; i < 1000000 ; i ++){
        pthread_mutex_lock(&lock);
        sum += 10;
        pthread_mutex_unlock(&lock);
    }
    printf("%s 끝\t %d\n", (char*)arg, sum);
}

int main(){
    char * name[] = {"황기태", "이찬수"};
    pthread_t pid[2];
    pthread_attr_t attr[2];

    for(int i = 0 ; i < 2 ; i ++)
        pthread_attr_init(&attr[i]);
    
    pthread_mutex_init(&lock, NULL);
    for(int i = 0 ; i < 2 ; i ++)
        pthread_create(&pid[i], &attr[i], worker, name[i]);
    
    for(int i = 0 ; i < 2 ; i ++)
        pthread_join(pid[i], NULL);
    printf("최종 sum = %d\n", sum);
    pthread_mutex_destroy(&lock);
    return 0;
}
```



### 2. Spinlock 구현

```c
#include <stdio.h>
#include <pthread.h>

int sum = 0;
pthread_spinlock_t lock;

void * worker(void * arg){
    printf("%s 시작\t %d\n", (char*)arg, sum);
    for(int i = 0 ; i < 1000000 ; i ++){
        pthread_spin_lock(&lock);
        sum += 10;
        pthread_spin_unlock(&lock);
    }
    printf("%s 끝\t %d\n", (char*)arg, sum);
}

int main(){
    char * name [] = {"황기태","이찬수"};
    pthread_t pid[2];
    pthread_attr_t attr[2];
    
    
    for(int i = 0 ; i < 2 ; i++)
    	pthread_attr_init(&attr[i]);
    
    pthread_spin_init(&lock, PTHREAD_PROCESS_PRIVATE);
    
    for(int i = 0 ; i < 2 ; i++)
        pthread_create(&pid[i], &attr[i], worker, name[i]);
    
    for(int i = 0 ; i < 2 ; i++)
        pthread_join(pid[i],NULL);
    printf("최종 sum = %d\n", sum);
    pthread_spin_destroy(&lock);
    
    return 0;
}
```



### 3. Semaphore

```c
#include <stdio.h>
#include <pthread.h>
#include <semaphore.h>
#include <unistd.h>

sem_t toiletsem;

void * guestThread(void * arg){
    int cnt = -1;
    
    sem_wait(&toiletsem);
    sem_getvalue(&toiletsem, &cnt);
    printf("고객%s 화장실에 들어간다... 세마포 counter %d\n", (char*)arg, cnt);
    sleep(1);
    printf("고객%s 화장실에서 나온다.\n", (char*)arg);
    sem_post(&toiletsem);
}

#define NO 0
#define MAX_COUNTER 3

int main(){
    int counter = -1;
    char * name [] = {"1","2","3","4","5"};
    pthread_t pid[5];
    
    int res = sem_init(&toiletsem, NO, MAX_COUNTER);
    if (res == -1){
        printf("semaphore is not supported\n");
        return 0;
    }
    sem_getvalue(&toiletsem, &counter);
    printf("세마포 counter = %d\n", counter);
    
    for(int i = 0 ; i < 5 ; i ++)
        pthread_create(&pid[i], NULL, guestThread, name[i]);
    
    for(int i = 0 ; i < 5 ; i ++)
        pthread_join(pid[i], NULL);
    
    printf("세마포 counter = %d\n", counter);
    sem_destroy(&toiletsem);
    
    return 0;
}
```





### 4. 생산자 소비자 문제

```c
#include <stdio.h>
#include <pthread.h>
#include <semaphore.h>
#include <unistd.h>
#include <stdlib.h>

#define MILLI 1000
#define N_COUNTER 4

void mywrite(int n);
int myread();

pthread_mutex_t critical_section;
sem_t semWrite, semRead;
int queue[N_COUNTER];
int wIdx = 0;
int rIdx = 0;

void * producer(void * arg){
    for(int i = 0 ; i < 10 ; i ++){
        mywrite(i);
        int m = rand() % 10;
        usleep(MILLI * m * 10);
    }
    return NULL;
}

void * consumer(void * arg){
    for(int i = 0 ; i < 10 ; i ++){
        int n = myread();
        int m = rand() % 10;
        usleep(MILLI * m * 10);
    }
    return NULL;
}

void mywrite(int n){
	sem_wait(&semWrite); // 잔여 버퍼 용량 -1
    pthread_mutex_lock(&critical_section);
    queue[wIdx] = n;
    wIdx = (wIdx + 1) % N_COUNTER;
    pthread_mutex_unlock(&critical_section);
    printf("producer : wrote %d\n", n);
    sem_post(&semRead); // 현재 버퍼 용량 + 1
}

int myread(){
    sem_wait(&semRead); // 현재 버퍼 용량 - 1
    pthread_mutex_lock(&critical_section);
    int n = queue[rIdx];
    rIdx = (rIdx + 1) % N_COUNTER;
    pthread_mutex_unlock(&critical_section);
    printf("consumer : read %d\n", n);
    sem_post(&semWrite); // 잔여 버퍼 용량 + 1 
    return n;
}

int main(){
    pthread_t pid[2];
    
    srand(time(NULL));
    pthread_mutex_init(&critical_section, NULL);
    int res = sem_init(&semWrite, 0, N_COUNTER);
    if (res == -1){
        printf("semaphore is not supported\n");
        return 0;
    }
    sem_init(&semRead, 0, 0);
    
    pthread_create(&pid[0], NULL, producer, NULL);
    pthread_create(&pid[1], NULL, consumer, NULL);
    
    for(int i = 0 ; i < 2 ; i ++)
        pthread_join(pid[i], NULL);
    
    sem_destroy(&semWrite);
    sem_destroy(&semRead);
    
    pthread_mutex_destroy(&critical_section);
    return 0;
}
```



