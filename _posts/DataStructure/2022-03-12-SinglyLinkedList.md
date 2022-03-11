---
layout: single
title: "[DS]SinglyLinkedList"
categories: ["algorithm"]
tag: [datastructure]
author_profile: true
sidebar_main: true
---

> **SinglyLinkedList**

SinglyLinkedList는 데이터를 보관하는 node와 다음 node의 주소를 저장하는 next로 구성되어있다. node의 tail 부분의 next는 NULL 값이 저장된다.

> **SinglyLinkedList Method**

* ```void addFrontNode(int n)```


LinkedList node 맨 앞에 데이터를 추가한다.
```cpp
void LinkedList::addFrontNode(int n){
    node* temp = new node;  //return받은 new node의 주소값을 temp에 저장(temp에 new node 주소 저장)
    temp->data = n; //temp의 data에 입력받은 데이터 n 저장

    if(head == NULL){   //LinkList가 비어있다면
        head = temp;    //head에 temp 저장
        tail = temp;    //tail에 temp 저장
    }   
    else{   //LinkedList에 데이터가 있다면 
        temp->next = head;  //다음 node를 가리키는 주소를 원래 있던 head로 변경
        head = temp;    //맨 앞에 새로운 데이터가 들어왔으니 temp를 head로 변경
    }
}
```

* ```void addNode(int n)```


LinkedList 맨 뒤에 데이터를 추가한다.
```cpp
void LinkedList::addNode(int n){
    node* temp = new node;
    temp->data = n;
    temp->next = NULL;

    if(head == NULL){
        head = temp;
        tail = temp;
    }
    else{
        tail->next = temp;  //다음 node를 가리키는 주소를 temp로 변경
        tail = temp;    //맨 뒤에 새로운 데이터가 들어왔으니 tail을 temp로 변경
    }
}
```

* ```void intsertNode(node* prevNode, int n)```


LinkedList 중간에 데이터를 추가한다.
```cpp
void LinkedList::insertNode(node* prev, int n){
    node* temp = new node;
    temp->data = n;

    temp->next = prev->next;    //temp는 이전의 next가 가리키는 주소 저장
    prev->next = temp;  //이전의 node가 가리키는 next에 temp 저장
}
```

* ```void deleteNode(node* prevNode)```


LinkedList 데이터를 삭제한다.
```cpp
void LinkedList::deleteNode(node* prev){
    node* temp = prev->next;    //이전의 node를 temp에 저장
    prev->next = temp->next;    //temp에 저장된 node를 이전 node에 저장

    delete temp;
}
```

* ```void display(node* head)```


LinkedList 데이터를 출력한다.
```cpp
void LinkedList::display(node* head){
    if(head == NULL){
        cout << "\n";
    }
    else{
        cout << head->data << " ";
        display(head->next);
    }
}
```

---

> **SinglyLinkedList 구현**

```cpp
#include<iostream>
using namespace std;

struct node{
    int data;
    node* next;
};

class LinkedList{
private:
    //node를 가리키는 포인터 head, tail 생성
    node* head;
    node* tail;

public:
    LinkedList();
    void addFrontNode(int n);   //LinkedList 맨 앞에 node 추가
    void addNode(int n);    //LinkedList 맨 뒤에 node 추가
    void insertNode(node* prevNode, int n); //LinkedList 중간에 node 추가 
    void deleteNode(node* prevNode);    //node 삭제
    void display(node* head);   //data 출력
    node* getHead(){    //첫번째 node 가져오기
        return head;
    }
};

LinkedList::LinkedList(){
    //head, tail 초기화
    head = NULL;
    tail = NULL;
}

void LinkedList::addFrontNode(int n){
    node* temp = new node;  //return받은 new node의 주소값을 temp에 저장(temp에 new node 주소 저장)
    temp->data = n; //temp의 data에 입력받은 데이터 n 저장

    if(head == NULL){   //LinkList가 비어있다면
        head = temp;    //head에 temp 저장
        tail = temp;    //tail에 temp 저장
    }   
    else{   //LinkedList에 데이터가 있다면 
        temp->next = head;  //다음 node를 가리키는 주소를 원래 있던 head로 변경
        head = temp;    //맨 앞에 새로운 데이터가 들어왔으니 temp를 head로 변경
    }
}

void LinkedList::addNode(int n){
    node* temp = new node;
    temp->data = n;
    temp->next = NULL;

    if(head == NULL){
        head = temp;
        tail = temp;
    }
    else{
        tail->next = temp;  //다음 node를 가리키는 주소를 temp로 변경
        tail = temp;    //맨 뒤에 새로운 데이터가 들어왔으니 tail을 temp로 변경
    }
}

void LinkedList::insertNode(node* prev, int n){
    node* temp = new node;
    temp->data = n;

    temp->next = prev->next;    //temp는 이전의 next가 가리키는 주소 저장
    prev->next = temp;  //이전의 node가 가리키는 next에 temp 저장
}

void LinkedList::deleteNode(node* prev){
    node* temp = prev->next;    //이전의 node를 temp에 저장
    prev->next = temp->next;    //temp에 저장된 node를 이전 node에 저장

    delete temp;
}

void LinkedList::display(node* head){
    if(head == NULL){
        cout << "\n";
    }
    else{
        cout << head->data << " ";
        display(head->next);
    }
}

int main(){
    LinkedList l;
    l.addNode(10);
    l.addNode(50);
    l.addNode(2);
    
    l.display(l.getHead());

    l.addFrontNode(76);

    l.insertNode(l.getHead()->next->next, 19);

    l.display(l.getHead());

    l.deleteNode(l.getHead()->next);

    l.display(l.getHead());
}
```