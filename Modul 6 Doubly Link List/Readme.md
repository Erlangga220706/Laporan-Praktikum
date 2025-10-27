
# <h1 align="center">Laporan Praktikum Modul 6 Doubly linked list </h1>
<p align="center">Radithia Erlangga - 103112400096</p>

## Dasar Teori

Doubly linked list adalah struktur data yang terdiri dari rangkaian node, di mana setiap node memiliki tiga bagian utama: data, pointer ke node sebelumnya (prev), dan pointer ke node berikutnya (next). Berbeda dengan singly linked list yang hanya bisa ditelusuri satu arah, doubly linked list memungkinkan penelusuran data baik dari depan ke belakang maupun sebaliknya, sehingga mempermudah operasi seperti penyisipan dan penghapusan data di kedua ujung atau di tengah-tengah list. Namun, penggunaan dua pointer membuat struktur ini membutuhkan lebih banyak memori dibanding singly linked list.

## Guide
```go
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* prev;
    Node* next;
};

Node* head = nullptr;
Node* tail = nullptr;

void insertDepan(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->prev = nullptr;
    newNode->next = head;

    if (head != nullptr)
       head->prev = newNode;
    else
       tail = newNode;

    head = newNode;
    cout << "Data " << data << " berhasil ditambahkan di depan. \n";
}

void insertBelakang(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    newNode->prev = tail;

    if (tail != nullptr)
        tail->next = newNode;
    else
        head = newNode;

    tail = newNode;
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void insertSetelah(int target, int data) {
    Node* current = head;
    while (current != nullptr && current ->data != target)
        current = current->next;

    if(current == nullptr) {
        cout << "Data " << target << " tidak ditemukan.\n";
        return;
    }

    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = current->next;
    newNode->prev = current;

    if (current->next != nullptr)
        current->next->prev = newNode;
    else
        tail = newNode;

    current->next = newNode;
    cout << "Data " << data << " berhasil disisipkan setelah " << target << ".\n";
}

void hapusDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    Node* temp = head;
    head = head->next;

    if (head != nullptr)
        head->prev = nullptr;
    else
        tail = nullptr;

    cout << "Data " << temp->data << " dihapus dari depan.\n";
    delete temp;
}

void hapusBelakang() {
    if  (tail == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    Node* temp = tail;
    tail = tail->prev;

    if (tail != nullptr)
        tail->next = nullptr;
    else
        head = nullptr;
    
    cout << "Data " << temp->data << " dihapus dari belakang.\n";
    delete temp;
}

void hapusData(int target) {
    Node* current = head;
    while (current != nullptr && current->data != target)
        current = current->next;

    if (current == nullptr) {
        cout << "Data " << target << " tidak ditemukan.\n";
        return;
    }

    if (current == head)
        hapusDepan();
    else if (current == tail)
        hapusBelakang();
    else {
        current->prev->next = current->next;
        current->next->prev = current->prev;
        cout << "Data " << target << " dihapus.\n";
        delete current;
    }
}
void updateData(int oldData, int newData) {
    Node* current = head;
    while (current != nullptr && current->data != oldData)
        current = current->next;

    if (current == nullptr) {
        cout << "Data " << oldData << " tidak ditemukan.\n";
        return;
    }

    current->data = newData;
    cout << "Data " << oldData << " diubah menjadi " << newData << ".\n";
}
void tampilDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari depan): ";
    Node* current = head;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->next;
    }
    cout << "\n";
}

// ====================================
// Fungsi: Tampilkan dari belakang
// ====================================
void tampilBelakang() {
    if (tail == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari belakang): ";
    Node* current = tail;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->prev;
    }
    cout << "\n";
}

// ====================================
// MAIN PROGRAM (MENU INTERAKTIF)
// ====================================
int main() {
    int pilihan, data, target, oldData, newData;

    do {
        cout << "\n===== MENU DOUBLE LINKED LIST =====\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah Data\n";
        cout << "4. Hapus Depan\n";
        cout << "5. Hapus Belakang\n";
        cout << "6. Hapus Data Tertentu\n";
        cout << "7. Update Data\n";
        cout << "8. Tampil dari Depan\n";
        cout << "9. Tampil dari Belakang\n";
        cout << "0. Keluar\n";
        cout << "===================================\n";
        cout << "Pilih menu: ";
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
                cin >> data;
                insertSetelah(target, data);
                break;
            case 4:
                hapusDepan();
                break;
            case 5:
                hapusBelakang();
                break;
            case 6:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> target;
                hapusData(target);
                break;
            case 7:
                cout << "Masukkan data lama: ";
                cin >> oldData;
                cout << "Masukkan data baru: ";
                cin >> newData;
                updateData(oldData, newData);
                break;
            case 8:
                tampilDepan();
                break;
            case 9:
                tampilBelakang();
                break;
            case 0:
                cout << "👋 Keluar dari program.\n";
                break;
            default:
                cout << "Pilihan tidak valid.\n";
        }

    } while (pilihan != 0);

    return 0;
}

```

## Unguide

### Soal 1
Buatlah ADT Doubly Linked list sebagai berikut di dalam file “Doublylist.h”:
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
> ![Screenshot bagian x](Output/week4_no1.jpg)

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
> ![Screenshot bagian x](Output/week4_no2.jpg)

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


