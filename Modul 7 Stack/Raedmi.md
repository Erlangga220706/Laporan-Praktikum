# <h1 align="center">Laporan Praktikum Modul 7 Stack</h1>
<p align="center">Radithia Erlangga - 103112400096</p>

## Dasar Teori
Stack adalah salah satu struktur data yang menggunakan prinsip LIFO (Last In, First Out), yaitu elemen yang terakhir dimasukkan akan menjadi elemen pertama yang dikeluarkan. Struktur ini dapat diibaratkan seperti tumpukan piring, di mana piring yang terakhir diletakkan di atas akan diambil terlebih dahulu. Operasi utama pada stack meliputi push (menambahkan elemen ke puncak stack), pop (menghapus elemen dari puncak stack), dan peek/top (melihat elemen teratas tanpa menghapusnya). Stack banyak digunakan dalam pemrograman, seperti untuk menyimpan data sementara dalam pemanggilan fungsi (call stack), membalik urutan data, dan dalam proses evaluasi ekspresi matematika atau algoritma backtracking.

## Guide
```
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

bool isEmpety(Node *top)
{
    return top == nullptr;
}

void push(Node *&top, int data){
    Node *newNode = new Node;
    newNode -> data = data;
    newNode -> next = top;
    top = newNode;
}

int pop(Node *&top)
{
    if (isEmpety(top))
    {
        cout << "Stack Kosong, tidak bisa pop!" << endl;
        return 0;
    }

    int poppedData = top -> data;
    top = top -> next;

    Node *temp;
    return poppedData;
}

void show (Node *top)
{
    if (isEmpety(top))
    {
        cout << "Stack kosong," << endl;
        return;
    }
    cout << "TOP -> ";
    Node *temp = top;

    while (temp != nullptr)
    {
        cout << temp->data << "-> ";
        temp = temp->next;
    }

    cout << "NULL" << endl;

}

int main()
{
    Node *stack = nullptr;

    push(stack, 10);
    push(stack, 20);
    push(stack, 30);

    cout << "Menampilkan isi stack:" << endl;
    show (stack);

    cout << "pop;" << pop(stack) << endl;

    cout << "Menampilkan sisa Stack:" << endl;
    show(stack);

    return 0;
}

```

## Unguide

### Soal 1
> ![Screenshot bagian x](Output/soal1.jpg)
## stack.h
```go
#ifndef STACK_H
#define STACK_H

const int MAX = 20;

typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);

#endif
```
## stack.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);
    while (S.top >= 0) {
        push(temp, pop(S));
    }
    S = temp;
}
```
## main.cpp
```go
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    push(S, 3);
    push(S, 4);
    push(S, 2);
    push(S, 9);
    pop(S);
    push(S, 2);
    push(S, 3);
    pop(S);
    push(S, 9);

    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);

    printInfo(S);

    return 0;
}

```

> Output
> ![Screenshot bagian x](Output/satu.jpg)
Program ini membuat struktur data stack yang bekerja dengan sistem LIFO (Last In First Out). Artinya, data yang terakhir dimasukkan akan keluar lebih dulu. Program bisa menambah data dengan push, menghapus data dengan pop, menampilkan isi stack dengan printInfo, dan membalik isi stack dengan balikStack. Di main, program mencoba beberapa operasi tersebut lalu menampilkan hasil sebelum dan sesudah stack dibalik.

### Soal 2
> ![Screenshot bagian x](Output/soal2.jpg)

# pelajaran.h
```go
#ifndef PELAJARAN_H_INCLUDED
#define PELAJARAN_H_INCLUDED
#include <string>
using namespace std;

struct Pelajaran {
    string namaMapel;
    string kodeMapel;
};

Pelajaran create_pelajaran(string namapel, string kodepel);
void tampil_pelajaran(Pelajaran pel);

#endif
```

# pelajaran.cpp
```go
#include <iostream>
#include "pelajaran.h"
using namespace std;

Pelajaran create_pelajaran(string namapel, string kodepel) {
    Pelajaran p;
    p.namaMapel = namapel;
    p.kodeMapel = kodepel;
    return p;
}

void tampil_pelajaran(Pelajaran pel) {
    cout << "nama pelajaran : " << pel.namaMapel << endl;
    cout << "nilai : " << pel.kodeMapel << endl;
}
```

# main.cpp
```go
#include <iostream>
#include "pelajaran.h"
using namespace std;

int main() {
    string namapel = "Struktur Data";
    string kodepel = "STD";

    Pelajaran pel = create_pelajaran(namapel, kodepel);
    tampil_pelajaran(pel);

    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/week3no2.jpg)

Program ini merupakan contoh penerapan Abstract Data Type (ADT) dalam C++. Konsep ADT digunakan untuk memisahkan antara tipe data, fungsi, dan program utama. Pada file pelajaran.h, terdapat tipe data struct Pelajaran dengan atribut namaMapel dan kodeMapel, serta deklarasi fungsi create_pelajaran() dan tampil_pelajaran(). File pelajaran.cpp berisi isi fungsi, yaitu membuat dan menampilkan data pelajaran. Sedangkan file main.cpp digunakan untuk menguji program dengan membuat objek pelajaran dan menampilkannya. Dengan cara ini, program lebih terstruktur, mudah dipahami, dan sesuai dengan konsep dasar ADT.

### Soal 3
> ![Screenshot bagian x](Output/soal3.jpg)

```go
#include <iostream>
using namespace std;

void tampilArray(int arr[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << arr[i][j] << "\t";
        }
        cout << endl;
    }
}

void tukarArrayPosisi(int arr1[3][3], int arr2[3][3], int baris, int kolom) {
    int temp = arr1[baris][kolom];
    arr1[baris][kolom] = arr2[baris][kolom];
    arr2[baris][kolom] = temp;
}

void tukarPointer(int *p1, int *p2) {
    int temp = *p1;
    *p1 = *p2;
    *p2 = temp;
}

int main() {
    int A[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int B[3][3] = {
        {9, 8, 7},
        {6, 5, 4},
        {3, 2, 1}
    };

    int x = 10, y = 20;
    int *ptr1 = &x;
    int *ptr2 = &y;

    cout << "=== Array A ===" << endl;
    tampilArray(A);
    cout << "\n=== Array B ===" << endl;
    tampilArray(B);

    cout << "\nMenukar elemen pada posisi [1][1] (baris 2 kolom 2)...\n";
    tukarArrayPosisi(A, B, 1, 1);

    cout << "\n=== Array A setelah ditukar ===" << endl;
    tampilArray(A);
    cout << "\n=== Array B setelah ditukar ===" << endl;
    tampilArray(B);

    cout << "\nSebelum tukar pointer:" << endl;
    cout << "x = " << x << ", y = " << y << endl;

    tukarPointer(ptr1, ptr2);

    cout << "Setelah tukar pointer:" << endl;
    cout << "x = " << x << ", y = " << y << endl;

    return 0;
}

```

> Output
> ![Screenshot bagian x](Output/week3no3.jpg)

Program ini menggunakan dua array 2D berukuran 3×3 dan dua pointer integer.
Fungsi tampilArray() digunakan untuk menampilkan isi array 2D.
Fungsi tukarArrayPosisi() menukar elemen antara dua array pada posisi tertentu (misalnya [1][1]).
Fungsi tukarPointer() menukar nilai dari dua variabel melalui pointer.
Program ini menunjukkan penggunaan array 2D, pointer, dan fungsi secara terpisah, sehingga mudah dipahami dan sesuai konsep dasar pemrograman C++.



## Referensi
1. https://www.w3schools.com/cpp/cpp_references.asp
2. https://www.w3schools.com/cpp/cpp_function_reference.asp
3. https://www.w3schools.com/cpp/cpp_function_structures.asp
4. https://www.w3schools.com/cpp/exercise.asp?x=xrcise_function_reference1
5. https://www.w3schools.com/cpp/cpp_function_param.asp

