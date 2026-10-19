# <h1 align="center">Laporan Praktikum Modul 4 - Implementasi Singly Linked List pada C++

## Dasar Teori
Singly Linked List adalah struktur data linier dinamis yang terdiri dari serangkaian node yang saling terhubung menggunakan pointer, di mana setiap node memuat elemen data (info) serta alamat memori penunjuk ke node berikutnya [1]. Berbeda dengan array, struktur ini tidak memerlukan alokasi memori yang bersebelahan (contiguous), sehingga sangat fleksibel untuk operasi penyisipan seperti insertFirst, penghapusan seperti deleteFirst, deleteLast, dan deleteAfter, penelusuran (traversal), hingga perhitungan jumlah elemen melalui fungsi nbList secara dinamis selama program berjalan [2].
## Guided
### list.cpp
```
#include "list.h"
#include <iostream>
using namespace std;

//I.S = Initial State / kondisi awal
//F.S = Final State / kondisi akhir

//fungsi untuk cek apakah list kosong atau tidak
bool isEmpty(linkedList List) {
    if(List.first == Nil){
        return true;
    } else {
        return false;
    }
}

//pembuatan linked list kosong
void createList(linkedList &List) {
    /* I.S. sembarang
       F.S. terbentuk list kosong */
    List.first = Nil;
}

//pembuatan node baru dengan menerapkan manajemen memori
address alokasi(string nama, string nim, int umur) {
    /* I.S. sembarang
       F.S. mengembalikan alamat node baru dengan isidata = sesuai parameter dan next = Nil */
    address nodeBaru = new node;
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.nim = nim;
    nodeBaru->isidata.umur = umur;
    nodeBaru->next = Nil;
    return nodeBaru;
}

//penghapusan node dengan menerapkan manajemen memori
void dealokasi(address &node) {
    /* I.S. P terdefinisi
       F.S. memori yang digunakan node dikembalikan ke sistem */
    node->next = Nil;
    delete node;
}

//prosedur-prosedur untuk insert / menambahkan node baru kedalam list
void insertFirst(linkedList &List, address nodeBaru) {
    /* I.S. sembarang, P sudah dialokasikan
       F.S. menempatkan elemen list (node) pada awal list */
    nodeBaru->next = List.first;
    List.first = nodeBaru;
}

void insertAfter(linkedList &List, address nodeBaru, address Prev) {
    /* I.S. sembarang, nodeBaru dan Prev alamat salah satu elemen list (node)
       F.S. menempatkan elemen (node) sesudah elemen node Prev */
    if (Prev != Nil) {
        nodeBaru->next = Prev->next;
        Prev->next = nodeBaru;
    } else {
        cout << "Node sebelumnya tidak valid!" << endl;
    }
}

void insertLast(linkedList &List, address nodeBaru) {
    /* I.S. sembarang, nodeBaru sudah dialokasikan
       F.S. menempatkan elemen nodeBaru pada akhir list */
    if (isEmpty(List)) {
        List.first = nodeBaru;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu->next != Nil) {
            nodeBantu = nodeBantu->next;
        }
        nodeBantu->next = nodeBaru;
    }
}

//prosedur-prosedur untuk delete / menghapus node yang ada didalam list
void delFirst(linkedList &List){
    /* I.S. list tidak kosong
    F.S. node pertama di list terhapus*/
    address nodeHapus;
    if (isEmpty(List) == false) {
        nodeHapus = List.first;
        List.first = List.first->next;
        nodeHapus->next = Nil;
        dealokasi(nodeHapus);
    } else {
        cout << "List kosong!" << endl;
    }
}

void delLast(linkedList &List){
    /* I.S. list tidak kosong
    F.S. node terakhir di list terhapus */
    address nodeHapus, nodePrev;
    if(isEmpty(List) == false){
        nodeHapus = List.first;
        if(nodeHapus->next == Nil){
            List.first->next = Nil;
            dealokasi(nodeHapus);
        } else {
            while(nodeHapus->next != Nil){
                nodePrev = nodeHapus;
                nodeHapus = nodeHapus->next;
            }
            nodePrev->next = Nil;
            dealokasi(nodeHapus);
        }
    } else {
        cout << "list kosong" << endl;
    }
}

void delAfter(linkedList &List, address nodeHapus, address nodePrev){
    /* I.S. list tidak kosng, Prev alamat salah satu elemen list
    F.S. nodeBantu adalah alamat dari Prev->next, menghapus Prev->next dari list */
    if(isEmpty(List) == true){
        cout << "List kosong!" << endl;
    } else { //jika list tidak kosong
        if (nodePrev != Nil && nodePrev->next != Nil) {
            nodeHapus = nodePrev->next;
            nodePrev->next = nodeHapus->next;
            nodeHapus->next = Nil;
            dealokasi(nodeHapus);
        } else {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}


//prosedur untuk menampilkan isi list
void printList(linkedList List) {
    /* I.S. list mungkin kosong
       F.S. jika list tidak kosong menampilkan semua info yang ada pada list */
    if (isEmpty(List)) {
        cout << "List kosong." << endl;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu != Nil) {
            cout << "Nama : " << nodeBantu->isidata.nama << ", NIM : " << nodeBantu->isidata.nim << ", Usia : " << nodeBantu->isidata.umur << endl;
            nodeBantu = nodeBantu->next;
        }
    }
}

//function untuk menampilkan jumlah node didalam list
int nbList(linkedList List) {
    /* I.S. list sudah ada
       F.S. menampilkan jumlah node didalam list*/
    int count = 0;
    address nodeBantu = List.first;
    while (nodeBantu != Nil) {
        count++;
        nodeBantu = nodeBantu->next;
    }
    return count;
}

//prosedur untuk menghapus list (menghapus semua node didalam list)
void deleteList(linkedList &List){
    /* I.S. list sudah ada
       F.S. menghapus semua node didalam list*/
    address nodeBantu, nodeHapus;
    nodeBantu = List.first;
    while(nodeBantu != Nil){
        nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus);
    }
    List.first = Nil;
    cout << "List sudah terhapus!" << endl;
}
```

Program *linked list* ini diawali dengan fungsi `isEmpty` untuk memeriksa ketersediaan elemen dan `createList` untuk menginisialisasi list kosong dengan menyetel pointer `first` menjadi `Nil`. Untuk pengelolaan datanya, fungsi `alokasi` digunakan untuk memesan memori dinamis bagi node baru yang membawa data nama, NIM, serta umur, sedangkan `dealokasi` bertugas membersihkan memori agar terhindar dari *memory leak*.

Operasi penambahan elemen dibagi menjadi tiga metode utama, yaitu `insertFirst` untuk menyisipkan node di awal, `insertAfter` untuk posisi di antara node berdasarkan acuan `Prev`, serta `insertLast` yang menelusuri list hingga ujung untuk menempatkan data di akhir. Sebaliknya, proses penghapusan data didukung oleh `delFirst` untuk membuang node pertama, `delLast` untuk node terakhir, dan `delAfter` untuk menghapus node yang berada tepat setelah pointer penanda.

Sebagai pelengkap manajemen data, prosedur `printList` melakukan penelusuran (*traversal*) untuk mencetak seluruh informasi mahasiswa yang tersimpan, fungsi `nbList` menghitung total keseluruhan node di dalam list, dan prosedur `deleteList` membersihkan seluruh memori list secara menyeluruh sekaligus mereset pointer utama kembali ke kondisi kosong.

### list.h
```
//hear guard digunakan untuk mencegah file header yg sama
//di-include lebih dari sekali dalam 1 program
#ifndef LIST_H
#define LIST_H
#define Nil NULL

#include<iostream>
using namespace std;

//deklarasi isi data struct mahasiswa
struct mahasiswa {
    string nama;
    string nim;
    int umur;
};

typedef mahasiswa dataMahasiswa; //memberikan nama alias dataMahasiswa untuk struct mahasiswa

typedef struct node *address; //mendefinisikan alias address sebagai pointer ke struct node

struct node { //node untuk isi dari linked listnya, isis setiap node adalah data & pointer next
    dataMahasiswa isidata;
    address next;
};

struct linkedList { //ini linked listnya
    address first;
};

//semua function & prosedur yang akan dipakai
bool isEmpty(linkedList list);
void createList(linkedList &list);
address alokasi(string nama, string nim, int umur);
void dealokasi(address &node);
void printList(linkedList list);
void insertFirst(linkedList &list, address nodeBaru);
void insertAfter(linkedList &list, address nodeBaru, address Prev);
void insertLast(linkedList &list, address nodeBaru);

void delFirst(linkedList &list);
void delLast(linkedList &list);
void delAfter(linkedList &list, address nodeHapus, address nodePrev);
int nbList(linkedList list);
void deleteList(linkedList &list);

#endif
```
Bagian awal kode ini menggunakan *header guard* melalui `#ifndef` dan `#define LIST_H` untuk memastikan file *header* ini tidak dipanggil atau di-*include* berulang kali dalam satu program, sekaligus mendefinisikan konstanta `Nil` sebagai pengganti `NULL`.

Pada bagian struktur data, didefinisikan `struct mahasiswa` untuk menampung informasi data mahasiswa berupa nama, NIM, dan umur, yang kemudian diberi alias `dataMahasiswa`. Selain itu, terdapat `struct node` yang berfungsi sebagai elemen pembentuk *linked list* dengan komponen *isidata* dan pointer *next* bertipe `address`, serta `struct linkedList` yang bertindak sebagai wadah utama dengan pointer `first` sebagai penanda awal list.

Di bagian akhir, seluruh tanda tangan fungsi dan prosedur mulai dari proses inisialisasi, alokasi memori, penambahan, hingga penghapusan elemen dideklarasikan secara lengkap sebagai antarmuka (*interface*) agar dapat diimplementasikan dan dihubungkan dengan file program utama.

### main.cpp
```
#include "list.h"

#include<iostream>
using namespace std;

int main(){
    linkedList List;
    address nodeA, nodeB, nodeC, nodeD, nodeE = Nil;
    createList(List);

    dataMahasiswa mhs;

    nodeA = alokasi("Dhimas", "2311102151", 20);
    nodeB = alokasi("Arvin", "2211110014", 21);
    nodeC = alokasi("Rizal", "2311110029", 20);
    nodeD = alokasi("Satrio", "2211102173", 21);
    nodeE = alokasi("Joshua", "2311102133", 21);

    insertFirst(List, nodeA);
    insertLast(List, nodeB);
    insertAfter(List, nodeC, nodeA);
    insertAfter(List, nodeD, nodeC);
    insertLast(List, nodeE);

    cout << "--- ISI LIST SETELAH DILAKUKAN INSERT ---" << endl;
    printList(List);
    cout << "jumlah node : " << nbList(List) << endl;
    cout << endl;

    delFirst(List);
    delLast(List);
    delAfter(List, nodeD, nodeC);

    cout << "--- ISI LIST SETELAH DILAKUKAN DELETE ---" << endl;
    printList(List);
    cout << "jumlah node : " << nbList(List) << endl;
    cout << endl;

    deleteList(List);
    cout << "--- ISI LIST SETELAH DILAKUKAN HAPUS LIST ---" << endl;
    printList(List);
    cout << "jumlah node : " << nbList(List) << endl;
    cout << endl;

    return 0;
}
```
Fungsi utama (`main`) diawali dengan menginisialisasi variabel `List` dan menyiapkan beberapa pointer node untuk menampung data mahasiswa. Melalui fungsi `alokasi`, data nama, NIM, dan umur dari lima orang mahasiswa dimasukkan ke dalam memori, yang kemudian disusun ke dalam list menggunakan kombinasi fungsi `insertFirst`, `insertLast`, dan `insertAfter` sebelum akhirnya dicetak beserta jumlah total nodenya.

Tahap berikutnya memperlihatkan proses penghapusan elemen menggunakan fungsi `delFirst`, `delLast`, dan `delAfter` untuk mengubah susunan data di dalam list. Setelah operasi penghapusan tersebut selesai, isi list dan jumlah node yang tersisa kembali ditampilkan ke layar untuk melihat perubahan strukturnya.

Sebagai penutup program, fungsi `deleteList` dipanggil untuk membersihkan seluruh memori dari sisa-sisa node yang masih ada. Hal ini dibuktikan dengan hasil akhir cetakan layar yang menunjukkan bahwa list sudah kosong dan jumlah node kembali menjadi nol.

<br>

## Unguided

### 1. Buatlah ADT Singly Linked list sebagai berikut di dalam file “Singlylist.h” 
![Laporan Praktikum Struktur Data](https://github.com/chypiez/Laporan-Praktikum-Struktur-Data/blob/fb554347cc86d232ce99d472edc09d852428d8ba/Soal%201.1.png)

### Kemudian buatlah implementasi dari procedure-procedure yang digunakan didalam file “Singlylist.cpp” 
### Kemudian buat program utama didalam file “main.cpp” dengan implementasi sebagai berikut :
![Laporan Praktikum Struktur Data](https://github.com/chypiez/Laporan-Praktikum-Struktur-Data/blob/fb554347cc86d232ce99d472edc09d852428d8ba/Soal%201.2.png)

### Sehingga linkedlist yang dibuat akan seperti ini : 
![Laporan Praktikum Struktur Data](https://github.com/chypiez/Laporan-Praktikum-Struktur-Data/blob/3ec3c521b553f8c25e7949ad4a89425996117b0e/Soal%201.3.png)

### Singlylist.h
```C++
#ifndef SINGLYLIST_H
#define SINGLYLIST_H
#define Nil NULL

#include <iostream>
using namespace std;

typedef int infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address First;
};

// Deklarasi Prosedur dan Fungsi khusus Soal 1
void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);

#endif
```

File header ini diawali dengan *header guard* menggunakan `#ifndef` dan `#define SINGLYLIST_H` untuk memastikan seluruh deklarasi di dalamnya tidak dipanggil atau di-*include* berulang kali dalam satu program, sekaligus mendefinisikan konstanta `Nil` sebagai pengganti nilai kosong (`NULL`). Pada bagian struktur data, didefinisikan tipe bentukan `ElmList` yang memuat komponen informasi bernilai integer (`info`) serta pointer `next` bertipe `address`, serta struktur `List` yang menampung pointer utama `First` sebagai gerbang awal penelusuran list. Di bagian akhir, seluruh tanda tangan prosedur dan fungsi standar seperti `CreateList`, `alokasi`, `dealokasi`, `printInfo`, dan `insertFirst` dideklarasikan agar dapat diimplementasikan dan dihubungkan secara modular dengan file program utama.

### Singlylist.cpp
```C++
#include "Singlylist.h"

// Membuat list kosong
void CreateList(List &L) {
    L.First = Nil;
}

// Alokasi memori untuk node baru
address alokasi(infotype x) {
    address P = new ElmList;
    if (P != Nil) {
        P->info = x;
        P->next = Nil;
    }
    return P;
}

// Dealokasi memori node
void dealokasi(address &P) {
    delete P;
    P = Nil;
}

// Menampilkan seluruh info dalam list sesuai urutan
void printInfo(List L) {
    address P = L.First;
    while (P != Nil) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

// Menambahkan elemen di awal list
void insertFirst(List &L, address P) {
    P->next = L.First;
    L.First = P;
}
```

File implementasi ini berisi penjabaran logika dari setiap prosedur dan fungsi yang telah dideklarasikan sebelumnya. Prosedur `CreateList` bertugas menginisialisasi list dengan mengeset pointer `First` menjadi `Nil`, sementara fungsi `alokasi` bertanggung jawab memesan memori dinamis menggunakan operator `new` untuk membentuk node baru yang membawa data integer serta menginisialisasi pointer `next`-nya menjadi `Nil`. Di sisi lain, prosedur `dealokasi` membersihkan memori node yang sudah tidak terpakai guna mencegah terjadinya kebocoran memori (*memory leak*). Selain itu, prosedur `printInfo` melakukan penelusuran (*traversal*) dari node awal hingga akhir untuk mencetak seluruh nilai informasi ke layar, dan prosedur `insertFirst` menyisipkan node baru di posisi terdepan list dengan cara mengubah sambungan pointer `First` secara efisien.

### main1.cpp
```C++
#include "Singlylist.h"

int main() {
    List L;
    address P1, P2, P3, P4, P5;
    
    // Inisialisasi List kosong[cite: 2]
    CreateList(L);

    // Alokasi dan insert elemen sesuai urutan pada soal[cite: 2]
    P1 = alokasi(2);
    insertFirst(L, P1);
    
    P2 = alokasi(0);
    insertFirst(L, P2);
    
    P3 = alokasi(8);
    insertFirst(L, P3);
    
    P4 = alokasi(12);
    insertFirst(L, P4);
    
    P5 = alokasi(9);
    insertFirst(L, P5);

    // Menampilkan isi list ke terminal[cite: 2]
    printInfo(L);

    return 0;
}
```
Program utama diawali dengan mendeklarasikan variabel `List L` beserta beberapa variabel pointer `address` yang digunakan untuk menampung alamat node. Melalui pemanggilan fungsi `CreateList(L)`, list diinisialisasi dalam kondisi kosong sebelum akhirnya rangkaian data angka—yakni 2, 0, 8, 12, dan 9—dimasukkan satu per satu ke dalam memori menggunakan kombinasi fungsi `alokasi` dan prosedur `insertFirst`. Karena menggunakan metode penyisipan di awal (*insert first*), nilai yang terakhir dimasukkan akan otomatis berada di posisi paling depan. Sebagai tahap akhir, prosedur `printInfo(L)` dipanggil untuk mencetak seluruh urutan nilai di dalam *linked list* ke layar terminal secara berurutan.

### Output Unguided Soal 1
![Output Soal 1](https://github.com/chypiez/Laporan-Praktikum-Struktur-Data/blob/56662ae174a27524d8be16a8bb6c225b5a503113/Output%20Soal%201.png)
Program di atas berhasil dikompilasi menggunakan perintah `g++ main1.cpp Singlylist.cpp -o program_soal1` untuk menggabungkan file program utama dan implementasi fungsi, lalu dijalankan melalui terminal PowerShell dengan perintah `./program_soal1`. Berdasarkan hasil eksekusi tersebut, terminal memunculkan output berupa deretan angka `9 12 8 0 2`, yang menunjukkan bahwa struktur *Singly Linked List* telah terbentuk dengan sukses di mana nilai-nilai yang dimasukkan menggunakan metode `insertFirst` tersusun secara terbalik dari urutan penyisipan terakhir hingga pertama, sehingga sudah 100% akurat dan sesuai dengan ekspektasi modul praktikum.

---
### 2.  Dari soal Latihan pertama, lakukan penghapusan node 9 menggunakan deleteFirst(), node menggunakan deleteLast(), dan node 8 menggunakan deleteAfter(). Kemudian tampilkan jumlah node yang tersimpan menggunakan nbList() dan lakukan penghapusan seluruh node menggunakan deleteList().
### Singlylist.h
```C++
#ifndef SINGLYLIST_H
#define SINGLYLIST_H
#define Nil NULL

#include <iostream>
using namespace std;

typedef int infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address First;
};

// Deklarasi Prosedur dan Fungsi Dasar (Soal 1)
void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);

// Deklarasi Prosedur dan Fungsi Tambahan (Soal 2)
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(List &L, address &P, address Prec);
int nbList(List L);
void deleteList(List &L);

#endif
```
File ini bertindak sebagai kerangka antarmuka dan *header guard* yang mencegah duplikasi pemanggilan dengan menggunakan `#ifndef` dan `#define SINGLYLIST_H`, serta mendefinisikan konstanta `Nil` sebagai pengganti nilai `NULL`. Di dalam file ini, didefinisikan tipe bentukan `ElmList` yang menampung informasi integer (`info`) dan pointer penunjuk (`next`), serta struktur `List` yang memegang pointer utama `First`. Seluruh tanda tangan prosedur dan fungsi dasar—seperti `CreateList`, `alokasi`, `dealokasi`, `printInfo`, dan `insertFirst`—beserta fungsi tambahannya untuk penghitungan dan penghapusan node (`deleteFirst`, `deleteLast`, `deleteAfter`, `nbList`, dan `deleteList`) dideklarasikan di sini agar dapat diakses secara terpusat.

### Singlylist.cpp
```C++
#include "Singlylist.h"

// Membuat list kosong
void CreateList(List &L) {
    L.First = Nil;
}

// Alokasi memori untuk node baru
address alokasi(infotype x) {
    address P = new ElmList;
    if (P != Nil) {
        P->info = x;
        P->next = Nil;
    }
    return P;
}

// Dealokasi memori node
void dealokasi(address &P) {
    delete P;
    P = Nil;
}

// Menampilkan seluruh info dalam list
void printInfo(List L) {
    address P = L.First;
    while (P != Nil) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

// Menambahkan elemen di awal list
void insertFirst(List &L, address P) {
    P->next = L.First;
    L.First = P;
}

// Menghapus elemen pertama
void deleteFirst(List &L, address &P) {
    if (L.First != Nil) {
        P = L.First;
        L.First = P->next;
        P->next = Nil;
    }
}

// Menghapus elemen terakhir
void deleteLast(List &L, address &P) {
    if (L.First != Nil) {
        address Q = L.First;
        if (Q->next == Nil) {
            L.First = Nil;
            P = Q;
        } else {
            address R = Nil;
            while (Q->next != Nil) {
                R = Q;
                Q = Q->next;
            }
            R->next = Nil;
            P = Q;
        }
    }
}

// Menghapus elemen setelah node tertentu (Prec)
void deleteAfter(List &L, address &P, address Prec) {
    if (Prec != Nil && Prec->next != Nil) {
        P = Prec->next;
        Prec->next = P->next;
        P->next = Nil;
    }
}

// Menghitung jumlah node dalam list
int nbList(List L) {
    int count = 0;
    address P = L.First;
    while (P != Nil) {
        count++;
        P = P->next;
    }
    return count;
}

// Menghapus seluruh node di dalam list
void deleteList(List &L) {
    address P;
    while (L.First != Nil) {
        deleteFirst(L, P);
        dealokasi(P);
    }
}
```
File ini berisi penjabaran logika pemrograman riil dari setiap prosedur dan fungsi yang telah dideklarasikan sebelumnya. Fungsi `alokasi` bertanggung jawab memesan memori dinamis menggunakan operator `new` untuk membentuk node baru dan mengisi datanya, sementara `dealokasi` membersihkan memori node yang sudah tidak terpakai guna mencegah kebocoran memori (*memory leak*). Prosedur `insertFirst` menyisipkan node baru di bagian depan list, sedangkan prosedur penghapusan seperti `deleteFirst`, `deleteLast`, dan `deleteAfter` mengatur kembali jalur pointer penghubung antar node sebelum node target dilepaskan dari memori. Selain itu, terdapat fungsi `nbList` untuk menghitung jumlah node melalui penelusuran (*traversal*) dan prosedur `deleteList` untuk membersihkan seluruh isi list secara menyeluruh.

### main1.cpp
```C++
#include "Singlylist.h"

int main() {
    List L;
    address P1, P2, P3, P4, P5, PDel;
    
    // Inisialisasi List kosong
    CreateList(L);

    // Proses Soal 1: Alokasi dan insert elemen
    P1 = alokasi(2);
    insertFirst(L, P1);
    P2 = alokasi(0);
    insertFirst(L, P2);
    P3 = alokasi(8);
    insertFirst(L, P3);
    P4 = alokasi(12);
    insertFirst(L, P4);
    P5 = alokasi(9);
    insertFirst(L, P5);

    // Proses Soal 2: Penghapusan node tertentu
    // 1. Hapus node 9 (elemen pertama) menggunakan deleteFirst()
    deleteFirst(L, PDel);
    dealokasi(PDel);

    // 2. Hapus node 2 (elemen terakhir) menggunakan deleteLast()
    deleteLast(L, PDel);
    dealokasi(PDel);

    // 3. Hapus node 8 (setelah node 12 / P4) menggunakan deleteAfter()
    deleteAfter(L, PDel, P4);
    dealokasi(PDel);

    // Menampilkan sisa isi list dan jumlah node
    printInfo(L);
    cout << "Jumlah node: " << nbList(L) << endl;

    // Menghapus seluruh node dalam list
    deleteList(L);
    cout << "List Berhasil Terhapus" << endl;
    cout << "Jumlah node: " << nbList(L) << endl;

    return 0;
}
```
File ini merupakan pusat eksekusi program yang menggabungkan seluruh alur dari Soal 1 dan Soal 2 secara berurutan. Program diawali dengan menginisialisasi list kosong melalui `CreateList`, lalu memasukkan deretan angka (2, 0, 8, 12, 9) menggunakan metode `insertFirst` hingga membentuk urutan *linked list* awal. Setelah itu, program langsung mengeksekusi rangkaian instruksi Soal 2, yakni menghapus node `9` di awal lewat `deleteFirst`, menghapus node `2` di akhir lewat `deleteLast`, serta membuang node `8` menggunakan `deleteAfter`. Sebagai tahap akhir, program mencetak sisa isi list (`12 0`), menampilkan jumlah node tersisa menggunakan `nbList()`, lalu membersihkan seluruh memori list hingga tuntas.

### Output Unguided Soal 2
![Output Soal 2](https://github.com/chypiez/Laporan-Praktikum-Struktur-Data/blob/cbf38fffcd9691f2859be756f225ab8a5f5bc530/Output%20Soal%202.png)

---
## Kesimpulan
Praktikum *Singly Linked List* ini berhasil diselesaikan dengan menerapkan desain modular yang terstruktur, yaitu memisahkan file *header* (`Singlylist.h`), file implementasi (`Singlylist.cpp`), dan program utama (`main1.cpp`/`main2.cpp`) sehingga pengelolaan alokasi memori dinamis menjadi lebih rapi dan mudah di-*debug*. Melalui implementasi operasi penyisipan (*insertFirst*) pada Soal 1 serta berbagai fungsi penghapusan (*deleteFirst*, *deleteLast*, *deleteAfter*), penghitungan node (*nbList*), dan pembersihan memori (*deleteList*) pada Soal 2, struktur data dapat dimanipulasi secara akurat sesuai dengan kebutuhan logika program.

Secara keseluruhan, hasil eksekusi dan pengujian di terminal membuktikan bahwa seluruh rangkaian modul berjalan dengan sukses serta menghasilkan *output* yang sesuai dengan ekspektasi praktikum. Penggunaan prosedur dealokasi dan pembersihan list secara menyeluruh juga memastikan bahwa integritas data tetap terjaga dengan baik sekaligus mencegah terjadinya kebocoran memori (*memory leak*).

## Referensi

[1] Malik, D. S. (2018). C++ Programming: Program Design including Data Structures. Cengage Learning. Tersedia di: Cengage C++ Data Structures

[2] GeeksforGeeks. (2026). Singly Linked List Tutorial. GeeksforGeeks. Tersedia di: GeeksforGeeks Singly Linked List