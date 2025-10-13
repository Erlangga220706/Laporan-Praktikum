# <h1 align="center">Laporan Praktikum Modul 4 Sinkly linked list </h1>
<p align="center">Radithia Erlangga - 103112400096</p>

## Dasar Teori

Linked List merupakan salah satu bentuk struktur data yang digunakan untuk menyimpan sekumpulan data secara dinamis, di mana setiap elemen saling terhubung melalui pointer. Berbeda dengan array yang bersifat statis dan memiliki ukuran tetap, linked list bersifat fleksibel karena dapat menambah atau menghapus elemen sesuai kebutuhan. Setiap elemen dalam linked list disebut node, yang umumnya terdiri dari dua bagian: data dan pointer yang menunjuk ke node berikutnya. Struktur ini memudahkan pengelolaan data yang sering berubah ukurannya. Dalam implementasinya, pointer digunakan untuk menghubungkan antar node menggunakan operator ->. Linked list cocok digunakan pada kondisi ketika jumlah data tidak diketahui secara pasti dan diperlukan efisiensi dalam proses penyisipan atau penghapusan elemen.
## Guide

## Likedlist.cpp
```go
#include <iostream>
using namespace std;

// Struktur Node
struct Node {
    int data;
    Node* next;
};

// Pointer awal dan akhir
Node* head = nullptr;

// Fungsi untuk membuat node baru
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}


void insertBelakang(int data) {
    Node* newNode = createNode(data);
    if (head == nullptr) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void insertSetelah(int target, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != target) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << target << " tidak ditemukan!\n";
    } else {
        Node* newNode = createNode(dataBaru);
        newNode->next = temp->next;
        temp->next = newNode;
        cout << "Data " << dataBaru << " berhasil disisipkan setelah " << target << ".\n";
    }
}

// ========== DELETE FUNCTION ==========
void hapusNode(int data) {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    Node* prev = nullptr;

    // Jika data di node pertama
    if (temp != nullptr && temp->data == data) {
        head = temp->next;
        delete temp;
        cout << "Data " << data << " berhasil dihapus.\n";
        return;
    }

    // Cari node yang akan dihapus
    while (temp != nullptr && temp->data != data) {
        prev = temp;
        temp = temp->next;
    }

    // Jika data tidak ditemukan
    if (temp == nullptr) {
        cout << "Data " << data << " tidak ditemukan!\n";
        return;
    }

    prev->next = temp->next;
    delete temp;
    cout << "Data " << data << " berhasil dihapus.\n";
}

// ========== UPDATE FUNCTION ==========
void updateNode(int dataLama, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != dataLama) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << dataLama << " tidak ditemukan!\n";
    } else {
        temp->data = dataBaru;
        cout << "Data " << dataLama << " berhasil diupdate menjadi " << dataBaru << ".\n";
    }
}

// ========== DISPLAY FUNCTION ==========
void tampilkanList() {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    cout << "Isi Linked List: ";
    while (temp != nullptr) {
        cout << temp->data << " -> ";
        temp = temp->next
    }
    cout << "NULL\n";
}

// ========== MAIN PROGRAM ==========
int main() {
    int pilihan, data, target, dataBaru;

    do {
        cout << "\n=== MENU SINGLE LINKED LIST ===\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah\n";
        cout << "4. Hapus Data\n";
        cout << "5. Update Data\n";
        cout << "6. Tampilkan List\n";
        cout << "0. Keluar\n";
        cout << "Pilih: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                insertDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                insertBelakang(data);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                insertSetelah(target, dataBaru);
                break;
            case 4:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> data;
                hapusNode(data);
                break;
            case 5:
                cout << "Masukkan data lama: ";
                cin >> data;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                updateNode(data, dataBaru);
                break;
            case 6:
                tampilkanList();
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 0);

    return 0;
}

```

## Unguide

### Soal 1

Buatlah single linked list untuk Antrian yang menyimpan data pembeli( nama dan pesanan). program memiliki beberapa menu seperti tambah antrian, layani antrian(hapus), dan tampilkan antrian. *antrian pertama harus yang pertama dilayani menggunakan c++
```go
#include <iostream>
#include <string>
using namespace std;

struct Pembeli {
    string nama;
    string pesanan;
    Pembeli* next; 
};


Pembeli* front = nullptr;
Pembeli* rear = nullptr;


bool isEmpty() {
    return (front == nullptr);
}


void tambahAntrian(string nama, string pesanan) {
    Pembeli* baru = new Pembeli;
    baru->nama = nama;
    baru->pesanan = pesanan;
    baru->next = nullptr;

    if (isEmpty()) {
        front = rear = baru;
    } else {
        rear->next = baru;
        rear = baru;
    }
    cout << "Antrian untuk " << nama << " berhasil ditambahkan.\n";
}


void layaniAntrian() {
    if (isEmpty()) {
        cout << "Antrian kosong, tidak ada yang dilayani.\n";
    } else {
        Pembeli* hapus = front;
        cout << "Melayani pembeli: " << hapus->nama
             << " | Pesanan: " << hapus->pesanan << endl;
        front = front->next;
        delete hapus;

        if (front == nullptr)
            rear = nullptr; 
    }
}


void tampilAntrian() {
    if (isEmpty()) {
        cout << "Antrian kosong.\n";
    } else {
        cout << "\n=== DAFTAR ANTRIAN PEMBELI ===\n";
        Pembeli* bantu = front;
        int nomor = 1;
        while (bantu != nullptr) {
            cout << nomor++ << ". Nama: " << bantu->nama
                 << " | Pesanan: " << bantu->pesanan << endl;
            bantu = bantu->next;
        }
        cout << "===============================\n";
    }
}


int main() {
    int pilihan;
    string nama, pesanan;

    do {
        cout << "\n===== MENU ANTRIAN PEMBELI =====" << endl;
        cout << "1. Tambah Antrian" << endl;
        cout << "2. Layani Antrian" << endl;
        cout << "3. Tampilkan Antrian" << endl;
        cout << "4. Keluar" << endl;
        cout << "Pilih menu (1-4): ";
        cin >> pilihan;
        cin.ignore(); 

        switch (pilihan) {
            case 1:
                cout << "Masukkan Nama Pembeli   : ";
                getline(cin, nama);
                cout << "Masukkan Pesanan        : ";
                getline(cin, pesanan);
                tambahAntrian(nama, pesanan);
                break;

            case 2:
                layaniAntrian();
                break;

            case 3:
                tampilAntrian();
                break;

            case 4:
                cout << "Terima kasih, program selesai.\n";
                break;

            default:
                cout << "Pilihan tidak valid, coba lagi.\n";
        }
    } while (pilihan != 4);

    return 0;
}

```

> Output
> ![Screenshot bagian x](Output/week3no1.jpg)

-Program ini menggunakan linked list untuk membuat sistem antrian pembeli.
-Struct Pembeli berisi data nama, pesanan, dan pointer next.
-Fungsi tambahAntrian() menambah data di belakang (enqueue).
-Fungsi layaniAntrian() menghapus data di depan (dequeue).
-Fungsi tampilAntrian() menampilkan semua pembeli dalam antrian.
-Program berjalan terus sampai pengguna memilih menu Keluar, dan mengikuti konsep FIFO (First In First Out) — pembeli pertama dilayani pertama kali.


### Soal 2
buatlah program kode untuk membalik (reverse) singly linked list (1-2-3 menjadi 3-2-1)

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

Buatlah program dengan ketentuan :

-2 buah array 2D integer berukuran 3x3 dan 2 buah pointer integer
-fungsi/prosedur yang menampilkan isi sebuah array integer 2D
-fungsi/prosedur yang akan menukarkan isi dari 2 array integer 2D pada posisi tertentu
-fungsi/prosedur yang akan menukarkan isi dari variabel yang ditunjuk oleh 2 buah pointerBuatlah program dengan ketentuan :

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

