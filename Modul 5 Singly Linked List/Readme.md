
# <h1 align="center">Laporan Praktikum Modul 5 Sinkly linked list </h1>
<p align="center">Radithia Erlangga - 103112400096</p>

## Dasar Teori

Dasar teori dari Singly Linked List adalah struktur data dinamis yang terdiri dari sekumpulan node, di mana setiap node menyimpan dua bagian utama yaitu data dan pointer (penunjuk) ke node berikutnya. Tidak seperti array yang memiliki ukuran tetap, linked list memungkinkan penambahan dan penghapusan elemen secara efisien tanpa perlu menggeser data. Dalam implementasinya, penggunaan pointer menjadi hal penting untuk menghubungkan antar-node dan mengatur alur data. Operasi dasar yang dapat dilakukan pada singly linked list meliputi pembuatan node baru, penelusuran (traversal), penyisipan (insertion), penghapusan (deletion), dan pencarian (search). Dengan memahami konsep ini, mahasiswa dapat membuat program yang memanfaatkan linked list untuk mengelola data secara dinamis sesuai kebutuhan aplikasi.
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
 buatlah searcing untuk mencari nama pembeli pada unguided sebelumnya
```go
#include <iostream>
#include <string>
using namespace std;

struct Pembeli {
    string nama;
    string pesanan;
    Pembeli* next;
};

Pembeli* front = NULL;
Pembeli* rear = NULL;

void tambahAntrian(string nama, string pesanan) {
    Pembeli* baru = new Pembeli();
    baru->nama = nama;
    baru->pesanan = pesanan;
    baru->next = NULL;

    if (rear == NULL) {
        front = rear = baru;
    } else {
        rear->next = baru;
        rear = baru;
    }
    cout << "Antrian pembeli berhasil ditambahkan.\n";
}

void layaniAntrian() {
    if (front == NULL) {
        cout << "Tidak ada antrian.\n";
        return;
    }
    Pembeli* hapus = front;
    front = front->next;
    if (front == NULL)
        rear = NULL;
    delete hapus;
    cout << "Antrian pertama telah dilayani.\n";
}

void tampilAntrian() {
    if (front == NULL) {
        cout << "Antrian kosong.\n";
        return;
    }
    Pembeli* temp = front;
    cout << "\n=== Daftar Antrian Pembeli ===\n";
    while (temp != NULL) {
        cout << "Nama: " << temp->nama << ", Pesanan: " << temp->pesanan << endl;
        temp = temp->next;
    }
}

void cariPembeli(string namaCari) {
    Pembeli* temp = front;
    bool ketemu = false;
    while (temp != NULL) {
        if (temp->nama == namaCari) {
            cout << "Pembeli ditemukan: " << temp->nama 
                 << " dengan pesanan " << temp->pesanan << endl;
            ketemu = true;
            break;
        }
        temp = temp->next;
    }
    if (!ketemu)
        cout << "Pembeli dengan nama '" << namaCari << "' tidak ditemukan.\n";
}

int main() {
    int pilih;
    string nama, pesanan;

    do {
        cout << "\n=== MENU ANTRIAN PEMBELI ===\n";
        cout << "1. Tambah Antrian\n";
        cout << "2. Layani Antrian\n";
        cout << "3. Tampilkan Antrian\n";
        cout << "4. Cari Nama Pembeli\n";
        cout << "0. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilih;
        cin.ignore();

        switch (pilih) {
            case 1:
                cout << "Masukkan nama pembeli: "; getline(cin, nama);
                cout << "Masukkan pesanan: "; getline(cin, pesanan);
                tambahAntrian(nama, pesanan);
                break;
            case 2:
                layaniAntrian();
                break;
            case 3:
                tampilAntrian();
                break;
            case 4:
                cout << "Masukkan nama pembeli yang dicari: ";
                getline(cin, nama);
                cariPembeli(nama);
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid.\n";
        }
    } while (pilih != 0);

    return 0;
}


```

> Output
> ![Screenshot bagian x](Output/week3_no1.jpg)

Program ini menggunakan singly linked list untuk menyimpan data antrian pembeli.
Setiap node menyimpan nama dan pesanan, lalu dihubungkan dengan pointer next.
Data baru selalu masuk di belakang (rear) dan yang pertama keluar di depan (front).
Fitur searching menggunakan traversal dari depan untuk menemukan nama pembeli tertentu.

### Soal 2
gunakan latihan pada pertemuan minggun ini dan tambahkan seardhing untuk mencari buku berdasarkan judul, penulis, dan ISBN

# 
```go
#include <iostream>
#include <string>
using namespace std;

struct Buku {
    string judul;
    string penulis;
    string ISBN;
    Buku* next;
};

Buku* head = NULL;

void tambahBuku(string judul, string penulis, string ISBN) {
    Buku* baru = new Buku();
    baru->judul = judul;
    baru->penulis = penulis;
    baru->ISBN = ISBN;
    baru->next = head;
    head = baru;
    cout << "Data buku berhasil ditambahkan.\n";
}

void tampilBuku() {
    if (head == NULL) {
        cout << "Belum ada data buku.\n";
        return;
    }
    Buku* temp = head;
    cout << "\n=== DAFTAR BUKU ===\n";
    while (temp != NULL) {
        cout << "Judul : " << temp->judul << endl;
        cout << "Penulis : " << temp->penulis << endl;
        cout << "ISBN : " << temp->ISBN << endl;
        cout << "-------------------------\n";
        temp = temp->next;
    }
}

void cariBuku(string key, string tipe) {
    Buku* temp = head;
    bool ketemu = false;
    while (temp != NULL) {
        if ((tipe == "judul" && temp->judul == key) ||
            (tipe == "penulis" && temp->penulis == key) ||
            (tipe == "isbn" && temp->ISBN == key)) {
            cout << "\nBuku ditemukan:\n";
            cout << "Judul : " << temp->judul << endl;
            cout << "Penulis : " << temp->penulis << endl;
            cout << "ISBN : " << temp->ISBN << endl;
            ketemu = true;
        }
        temp = temp->next;
    }
    if (!ketemu)
        cout << "Buku tidak ditemukan berdasarkan " << tipe << ".\n";
}

int main() {
    int pilih;
    string judul, penulis, isbn, key, tipe;

    do {
        cout << "\n=== MENU DATA BUKU ===\n";
        cout << "1. Tambah Buku\n";
        cout << "2. Tampilkan Buku\n";
        cout << "3. Cari Buku\n";
        cout << "0. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilih;
        cin.ignore();

        switch (pilih) {
            case 1:
                cout << "Judul buku : "; getline(cin, judul);
                cout << "Penulis    : "; getline(cin, penulis);
                cout << "ISBN       : "; getline(cin, isbn);
                tambahBuku(judul, penulis, isbn);
                break;
            case 2:
                tampilBuku();
                break;
            case 3:
                cout << "Cari berdasarkan (judul/penulis/isbn): ";
                getline(cin, tipe);
                cout << "Masukkan kata kunci: ";
                getline(cin, key);
                cariBuku(key, tipe);
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid.\n";
        }
    } while (pilih != 0);

    return 0;
}


```

> Output
> ![Screenshot bagian x](Output/week3_no2.jpg)

Program ini memanfaatkan singly linked list untuk menyimpan daftar buku.
Setiap node menyimpan data judul, penulis, dan ISBN.
Penambahan data dilakukan di awal list agar efisien.
Fitur searching memungkinkan pencarian buku berdasarkan salah satu dari tiga atribut — membantu menemukan data dengan cepat tanpa harus membuka seluruh daftar manual.


## Referensi
1.https://www.w3schools.com/dsa/dsa_theory_linkedlists.php
2.https://www.w3schools.com/dsa/dsa_algo_linkedlists_operations.php
3.https://www.w3schools.com/dsa/dsa_data_linkedlists_types.php
4.https://www.w3schools.com/dsa/dsa_theory_linkedlists_memory.php
5.https://www.w3schools.com/dsa/dsa_data_queues.php

