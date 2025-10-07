# <h1 align="center">Laporan Praktikum Modul 2 <br> Pengenalan C++</h1>
<p align="center">Radithia Erlangga - 103112400096</p>

## Dasar Teori
Call by Reference adalah cara memanggil fungsi di C++ di mana yang dikirim ke fungsi bukan nilai variabel, tetapi alamat memorinya. Dengan menambahkan tanda & pada parameter fungsi, maka fungsi bisa mengakses dan mengubah nilai asli dari variabel yang dikirim.
Berbeda dengan Call by Value yang hanya menyalin nilai, Call by Reference memungkinkan perubahan di dalam fungsi langsung memengaruhi variabel asli. Metode ini lebih efisien karena tidak membuat salinan data dan sering digunakan saat program perlu mengubah nilai variabel secara langsung.
## Guide

## 01_Array
```go
#include <iostream>
using namespace std;

int main() {

    int nilai[5] = {1, 2, 3, 4, 5};

    for ( int i = 0;  i < 5; i++)
    {
       
        cout << "elemen ke-" << i << "=" << nilai[i] << endl;
    }
    return 0;
}
```

## 02_Array
```go
#include <iostream>
using namespace std;

int main() {
    int matrik[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            cout << matrik[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

## 03_pointer
```go
#include <iostream>
using namespace std;

int main()
{
    int umur = 25;
    int *p_umur;

    p_umur = &umur;

    cout << "Nilai 'umur' : " << umur << endl;
    cout << "Alamat memori 'umur' : " << &umur << endl;
    cout << "Nilai 'p_umur' (alamat) : " << p_umur << endl;
    cout << "Nilai yang diakses 'p_umur' : " << *p_umur << endl;
    cout << "Alamat memori dari pointer 'p_umur' itu sendiri : " << &p_umur << endl;

    return 0;
}
```

## 04_array_pointer
```go
#include <iostream>
using namespace std;

int main()
{
    int data[5] = {10, 20, 30, 40, 50};
    int *p_data = data;

    cout << "Mengakses elemen array cara normal:" << endl;

    for (int i = 0; i < 5; ++i)
    {
        cout << "Nilai elemen ke-" << i << " : " << data[i] << endl;
    }

    cout << "Mengakses elemen array menggunakan pointer:" << endl;

    for (int i = 0; i < 5; ++i)
    {
        cout << "Nilai elemen ke-" << i << " : " << *(p_data + i) << endl;
    }

    return 0;
}
```

## 05_string_pointer
```go
#include <iostream>
using namespace std;

int main()
{
    char pesan_array[] = "Nasi Padang";
    char *pesan_pointer = "Ayam Bakar 23";

    cout << "String Array: " << pesan_array << endl;
    cout << "String Pointer: " << pesan_pointer << endl;

    // Mengubah karakter dalam array diperbolehkan
    pesan_array[0] = 'h';
    cout << "String Array setelah diubah: " << pesan_array << endl;

    // Pointer dapat diubah untuk menunjuk ke string lain
    pesan_pointer = "Sariman";
    cout << "String Pointer setelah menunjuk ke string lain: " << pesan_pointer << endl;

    return 0;
}
```

## 06_
```go

```

## 07_call_by_pointer
```go
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(&a, &b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int *px, int *py)
{
    int temp = *px;
    *px = *py;
    *py = temp;
}
```

## 08_call_by_reference
```go
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(a, b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int &x, int &y)
{
    int temp = x;
    x = y;
    y = temp;
}
```


## Unguide

### Soal 1

Buatlah sebuah program untuk melakukan transpose pada sebuah matriks persegi berukuran 3x3. Operasi transpose adalah mengubah baris menjadi kolom dan sebaliknya. Inisialisasi matriks awal di dalam kode, kemudian buat logika untuk melakukan transpose dan simpan hasilnya ke dalam matriks baru. Terakhir, tampilkan matriks awal dan matriks hasil transpose.

Contoh Output:

Matriks Awal:

1 2 3

4 5 6

7 8 9

Matriks Hasil Transpose:

1 4 7

2 5 8

3 6 9

```go
#include <iostream>
using namespace std;

int main() {
    int matriks[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    cout << "Matriks Awal:" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << matriks[i][j] << " ";
        }
        cout << endl;
    }

    for (int i = 0; i < 3; i++) {
        for (int j = i + 1; j < 3; j++) {
            int temp = matriks[i][j];
            matriks[i][j] = matriks[j][i];
            matriks[j][i] = temp;
        }
    }

    cout << endl;

    cout << "Matriks Hasil Transpose:" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << matriks[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}

```
> Output
> ![Screenshot bagian x](Output/week2_no1.jpg)
Pada kode ini, proses transpose dilakukan langsung di dalam matriks yang sama dengan menukar elemen matriks[i][j] dan matriks[j][i]. Dengan cara ini, tidak perlu membuat matriks baru untuk menyimpan hasilnya.

### Soal 2

Buatlah program yang menunjukkan penggunaan call by reference. Buat sebuah prosedur bernama kuadratkan yang menerima satu parameter integer secara referensi (&). Prosedur ini akan mengubah nilai asli variabel yang dilewatkan dengan nilai kuadratnya. Tampilkan nilai variabel di main() sebelum dan sesudah memanggil prosedur untuk membuktikan perubahannya. 

Contoh Output:

Nilai awal: 5
Nilai setelah dikuadratkan: 25

```go
#include <iostream>
using namespace std;

void kuadratkan(int &x) {
    x = x * x; 
}

int main() {
    int angka = 5;

    cout << "Nilai awal: " << angka << endl;

    kuadratkan(angka);

    cout << "Nilai setelah dikuadratkan: " << angka << endl;

    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/week2_no_2.jpg)
Program ini menggunakan call by reference dengan menambahkan tanda & pada parameter fungsi kuadratkan.
Karena variabel dikirim melalui referensi, maka perubahan yang terjadi di dalam fungsi langsung memengaruhi nilai asli di main().
Hasilnya, setelah fungsi dipanggil, nilai angka berubah dari 5 menjadi 25.

## Referensi
1.https://www.geeksforgeeks.org/cpp-functions-pass-by-reference/
2.https://www.programiz.com/cpp-programming/pointers-function
3.https://www.tutorialspoint.com/cplusplus/cpp_function_call_by_reference.htm
4.https://www.geeksforgeeks.org/references-in-cpp/
5.https://www.ibm.com/docs/en/zos/2.4.0?topic=calls-pass-by-reference-c-only
