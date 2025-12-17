# <h1 align="center">Laporan Praktikum Modul 14 GRAPH</h1>
<p align="center">Radithia Erlangga - 103112400096</p>

## Dasar Teori
Graph merupakan himpunan tidak kosong dari node (vertec) dan garis penghubung (edge). Contoh sederhana tentang graph, yaitu antara Tempat Kost Anda dengan Common Lab. Tempat Kost Anda
dan Common Lab merupakan node (vertec). Jalan yang menghubungkan tempat Kost dan Common Lab merupakan garis penghubung antara keduanya (edge).
## Guide
## graph.h
```go
#ifndef GRAF_H_INCLUDED
#define GRAF_H_INCLUDED

#include <iostream>
using namespace std;

typedef char infoGraph;

struct ElmNode;
struct ElmEdge;

typedef ElmNode *adrNode;
typedef ElmEdge *adrEdge;

struct ElmNode
{
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode next;
};

struct ElmEdge
{
    adrNode node;
    adrEdge next;
};

struct Graph
{
    adrNode first;
};

// PRIMITIF GRAPH
void CreateGraph(Graph &G);
adrNode AllocateNode(infoGraph X);
adrEdge AllocateEdge(adrNode N);

void InsertNode(Graph &G, infoGraph X);
adrNode FindNode(Graph G, infoGraph X);

void ConnectNode(Graph &G, infoGraph A, infoGraph B);

void PrintInfoGraph(Graph G);

// Traversal
void ResetVisited(Graph &G);
void PrintDFS(Graph &G, adrNode N);
void PrintBFS(Graph &G, adrNode N);

#endif


```
## graph.cpp
```go
#include "graf.h"
#include <queue>
#include <stack>

void CreateGraph(Graph &G)
{
    G.first = NULL;
}

adrNode AllocateNode(infoGraph X)
{
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;
    P->firstEdge = NULL;
    P->next = NULL;
    return P;
}

adrEdge AllocateEdge(adrNode N)
{
    adrEdge P = new ElmEdge;
    P->node = N;
    P->next = NULL;
    return P;
}

void InsertNode(Graph &G, infoGraph X)
{
    adrNode P = AllocateNode(X);
    P->next = G.first;
    G.first = P;
}

adrNode FindNode(Graph G, infoGraph X)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        if (P->info == X)
            return P;
        P = P->next;
    }
    return NULL;
}

void ConnectNode(Graph &G, infoGraph A, infoGraph B)
{
    adrNode N1 = FindNode(G, A);
    adrNode N2 = FindNode(G, B);

    if (N1 == NULL || N2 == NULL)
    {
        cout << "Node tidak ditemukan!\n";
        return;
    }

    // Buat edge dari N1 ke N2
    adrEdge E1 = AllocateEdge(N2);
    E1->next = N1->firstEdge;
    N1->firstEdge = E1;

    // Karena undirected → buat edge balik
    adrEdge E2 = AllocateEdge(N1);
    E2->next = N2->firstEdge;
    N2->firstEdge = E2;
}

void PrintInfoGraph(Graph G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        cout << P->info << " -> ";
        adrEdge E = P->firstEdge;
        while (E != NULL)
        {
            cout << E->node->info << " ";
            E = E->next;
        }
        cout << endl;
        P = P->next;
    }
}

void ResetVisited(Graph &G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        P->visited = 0;
        P = P->next;
    }
}

void PrintDFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    N->visited = 1;
    cout << N->info << " ";

    adrEdge E = N->firstEdge;
    while (E != NULL)
    {
        if (E->node->visited == 0)
        {
            PrintDFS(G, E->node);
        }
        E = E->next;
    }
}

void PrintBFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    queue<adrNode> Q;
    Q.push(N);

    while (!Q.empty())
    {
        adrNode curr = Q.front();
        Q.pop();

        if (curr->visited == 0)
        {
            curr->visited = 1;
            cout << curr->info << " ";

            adrEdge E = curr->firstEdge;
            while (E != NULL)
            {
                if (E->node->visited == 0)
                {
                    Q.push(E->node);
                }
                E = E->next;
            }
        }
    }
}

```
## main.cpp
```go
#include "graf.h"
#include "graf.cpp"
#include <iostream>
using namespace std;

int main()
{
    Graph G;
    CreateGraph(G);

    // Tambah node
    InsertNode(G, 'A');
    InsertNode(G, 'B');
    InsertNode(G, 'C');
    InsertNode(G, 'D');
    InsertNode(G, 'E');

    // Hubungkan node (graph tidak berarah)
    ConnectNode(G, 'A', 'B');
    ConnectNode(G, 'A', 'C');
    ConnectNode(G, 'B', 'D');
    ConnectNode(G, 'C', 'E');

    cout << "=== Struktur Graph ===\n";
    PrintInfoGraph(G);

    cout << "\n=== DFS dari Node A ===\n";
    ResetVisited(G);
    PrintDFS(G, FindNode(G, 'A'));

    cout << "\n\n=== BFS dari Node A ===\n";
    ResetVisited(G);
    PrintBFS(G, FindNode(G, 'A'));

    cout << endl;
    return 0;
}
```
## Unguide

### Soal 1
>  ![Screenshot bagian x](Output/soal.jpg)
## graph.h
```go
#ifndef GRAPH_H
#define GRAPH_H

typedef char infoGraph;

typedef struct ElmEdge *adrEdge;
typedef struct ElmNode *adrNode;

struct ElmEdge {
    adrNode node;
    adrEdge next;
};

struct ElmNode {
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode next;
};

struct Graph {
    adrNode first;
};

// Prosedur
void CreateGraph(Graph &G);
adrNode InsertNode(Graph &G, infoGraph X);
void ConnectNode(adrNode N1, adrNode N2);
void PrintInfoGraph(Graph G);

#endif


```
## graph.cpp
```go
#include <iostream>
#include "graph.h"
using namespace std;

void CreateGraph(Graph &G) {
    G.first = NULL;
}

adrNode InsertNode(Graph &G, infoGraph X) {
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;
    P->firstEdge = NULL;
    P->next = NULL;

    if (G.first == NULL) {
        G.first = P;
    } else {
        adrNode Q = G.first;
        while (Q->next != NULL) {
            Q = Q->next;
        }
        Q->next = P;
    }
    return P;
}

void ConnectNode(adrNode N1, adrNode N2) {
    adrEdge E = new ElmEdge;
    E->node = N2;
    E->next = NULL;

    if (N1->firstEdge == NULL) {
        N1->firstEdge = E;
    } else {
        adrEdge T = N1->firstEdge;
        while (T->next != NULL) {
            T = T->next;
        }
        T->next = E;
    }
}

void PrintInfoGraph(Graph G) {
    adrNode N = G.first;
    while (N != NULL) {
        cout << N->info << " : ";
        adrEdge E = N->firstEdge;
        while (E != NULL) {
            cout << E->node->info << " ";
            E = E->next;
        }
        cout << endl;
        N = N->next;
    }
}

```
## main.cpp
```go
#include <iostream>
#include "graph.h"
using namespace std;

int main() {
    Graph G;
    CreateGraph(G);

    // Insert Node
    adrNode A = InsertNode(G, 'A');
    adrNode B = InsertNode(G, 'B');
    adrNode C = InsertNode(G, 'C');
    adrNode D = InsertNode(G, 'D');
    adrNode E = InsertNode(G, 'E');
    adrNode F = InsertNode(G, 'F');
    adrNode Gg = InsertNode(G, 'G');
    adrNode H = InsertNode(G, 'H');

    // Connect sesuai gambar
    ConnectNode(A, B);
    ConnectNode(A, C);

    ConnectNode(B, D);
    ConnectNode(B, E);

    ConnectNode(C, F);
    ConnectNode(C, Gg);

    ConnectNode(E, H);
    ConnectNode(F, H);
    ConnectNode(Gg, H);

    // Print Graph
    cout << "=== Representasi Graph ===" << endl;
    PrintInfoGraph(G);

    return 0;
}

```

> Output
> ![Screenshot bagian x](Output/ssno1.jpg)
InsertNode → menambahkan simpul (vertex).
ConnectNode → membuat edge (hubungan) dari satu node ke node lain.
PrintInfoGraph → menampilkan adjacency list.
### Soal 2
Buatlah prosedur untuk menampilkanhasil penelusuran DFS. prosedur PrintDFS (Graph G, adrNode N);

## graph.h
```go
#ifndef GRAPH_H
#define GRAPH_H

typedef char infoGraph;

typedef struct ElmEdge *adrEdge;
typedef struct ElmNode *adrNode;

struct ElmEdge {
    adrNode node;
    adrEdge next;
};

struct ElmNode {
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode next;
};

struct Graph {
    adrNode first;
};

void CreateGraph(Graph &G);
adrNode InsertNode(Graph &G, infoGraph X);
void ConnectNode(adrNode N1, adrNode N2);
void PrintInfoGraph(Graph G);

// nomor 2
void PrintDFS(Graph &G, adrNode N);
void resetVisited(Graph &G);

#endif

```
## graph.cpp
```go
#include <iostream>
#include "graph.h"
using namespace std;

void CreateGraph(Graph &G) {
    G.first = NULL;
}

adrNode InsertNode(Graph &G, infoGraph X) {
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;
    P->firstEdge = NULL;
    P->next = NULL;

    if (G.first == NULL) {
        G.first = P;
    } else {
        adrNode Q = G.first;
        while (Q->next != NULL) {
            Q = Q->next;
        }
        Q->next = P;
    }
    return P;
}

void ConnectNode(adrNode N1, adrNode N2) {
    adrEdge E = new ElmEdge;
    E->node = N2;
    E->next = NULL;

    if (N1->firstEdge == NULL) {
        N1->firstEdge = E;
    } else {
        adrEdge T = N1->firstEdge;
        while (T->next != NULL) {
            T = T->next;
        }
        T->next = E;
    }
}

void PrintInfoGraph(Graph G) {
    adrNode N = G.first;
    while (N != NULL) {
        cout << N->info << " : ";
        adrEdge E = N->firstEdge;
        while (E != NULL) {
            cout << E->node->info << " ";
            E = E->next;
        }
        cout << endl;
        N = N->next;
    }
}

// ---------------------- Nomor 2 (DFS) ---------------------- //

void resetVisited(Graph &G) {
    adrNode P = G.first;
    while (P != NULL) {
        P->visited = 0;
        P = P->next;
    }
}

void PrintDFS(Graph &G, adrNode N) {
    if (N == NULL) return;

    cout << N->info << " ";
    N->visited = 1;

    adrEdge E = N->firstEdge;
    while (E != NULL) {
        if (E->node->visited == 0) {
            PrintDFS(G, E->node);
        }
        E = E->next;
    }
}

```
## main.cpp
```go
#include <iostream>
#include "graph.h"
using namespace std;

int main() {
    Graph G;
    CreateGraph(G);

    // Insert Node sesuai gambar
    adrNode A = InsertNode(G, 'A');
    adrNode B = InsertNode(G, 'B');
    adrNode C = InsertNode(G, 'C');
    adrNode D = InsertNode(G, 'D');
    adrNode E = InsertNode(G, 'E');
    adrNode F = InsertNode(G, 'F');
    adrNode Gg = InsertNode(G, 'G');
    adrNode H = InsertNode(G, 'H');

    // Connect Node sesuai graf
    ConnectNode(A, B);
    ConnectNode(A, C);

    ConnectNode(B, D);
    ConnectNode(B, E);

    ConnectNode(C, F);
    ConnectNode(C, Gg);

    ConnectNode(E, H);
    ConnectNode(F, H);
    ConnectNode(Gg, H);

    cout << "=== Representasi Graph (Adjacency List) ===" << endl;
    PrintInfoGraph(G);

    cout << "\n=== Hasil DFS dimulai dari node A ===" << endl;
    resetVisited(G);
    PrintDFS(G, A);

    cout << endl << endl;
    return 0;
}


```

> Output
> ![Screenshot bagian x](Output/ssno2.jpg)
PrintDFS adalah prosedur penelusuran graf yang dilakukan secara mendalam, yaitu mulai dari simpul awal lalu langsung masuk ke simpul berikutnya terus menerus sampai tidak ada jalur lagi. Setiap simpul yang dikunjungi diberi tanda agar tidak dikunjungi dua kali, kemudian proses dilanjutkan secara rekursif ke tetangga yang belum dikunjungi. Dengan cara ini, DFS menelusuri graf seperti menelusuri jalan sampai ke ujung dulu, baru kembali dan melanjutkan ke jalur lainnya.
### Soal 3
Buatlah prosedur untuk menampilkanhasil penelusuran DFS. prosedur PrintBFS (Graph G, adrNode N);
## main.cpp
```go
#include <iostream>
#include <queue>
using namespace std;

struct Node;
struct Adj {
    Node* node;
    Adj* next;
};

struct Node {
    char info;
    Adj* adj;
    Node* next;
};

struct Graph {
    Node* first;
};

// ------------------- CREATE GRAPH -------------------
void createGraph(Graph &G) {
    G.first = NULL;
}

// ------------------- FIND NODE -------------------
Node* findNode(Graph G, char x) {
    Node* p = G.first;
    while (p != NULL) {
        if (p->info == x) return p;
        p = p->next;
    }
    return NULL;
}

// ------------------- ADD NODE -------------------
void addNode(Graph &G, char x) {
    if(findNode(G, x) != NULL) return; // node sudah ada
    Node* p = new Node;
    p->info = x;
    p->adj = NULL;
    p->next = G.first;
    G.first = p;
}

// ------------------- ADD EDGE -------------------
void addEdge(Graph &G, char src, char dst) {
    Node* p = findNode(G, src);
    Node* q = findNode(G, dst);

    if (p == NULL || q == NULL) {
        cout << "Node tidak ditemukan!\n";
        return;
    }

    Adj* a = new Adj;
    a->node = q;
    a->next = p->adj;
    p->adj = a;
}

// ------------------- PRINT BFS -------------------
void PrintBFS(Graph G, Node* start) {
    if (!start) return;

    bool visited[256] = {false};
    queue<Node*> Q;

    Q.push(start);
    visited[start->info] = true;

    cout << "BFS : ";
    while (!Q.empty()) {
        Node* curr = Q.front(); Q.pop();
        cout << curr->info << " ";

        Adj* a = curr->adj;
        while (a != NULL) {
            if (!visited[a->node->info]) {
                visited[a->node->info] = true;
                Q.push(a->node);
            }
            a = a->next;
        }
    }
    cout << endl;
}

// ------------------- PRINT DFS -------------------
void PrintDFSUtil(Node* n, bool visited[]) {
    if (!n) return;
    visited[n->info] = true;
    cout << n->info << " ";

    Adj* a = n->adj;
    while (a != NULL) {
        if (!visited[a->node->info]) {
            PrintDFSUtil(a->node, visited);
        }
        a = a->next;
    }
}

void PrintDFS(Graph G, Node* start) {
    bool visited[256] = {false};
    cout << "DFS : ";
    PrintDFSUtil(start, visited);
    cout << endl;
}

// ------------------- MAIN -------------------
int main() {
    Graph G;
    createGraph(G);

    // contoh node
    addNode(G, 'A');
    addNode(G, 'B');
    addNode(G, 'C');
    addNode(G, 'D');
    addNode(G, 'E');

    // contoh edge
    addEdge(G, 'A', 'B');
    addEdge(G, 'A', 'C');
    addEdge(G, 'B', 'D');
    addEdge(G, 'C', 'E');

    Node* start = findNode(G, 'A');

    PrintDFS(G, start);
    PrintBFS(G, start);

    return 0;
}

```
> Output
> ![Screenshot bagian x](Output/ssno3.jpg)
PrintBFS adalah prosedur penelusuran graf yang dilakukan secara melebar, yaitu mulai dari simpul awal lalu mengunjungi semua tetangganya terlebih dahulu. BFS menggunakan struktur data queue untuk mengantri simpul yang akan dikunjungi, sehingga simpul yang masuk duluan akan diproses dulu. Dengan cara ini, BFS menelusuri graf berdasarkan urutan tingkat atau level, sehingga semua simpul terdekat dari titik awal akan dikunjungi lebih dulu sebelum lanjut ke simpul lain.

## Referensi
1.https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/
2.https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/
3.https://visualgo.net/en/dfsbfs
4.https://www.programiz.com/dsa/graph-dfs
5.https://www.programiz.com/dsa/graph-bfs





