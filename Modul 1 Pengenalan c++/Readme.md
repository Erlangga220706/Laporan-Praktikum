# <h1 align="center">Laporan Praktikum Modul 1 <br> Pengenalan c++ </h1>
<p align="center"> RADITHIA ERLANGGA - 103112400096 </p>

## Dasar Teori
C++ adalah bahasa pemrograman turunan dari C yang cepat, efisien, dan mendukung OOP. Struktur dasarnya terdiri dari library, fungsi main(), serta perintah. Ia menyediakan tipe data, input-output dengan cin dan cout, logika melalui if-else dan perulangan, serta fungsi dan class untuk membuat kode lebih rapi dan kompleks. Dengan dasar ini, C++ dapat digunakan untuk program sederhana hingga aplikasi besar.

### Soal 1

copy paste soal nomor 1 disini

```go
#include <iostream>
using namespace std;

int main() {
    float bil1, bil2;

    cout << "Masukkan bilangan pertama: ";
    cin >> bil1;
    cout << "Masukkan bilangan kedua : ";
    cin >> bil2;

    cout << "\n=== Hasil Operasi Aritmatika ===" << endl;
    cout << "Penjumlahan : " << bil1 + bil2 << endl;
    cout << "Pengurangan : " << bil1 - bil2 << endl;
    cout << "Perkalian   : " << bil1 * bil2 << endl;

    if (bil2 != 0) {
        cout << "Pembagian   : " << bil1 / bil2 << endl;
    } else {
        cout << "Pembagian   : Tidak bisa (pembagi = 0)" << endl;
    }

    return 0;
}

```

> Output
> ![Screenshot bagian x](Output/no1.jpg)
> %% Untuk mencantumkan screenshot, tidak boleh ada spasi di urlnya `()`, penamaan file bebas asal gak sara dan mudah dipahami aja,, dan jangan lupa hapus komen ini yah%%

Penjelasan ttg kode kalian disini

### Soal 2

soal nomor 2A

```go
#include <iostream>
using namespace std;

string angkaKeTulisan(int n) {
    string satuan[] = {"nol", "satu", "dua", "tiga", "empat", "lima",
                       "enam", "tujuh", "delapan", "sembilan", "sepuluh",
                       "sebelas", "dua belas", "tiga belas", "empat belas",
                       "lima belas", "enam belas", "tujuh belas", "delapan belas", "sembilan belas"};
                       
    string puluhan[] = {"", "", "dua puluh", "tiga puluh", "empat puluh",
                        "lima puluh", "enam puluh", "tujuh puluh", "delapan puluh", "sembilan puluh"};

    if (n < 20) {
        return satuan[n];
    } else if (n < 100) {
        int p = n / 10;
        int s = n % 10;
        if (s == 0) return puluhan[p];
        else return puluhan[p] + " " + satuan[s];
    } else if (n == 100) {
        return "seratus";
    } else {
        return "angka di luar jangkauan";
    }
}

int main() {
    int angka;
    cout << "Masukkan angka (0 - 100): ";
    cin >> angka;

    cout << angka << " : " << angkaKeTulisan(angka) << endl;

    return 0;
}

```
> Output
> ![Screenshot bagian x](Output/no2.jpg)
Buat array kata angka → ada satuan (0–19) dan puluhan (20, 30, dst.). Tujuannya biar gampang ngambil kata sesuai angka.
Cek kondisi angka:
Kalau < 20 langsung ambil dari array satuan.
Kalau 20–99, ambil kata dari puluhan terus ditambah kata dari satuan kalau ada sisa satuannya.
Kalau 100, langsung tulis "seratus".
Main function → minta input dari user, terus panggil fungsi angkaKeTulisan() buat ubah angka ke tulisan.
Output → tampilkan angka asli dan tulisannya (contoh: 79 : tujuh puluh sembilan).


```go
package main

func main() {
	fmt.Println("kode untuk soal nomor 2B")
}
```

> Output
> ![Screenshot bagian x](output/screenshot_soal2B.png)

penjelasan bedanya sesuai soal

## Referensi

1. https://en.wikipedia.org/wiki/Data_structure (diakses blablabla)

