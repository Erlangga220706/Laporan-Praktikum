# <h1 align="center">Laporan Praktikum Modul 13 Multi Linked List</h1>
<p align="center">Radithia Erlangga - 103112400096</p>

## Dasar Teori
Multi linked list adalah struktur data yang menggunakan lebih dari satu pointer pada setiap node sehingga satu node dapat terhubung ke beberapa arah atau level sekaligus. Berbeda dengan single linked list yang hanya memiliki pointer berikutnya (next), pada multi linked list biasanya terdapat pointer tambahan seperti next, down, atau child sehingga data dapat direpresentasikan dalam bentuk hierarki atau kategori bertingkat. Struktur ini cocok digunakan ketika data memiliki hubungan bercabang, seperti daftar fakultas → jurusan → kelas → mahasiswa, sehingga memudahkan organisasi dan traversing data yang tidak bersifat linear saja.
## Guide
```
#include <iostream>
#include <string>
using namespace std;

struct ChildNode
{
    string info;
    ChildNode *next;
};

struct ParentNode
{
    string info;
    ChildNode *childHead;
    ParentNode *next;
};

ParentNode *createParent(string info)
{
    ParentNode *newNode = new ParentNode;
    newNode->info = info;
    newNode->childHead = NULL;
    newNode->next = NULL;
    return newNode;
}

ChildNode *createChild(string info)
{
    ChildNode *newNode = new ChildNode;
    newNode->info = info;
    newNode->next = NULL;
    return newNode;
}

void insertParent(ParentNode *&head, string info)
{
    ParentNode *newNode = createParent(info);
    if (head == NULL)
    {
        head = newNode;
    }
    else
    {
        ParentNode *temp = head;
        while (temp->next != NULL)
        {
            temp = temp->next;
        }
        temp->next = newNode;
    }
}

void insertChild(ParentNode *head, string parentInfo, string childInfo)
{
    ParentNode *p = head;
    while (p != NULL && p->info != parentInfo)
    {
        p = p->next;
    }

    if (p != NULL)
    {
        ChildNode *newChild = createChild(childInfo);
        if (p->childHead == NULL)
        {
            p->childHead = newChild;
        }
        else 
        {
            ChildNode *c = p->childHead;
            while (c->next != NULL)
            {
                c = c->next;
            }
            c->next = newChild;
        }
    }
}

void printAll(ParentNode *head)
{
    ParentNode *p = head;
    while (p != NULL)
    {
        cout << p->info;
        ChildNode *c = p->childHead;
        if (c != NULL)
        {
            while (c != NULL)
            {
                cout << " -> " << c->info;
                c = c->next;
            }
        }
        cout << endl;
        p = p->next;
    }
}

int main()
{
    ParentNode *list = NULL;

    insertParent(list, "Parent Node 1");
    insertParent(list, "Parent Node 2");

    insertChild(list, "Parent Node 1", "Child Node A");
    insertChild(list, "Parent Node 1", "Child Node B");
    insertChild(list, "Parent Node 2", "Child Node C");

    printAll(list);

    return 0;
}
```

## Unguide

### Soal 1
>  ![Screenshot bagian x](Output/soalwan.jpg)
## bstree.h
```go
#ifndef BSTREE_H
#define BSTREE_H

typedef int infotype;

struct Node {
    infotype info;
    Node* left;
    Node* right;
};

typedef Node* address;

address alokasi(infotype x);
void insertNode(address &root, infotype x);
address findNode(infotype x, address root);
void printInOrder(address root);

#endif
```
## bstree.cpp
```go
#include "bstree.h"
#include <iostream>
using namespace std;

// fungsi alokasi
address alokasi(infotype x) {
    address p = new Node;
    p->info = x;
    p->left = NULL;
    p->right = NULL;
    return p;
}

// prosedur insertNode (BST)
void insertNode(address &root, infotype x) {
    if (root == NULL) {
        root = alokasi(x);
    } else {
        if (x < root->info) {
            insertNode(root->left, x);
        } else if (x > root->info) {
            insertNode(root->right, x);
        }
    }
}

// function findNode
address findNode(infotype x, address root) {
    if (root == NULL) return NULL;
    else if (x == root->info) return root;
    else if (x < root->info) return findNode(x, root->left);
    else return findNode(x, root->right);
}

// prosedur printInOrder
void printInOrder(address root) {
    if (root != NULL) {
        printInOrder(root->left);
        cout << root->info << " ";
        printInOrder(root->right);
    }
}
```
## main.cpp
```go
#include <iostream>
#include "bstree.h"

using namespace std;

int main() {
    cout << "Hello World!" << endl;

    address root = NULL;

    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 7);

    printInOrder(root);

    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/jb1.jpg)
Program di atas membuat Binary Search Tree (BST).
Setiap angka dimasukkan ke tree:
kalau lebih kecil masuk ke kiri,
kalau lebih besar masuk ke kanan.
Setelah semua angka dimasukkan, program mencetak tree dengan cara in-order, sehingga hasilnya muncul urut:
1 2 3 4 5 6 7
Itu saja inti kerjanya.
### Soal 2
> ![Screenshot bagian x](Output/soaltu.jpg)

## main.cpp
```go
#include <iostream>
using namespace std;

struct Node {
    int info;
    Node *left, *right;
};

typedef Node* address;

/*================= FUNGSI INSERT =================*/
void insertNode(address &root, int x) {
    if (root == NULL) {
        root = new Node;
        root->info = x;
        root->left = root->right = NULL;
    } else if (x < root->info) {
        insertNode(root->left, x);
    } else {
        insertNode(root->right, x);
    }
}

/*================= TRAVERSAL =================*/
void InOrder(address root) {
    if (root != NULL) {
        InOrder(root->left);
        cout << root->info << " - ";
        InOrder(root->right);
    }
}

/*================= 1. hitungJumlahNode =================*/
// mengembalikan jumlah node dalam BST
int hitungJumlahNode(address root) {
    if (root == NULL) return 0;
    return 1 + hitungJumlahNode(root->left) + hitungJumlahNode(root->right);
}

/*================= 2. hitungTotalInfo =================*/
// mengembalikan total penjumlahan semua info node
int hitungTotalInfo(address root) {
    if (root == NULL) return 0;
    return root->info + hitungTotalInfo(root->left) + hitungTotalInfo(root->right);
}

/*================= 3. hitungKedalaman =================*/
// mengembalikan kedalaman maksimal pohon
int hitungKedalaman(address root) {
    if (root == NULL) return 0;
    int L = hitungKedalaman(root->left);
    int R = hitungKedalaman(root->right);
    return 1 + (L > R ? L : R);
}

/*================= MAIN =================*/
int main() {
    cout << "Hello World" << endl;

    address root = NULL;

    insertNode(root,1);
    insertNode(root,2);
    insertNode(root,6);
    insertNode(root,4);
    insertNode(root,5);
    insertNode(root,3);
    insertNode(root,7);

    InOrder(root);

    cout << "\n\n";
    cout << "kedalaman : " << hitungKedalaman(root) << endl;
    cout << "jumlah node : " << hitungJumlahNode(root) << endl;
    cout << "total : " << hitungTotalInfo(root) << endl;

    return 0;
}

```
> Output
> ![Screenshot bagian x](Output/jb2.jpg)
insertNode() → memasukkan angka ke BST.
hitungJumlahNode() → menghitung berapa banyak node dengan cara rekursif.
hitungTotalInfo() → menjumlahkan semua nilai node.
hitungKedalaman() → mencari kedalaman maksimal pohon.
InOrder() → mencetak node BST secara terurut.

### Soal 3
> ![Screenshot bagian x](Output/soaltre.jpg)
## main.cpp
```go
#include <iostream>
using namespace std;

struct Node {
    int info;
    Node *left, *right;
};

typedef Node* address;

/*=========== INSERT (Sesuai BST) ===========*/
void insertNode(address &root, int x) {
    if (root == NULL) {
        root = new Node;
        root->info = x;
        root->left = root->right = NULL;
    } 
    else if (x < root->info)
        insertNode(root->left, x);
    else
        insertNode(root->right, x);
}

/*=========== PRE-ORDER ===========*/
// Root - Left - Right
void preOrder(address root) {
    if (root != NULL) {
        cout << root->info << " ";
        preOrder(root->left);
        preOrder(root->right);
    }
}

/*=========== POST-ORDER ===========*/
// Left - Right - Root
void postOrder(address root) {
    if (root != NULL) {
        postOrder(root->left);
        postOrder(root->right);
        cout << root->info << " ";
    }
}

/*=========== MAIN PROGRAM ===========*/
int main() {
    address root = NULL;

    // memasukkan data sesuai gambar
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 7);
    insertNode(root, 2);
    insertNode(root, 5);
    insertNode(root, 1);
    insertNode(root, 3);

    cout << "Pre-Order   : ";
    preOrder(root);

    cout << "\nPost-Order  : ";
    postOrder(root);

    cout << endl;
    return 0;
}

```
> Output
> ![Screenshot bagian x](Output/jb3.jpg)
Program ini membuat sebuah Binary Search Tree (BST) memakai struct Node yang memiliki nilai serta pointer ke anak kiri dan kanan, kemudian data dimasukkan menggunakan fungsi insertNode sehingga bentuk tree sesuai dengan gambar soal; setelah tree terbentuk, program mencetak urutan node menggunakan dua jenis traversal, yaitu pre-order (Root–Left–Right) yang menghasilkan output 6 4 2 1 3 5 7, dan post-order (Left–Right–Root) yang menghasilkan 1 3 2 5 4 7 6, sehingga program ini menunjukkan cara membaca struktur tree dari dua arah berbeda sesuai permintaan soal.


## Referensi
1.https://www.geeksforgeeks.org/binary-tree-data-structure/
2.https://www.geeksforgeeks.org/binary-search-tree-data-structure/
3.https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/
4.https://www.javatpoint.com/binary-search-tree
5.https://www.w3schools.com/dsa/dsa_data_trees.php





