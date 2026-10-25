# <h1 align="center">Laporan Praktikum Modul 3 - ABSTRACT DATA TYPE (ADT) DAN PEMROGRAMAN MODULAR PADA C++
<p align="center">Assyifa Zahra - 109082500196</p>

## Dasar Teori
Abstract Data Type (ADT) merupakan model pemrosesan data yang mendefinisikan tipe data beserta operasi-operasinya secara abstrak tanpa bergantung pada detail implementasi teknisnya [1]. Pada bahasa C++, ADT direalisasikan melalui pemrograman modular dengan memanfaatkan struct serta memisahkan komponen program ke dalam file header (.h), file implementasi (.cpp), dan file utama (mainpelajaran.cpp) [1], [2]. Pendekatan ini bertujuan untuk meningkatkan keterbacaan kode, mempermudah pemeliharaan program, dan memungkinkan seluruh file terkait dikompilasi secara bersamaan menggunakan perintah g++ pada terminal [2], [3].
## Guided
### mahasiswa.cpp
```
#include <iostream>
#include "mahasiswa.h"

using namespace std;

void inputMhs(mahasiswa &m) {
    cout << "input nim = ";
    cin >> (m).nim;
    cout << "input nilai = ";
    cin >> (m).nilai1;
    cout << "input nilai2 = ";
    cin >> (m).nilai2;
} 

float rata2(mahasiswa m) {
    return float(m.nilai1+m.nilai2)/2;
}
```
File ini berfungsi sebagai wadah untuk mendefinisikan struktur data serta deklarasi fungsi yang akan digunakan di dalam program secara keseluruhan. Di bagian awal, terdapat baris pengaman yang mencegah terjadinya pemanggilan file header secara berulang saat proses kompilasi. Di dalam file ini juga didefinisikan sebuah struct bernama mahasiswa yang menampung atribut penting seperti NIM berupa array karakter serta dua variabel bilangan bulat untuk menyimpan nilai ujian. Selain itu, terdapat deklarasi fungsi untuk proses input data dan perhitungan nilai rata-rata tanpa menyertakan blok kode isinya secara langsung.
### mahasiswa.h
```
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED
struct mahasiswa{
    char nim[15];
    int nilai1, nilai2;
};

void inputMhs (mahasiswa &m) ;
float rata2 (mahasiswa m) ;
#endif // MAHASISWA_H_INCLUDED
```
File ini berisi penjabaran lengkap mengenai blok kode dan logika dari fungsi-fungsi yang sebelumnya sudah dideklarasikan di dalam file header. Fungsi pertama bertugas untuk meminta masukan data dari pengguna berupa NIM dan dua buah nilai melalui keyboard, di mana penggunaan tanda referensi memastikan bahwa data yang dimasukkan langsung tersimpan pada memori objek yang bersangkutan. Sementara itu, fungsi kedua bertugas mengolah data nilai yang telah dimasukkan dengan menjumlahkannya lalu membaginya dengan angka dua, serta mengonversi hasilnya ke dalam bentuk desimal agar perhitungan nilai rata-rata menjadi lebih akurat.

### main.cpp
```
#include <iostream>
#include "mahasiswa.h"

using namespace std;

int main()
{
    mahasiswa mhs;
    inputMhs (mhs) ;
    cout << "rata-rata = " << rata2 (mhs) ;
    return 0;
}
```
File ini merupakan pusat dari program yang mengatur alur jalannya eksekusi aplikasi secara keseluruhan. Di dalam fungsi utamanya, program mendeklarasikan sebuah variabel objek berbasis struct mahasiswa untuk menampung data yang akan diproses. Selanjutnya, program memanggil prosedur input untuk mulai meminta data dari pengguna, lalu mencetak hasil akhir perhitungan rata-rata ke layar dengan memanfaatkan fungsi pengolahan data yang sudah disiapkan sebelum akhirnya program ditutup dan mengembalikan nilai sukses

<br>

## Unguided

### 1. Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI dengan rumus 0.3*uts+0.4*uas+0.3*tugas. 
```
#ifndef PELAJARAN_H_INCLUDED
#define PELAJARAN_H_INCLUDED

#include <iostream>
#include <string>

using namespace std;

struct pelajaran {
    string namaMapel;
    string kodeMapel;
};

pelajaran create_pelajaran(string namatapel, string kodepel);
void tampil_pelajaran(pelajaran pel);

#endif // PELAJARAN_H_INCLUDED
```
File header ini diawali dengan perintah pengaman kompilasi untuk mencegah terjadinya pendefinisian ganda saat file dipanggil berulang kali, yang kemudian diikuti dengan penyertaan pustaka dasar C++ untuk menangani fungsi standar dan tipe data teks string. Di dalamnya, didefinisikan sebuah struktur data bernama pelajaran yang membungkus dua atribut penting, yaitu nama mata pelajaran dan kode pelajarannya. Selain itu, file ini juga memuat deklarasi fungsi pembuatan objek pelajaran serta prosedur untuk menampilkan data ke layar tanpa menuliskan isi kodenya secara langsung di sini.

### 2. Buatlah ADT pelajaran sebagai berikut di dalam file “pelajaran.h”: 
### Type pelajaran <  namaMapel : string  kodeMapel : string >  function create_pelajaran( namapel : string,     kodepel : string ) → pelajaran procedure tampil_pelajaran( input pel : pelajaran ) 
```
#include "pelajaran.h"

pelajaran create_pelajaran(string namatapel, string kodepel) {
    pelajaran pel;
    pel.namaMapel = namatapel;
    pel.kodeMapel = kodepel;
    return pel;
}

void tampil_pelajaran(pelajaran pel) {
    cout << "nama pelajaran : " << pel.namaMapel << endl;
    cout << "nilai : " << pel.kodeMapel << endl;
}
```
File implementasi ini diawali dengan menyertakan file header pelajaran.h agar compiler mengenali struktur dan fungsi yang akan dijabarkan kodenya. Di bagian dalam, terdapat penjabaran fungsi pembuatan pelajaran yang bertugas menyiapkan variabel penampung sementara, mengisi atribut nama dan kode mata pelajaran sesuai parameter yang dikirimkan, lalu mengembalikan objek tersebut. Berdampingan dengan fungsi tersebut, terdapat pula prosedur pencetakan data yang bertugas menampilkan label teks beserta isi informasi mata pelajaran ke layar konsol secara rapi.

### 3. Buatlah program dengan ketentuan : 
### - 2 buah array 2D integer berukuran 3x3 dan 2 buah pointer integer 
### - fungsi/prosedur yang menampilkan isi sebuah array integer 2D 
### - fungsi/prosedur yang akan menukarkan isi dari 2 array integer 2D pada posisi tertentu - fungsi/prosedur yang akan menukarkan isi dari variabel yang ditunjuk oleh 2 buah pointer 
```
#include <iostream>
#include "pelajaran.h"

using namespace std;

int main() {
    string namatapel = "Struktur Data";
    string kodepel = "STD";
    pelajaran pel = create_pelajaran(namatapel, kodepel);
    tampil_pelajaran(pel);
    
    return 0;
}
```
File utama ini berfungsi sebagai pusat pengendali jalannya program secara keseluruhan dengan menyertakan pustaka input-output serta file header pelajaran yang telah dibuat sebelumnya. Di dalam fungsi utamanya, program mendeklarasikan variabel teks lokal untuk menampung data nama mata pelajaran beserta kodenya. Selanjutnya, program memanggil fungsi khusus pembuat pelajaran untuk mengemas data teks tersebut ke dalam objek, menjalankan prosedur pencetakan untuk menampilkan hasilnya ke layar, dan mengakhiri eksekusi program dengan mengembalikan nilai sukses.

### Output Unguided
![Output Modul 3](https://raw.githubusercontent.com/chypiez/Laporan-Praktikum-Struktur-Data/dc27269fc0b7ede896dc978ca7a19a4f628bf899/Output%20Modul%203.png)
Gambar tersebut memperlihatkan aktivitas di dalam terminal PowerShell Visual Studio Code saat proses kompilasi dan eksekusi program C++ modular untuk materi ADT Pelajaran. Pada baris pertama, terdapat perintah untuk menggabungkan dan mengkompilasi file mainpelajaran.cpp dan pelajaran.cpp menjadi satu file siap jalan bernama program_pelajaran. Selanjutnya, program tersebut dijalankan di terminal dengan perintah eksekusi Windows, yang kemudian menampilkan hasil keluaran berupa teks nama mata pelajaran dan nilai atau kodenya secara sukses. Baris terakhir turut menampilkan pengujian alternatif untuk menjalankan file eksekutable yang sama dengan hasil cetak data yang identik.

## Kesimpulan
Praktikum ini mempelajari konsep Abstract Data Type (ADT) serta penerapan teknik pemrograman modular pada bahasa C++ yang memisahkan struktur data dan fungsi ke dalam file header (.h), file implementasi (.cpp), dan file utama eksekusi (.cpp). Melalui pemisahan ini, struktur program menjadi lebih terorganisir, mudah dibaca, serta mempermudah proses pemeliharaan kode (maintenance). Selain itu, pemahaman mengenai proses kompilasi manual menggunakan perintah g++ di terminal membuktikan bahwa file-file terpisah tersebut dapat digabungkan secara efektif menjadi satu kesatuan program siap jalan (executable) yang menghasilkan keluaran sesuai dengan perancangan logika yang diinginkan.
## Referensi

[1] / (Stroustrup, 2013)

Stroustrup, B. (2013). The C++ Programming Language (4th ed.). Addison-Wesley.

[2] / (Malik, 2018)

Malik, D. S. (2018). C++ Programming: From Problem Analysis to Program Design (8th ed.). Cengage Learning.