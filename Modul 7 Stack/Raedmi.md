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

Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array
dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI
dengan rumus 0.3*uts+0.4*uas+0.3*tugas.
```go
#include <iostream>
#include <iomanip>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    float uts;
    float uas;
    float tugas;
    float nilaiAkhir;
};

float hitungNilaiAkhir(float uts, float uas, float tugas) {
    return 0.3 * uts + 0.4 * uas + 0.3 * tugas;
}

int main() {
    Mahasiswa mhs[10];
    int jumlah = 0;
    int pilihan;

    do {
        cout << "\n===== MENU DATA MAHASISWA =====" << endl;
        cout << "1. Tambah Data Mahasiswa" << endl;
        cout << "2. Tampilkan Data Mahasiswa" << endl;
        cout << "3. Keluar" << endl;
        cout << "Pilih menu (1-3): ";
        cin >> pilihan;

        switch (pilihan) {
            case 1: {
                if (jumlah >= 10) {
                    cout << "Data sudah penuh (maksimum 10)!" << endl;
                    break;
                }

                cout << "\nMasukkan data mahasiswa ke-" << jumlah + 1 << endl;
                cin.ignore();
                cout << "Nama   : ";
                getline(cin, mhs[jumlah].nama);
                cout << "NIM    : ";
                cin >> mhs[jumlah].nim;
                cout << "UTS    : ";
                cin >> mhs[jumlah].uts;
                cout << "UAS    : ";
                cin >> mhs[jumlah].uas;
                cout << "Tugas  : ";
                cin >> mhs[jumlah].tugas;

                mhs[jumlah].nilaiAkhir = hitungNilaiAkhir(mhs[jumlah].uts, mhs[jumlah].uas, mhs[jumlah].tugas);
                jumlah++;

                cout << "\nData berhasil ditambahkan!\n";
                break;
            }

            case 2: {
                if (jumlah == 0) {
                    cout << "\nBelum ada data mahasiswa.\n";
                } else {
                    cout << "\n============================================================\n";
                    cout << left << setw(15) << "Nama"
                         << setw(10) << "NIM"
                         << setw(10) << "UTS"
                         << setw(10) << "UAS"
                         << setw(10) << "Tugas"
                         << setw(10) << "Akhir" << endl;
                    cout << "============================================================\n";

                    for (int i = 0; i < jumlah; i++) {
                        cout << left << setw(15) << mhs[i].nama
                             << setw(10) << mhs[i].nim
                             << setw(10) << mhs[i].uts
                             << setw(10) << mhs[i].uas
                             << setw(10) << mhs[i].tugas
                             << setw(10) << fixed << setprecision(2) << mhs[i].nilaiAkhir
                             << endl;
                    }
                    cout << "============================================================\n";
                }
                break;
            }

            case 3:
                cout << "\nTerima kasih! Program selesai.\n";
                break;

            default:
                cout << "\nPilihan tidak valid. Silakan coba lagi.\n";
        }

    } while (pilihan != 3);

    return 0;
}

```

> Output
> ![Screenshot bagian x](Output/week3no1.jpg)

Program ini menampilkan menu utama agar pengguna bisa memilih:
1️. Tambah data mahasiswa (memasukkan nama, NIM, nilai UTS, UAS, dan tugas)
2️. Lihat semua data mahasiswa yang sudah disimpan
3️. Keluar dari program

Setiap kali data dimasukkan, program otomatis menghitung nilai akhir dengan rumus
0.3 * UTS + 0.4 * UAS + 0.3 * Tugas.
Program terus berulang sampai pengguna memilih keluar (3).


### Soal 2
> ![Screenshot bagian x](Output/soalno2.jpg)

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

