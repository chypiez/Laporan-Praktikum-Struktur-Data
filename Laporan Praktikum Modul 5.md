# <h1 align="center">Laporan Praktikum Modul 5 - Implementasi Singly Linked List pada C++
<p align="center">Assyifa Zahra - 109082500196

## **Dasar Teori**

Struktur data linier yang terdiri dari sekumpulan simpul (*node*) yang saling terhubung melalui pointer disebut sebagai *Linked List*, di mana salah satu bentuk variasinya adalah *Singly Linked List*. Pada *Singly Linked List*, setiap simpul terbagi menjadi dua komponen utama, yaitu bagian data (seperti `infotype`) untuk menyimpan informasi dan bagian pointer (`next`) yang menunjuk ke alamat simpul berikutnya. Berbeda dengan array statis yang ukurannya kaku, *Linked List* bersifat dinamis karena penambahan atau pengurangan simpul (*node*) dapat dilakukan sewaktu-waktu saat program berjalan dengan memanfaatkan alokasi memori dinamis.

Operasi dasar yang sering diterapkan pada *Singly Linked List* meliputi pembuatan list kosong (`CreateList`), pemeriksaan kondisi list, manajemen memori berupa alokasi (`alokasi`) dan dealokasi (`dealokasi`), serta penambahan elemen baru di awal list melalui prosedur `insertFirst`. Selain itu, pengelolaan pointer secara cermat sangat diperlukan agar tidak terjadi kebocoran memori (*memory leak*) ataupun pemutusan rantai antar simpul saat melakukan manipulasi data.



# Guided
### listBuah.cpp
```
#include "listBuah.h"
#include <iostream>
using namespace std;

//fungsi untuk cek apakah list kosong atau tidak
bool isEmpty(linkedlist List) {
    if(List.first == Nil){
        return true; 
    } else {
        return false;
    }
}

//pembuatan linked list kosong
void createList(linkedlist &List) {
    List.first = Nil;
}

//pembuatan node baru dengan menerapkan manajemen memori
address alokasi(string nama, int jumlah, float harga) { 
    address nodeBaru = new node; 
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.jumlah = jumlah; 
    nodeBaru->isidata.harga = harga;
    nodeBaru->next = Nil;
    return nodeBaru;
}

//penghapusan node dengan menerapkan manajemen memori
void dealokasi(address &node) {
    node->next = Nil;
    delete node;
}

//prosedur-prosedur untuk insert / menambahkan node baru kedalam list
void insertFirst(linkedlist &List, address nodeBaru) {
    nodeBaru->next = List.first; 
    List.first = nodeBaru;
}

void insertAfter(linkedlist &List, address nodeBaru, address Prev) {
    if (Prev != Nil) {
        nodeBaru->next = Prev->next;
        Prev->next = nodeBaru;
    } else {
        cout << "Node sebelumnya tidak valid!" << endl;
    }
}

void insertLast(linkedlist &List, address nodeBaru) {
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
void delFirst(linkedlist &List){
    address nodeHapus;
    if (isEmpty(List) == false) {
        nodeHapus = List.first;
        List.first = List.first->next;
        nodeHapus->next = Nil;
        dealokasi(nodeHapus);
        cout << "Node pertama berhasil terhapus!" << endl;
    } else {
        cout << "List kosong!" << endl;
    }
}

void delLast(linkedlist &List){
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
        cout << "Node terakhir berhasil terhapus!" << endl;
    } else {
        cout << "list kosong" << endl;
    }
}

void delAfter(linkedlist &List, address nodeHapus, address nodePrev){
    if(isEmpty(List) == true){
        cout << "List kosong!" << endl;
    } else { //jika list tidak kosong
        if (nodePrev != Nil && nodePrev->next != Nil) { 
            nodeHapus = nodePrev->next;       
            nodePrev->next = nodeHapus->next;  
            nodeHapus->next = Nil;         
            dealokasi(nodeHapus);
            cout << "Node setelah node " << nodePrev->isidata.nama << " berhasil terhapus!" << endl;
        } else {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

//prosedur untuk menampilkan isi list
void printList(linkedlist List) {
    if (isEmpty(List)) {
        cout << "List kosong." << endl;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu != Nil) { 
            cout << "Nama Buah : " << nodeBantu->isidata.nama << ", Jumlah : " << nodeBantu->isidata.jumlah << ", Harga : " << nodeBantu->isidata.harga << endl;
            nodeBantu = nodeBantu->next;
        }
    }
}

//function untuk menampilkan jumlah node didalam list
int nbList(linkedlist List) {
    int count = 0;
    address nodeBantu = List.first;
    while (nodeBantu != Nil) {
        count++;
        nodeBantu = nodeBantu->next; 
    }
    return count;
}

//prosedur untuk menghapus list (menghapus semua node didalam list)
void deleteList(linkedlist &List){
    address nodeBantu, nodeHapus;
    nodeBantu = List.first;
    while(nodeBantu != Nil){
        nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus); 
    }
    List.first = Nil; 
    cout << "List berhasil terhapus!" << endl;
}

/*----- MATERI PERTEMUAN 5 - SINGLY LINKED LIST (BAGIAN KEDUA) - UPDATE -----*/
//prosedur-prosedur untuk melakukan update data node
void updateFirst(linkedlist List){
    if(isEmpty(List) == true){
        cout << "List kosong!" << endl;
    } else {
        cout << "Masukkan update data node pertama : " << endl;
        cout << "Nama buah : ";
        cin >> List.first->isidata.nama;
        cout << "Jumlah : ";
        cin >> List.first->isidata.jumlah;
        cout << "Harga : ";
        cin >> List.first->isidata.harga;
        cout << "Data Berhasil Diupdate!" << endl;
        cout << endl;
    }
}

void updateLast(linkedlist List){
    if (isEmpty(List) == true) {
        cout << "List Kosong!" << endl;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu->next != Nil) {
            nodeBantu = nodeBantu->next;
        }
        cout << "masukkan update data node terakhir : " << endl;
        cout << "Nama buah : ";
        cin >> nodeBantu->isidata.nama;
        cout << "Jumlah : ";
        cin >> nodeBantu->isidata.jumlah;
        cout << "Harga : ";
        cin >> nodeBantu->isidata.harga;
        cout << "Data Berhasil Diupdate!" << endl;
        cout << endl;
    }
}

void updateAfter(linkedlist List, address nodePrev){
    if(isEmpty(List) == true){
        cout << "List kosong!" << endl;
    } else {
        if (nodePrev != Nil && nodePrev->next != Nil){
            address nodeBantu = nodePrev->next;
            cout << "masukkan update data node setelah node " << nodePrev->isidata.nama << " : " << endl;
            cout << "Nama buah : ";
            cin >> nodeBantu->isidata.nama;
            cout << "Jumlah : ";
            cin >> nodeBantu->isidata.jumlah;
            cout << "Harga : ";
            cin >> nodeBantu->isidata.harga;
            cout << "Data Berhasil Diupdate!" << endl;
            cout << endl;
        } else {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

/*----- MATERI PERTEMUAN 5 - SINGLY LINKED LIST (BAGIAN KEDUA) - SEARCHING -----*/
//prosedur-prosedur untuk searching data
//prosedur untuk mencari node berdasarkan data
void FindNodeByData(linkedlist list, string data){
    if(isEmpty(list) == true){
        cout << "List kosong!" << endl;
    } else {
        address nodeBantu = list.first;
        int posisi = 0;
        bool found = false;
        while(nodeBantu != Nil){
            posisi++;
            if(nodeBantu->isidata.nama == data){
                cout << "Data " << data << " ditemukan pada posisi ke-" << posisi << "!" << endl;
                cout << "Nama Buah : " << nodeBantu->isidata.nama << ", Jumlah : " << nodeBantu->isidata.jumlah << ", Harga : " << nodeBantu->isidata.harga << endl;
                found = true;
                break;
            }
            nodeBantu = nodeBantu->next;
        }
        if(found == false){
            cout << "Node dengan data " << data << " tidak ditemukan!" << endl;
        }
    }
    cout << endl;
}

//prosedur untuk mencari node berdasarkan alamat node
void FindNodeByAddress(linkedlist list, address node) {
    if(isEmpty(list) == true) {
        cout << "List kosong!" << endl;
    } else {
        address nodeBantu = list.first;
        int posisi = 0;
        bool found = false;
        while (nodeBantu != Nil) {
            posisi++;
            if(nodeBantu == node) {
                cout << "Node ditemukan pada posisi ke-" << posisi << "!" << endl;
                cout << "Alamat node : " << nodeBantu << endl;
                cout << "Nama Buah : " << nodeBantu->isidata.nama << ", Jumlah : " << nodeBantu->isidata.jumlah << ", Harga : " << nodeBantu->isidata.harga << endl;
                found = true;
                break;
            }
            nodeBantu = nodeBantu->next;
        }
        if(found == false) {
            cout << "Node dengan alamat " << node << " tidak ditemukan dalam list!" << endl;
        }
    }
    cout << endl;
}

//prosedur untuk mencari node berdasarkan range data (range harga)
void FindNodeByRange(linkedlist list, float hargaAwal, float hargaAkhir) {
    if(isEmpty(list) == true) {
        cout << "List kosong!" << endl;
    } else {
        address nodeBantu = list.first;
        int posisi = 0;
        bool found = false;
        cout << "--- Buah dalam range harga " << hargaAwal << " - " << hargaAkhir << " ---" << endl;
        cout << "-------------------------------------------" << endl;
        while (nodeBantu != Nil) {
            posisi++;
            float harga = nodeBantu->isidata.harga;
            if(harga >= hargaAwal && harga <= hargaAkhir) {
                cout << "Data ditemukan pada posisi ke-" << posisi << " :" << endl;
                cout << "Nama Buah : " << nodeBantu->isidata.nama << ", Jumlah : " << nodeBantu->isidata.jumlah << ", Harga : " << nodeBantu->isidata.harga << endl;
                cout << "-------------------------------------------" << endl;
                found = true;
            }
            nodeBantu = nodeBantu->next;
        }
        if(found == false) {
            cout << "Tidak ada data buah dalam range harga tersebut!" << endl;
            cout << "-------------------------------------------" << endl;
        }
    }
    cout << endl;
}
```

Program `listBuah.cpp` adalah implementasi struktur data **Singly Linked List** dalam bahasa C++ yang dirancang untuk mengelola data inventaris buah (mencakup nama, jumlah, dan harga) melalui serangkaian operasi manajemen memori yang lengkap. Program ini menyediakan fungsi dasar seperti pembuatan list, pengecekan kekosongan, alokasi dan dealokasi node, serta prosedur manipulasi data secara dinamis mulai dari penambahan (`insert First/Last/After`), penghapusan (`delete First/Last/After`), pembaruan data (`update`), hingga pencarian node berdasarkan kriteria tertentu (`FindNodeByData`, `Address`, maupun `Range` harga).

### listBuah.h
```
#ifndef LISTBUAH_H
#define LISTBUAH_H
#define Nil NULL

#include<iostream>
using namespace std;

struct buah{
    string nama;
    int jumlah; 
    float harga;
};

typedef buah dataBuah; 

typedef struct node *address; 

struct node{ 
    dataBuah isidata;
    address next;
};

struct linkedlist{ 
    address first;
};

bool isEmpty(linkedlist List);
void createList(linkedlist &List);
address alokasi(string nama, int jumlah, float harga);
void dealokasi(address &node);
void printList(linkedlist List);
void insertFirst(linkedlist &List, address nodeBaru);
void insertAfter(linkedlist &List, address nodeBaru, address prev);
void insertLast(linkedlist &List, address nodeBaru);
void delFirst(linkedlist &List);
void delLast(linkedlist &List);
void delAfter(linkedlist &List, address nodeHapus, address nodePrev);
int nbList(linkedlist List);
void deleteList(linkedlist &List);

void updateFirst(linkedlist List);
void updateLast(linkedlist List);
void updateAfter(linkedlist List, address prev);

void FindNodeByData(linkedlist list, string data);
void FindNodeByAddress(linkedlist list, address node);
void FindNodeByRange(linkedlist list, float hargaAwal, float HargaAkhir);

#endif
```

File header `listBuah.h` berfungsi sebagai antarmuka (interface) deklarasi yang mendefinisikan seluruh struktur data, tipe data bentukan, serta prototipe fungsi dan prosedur yang diimplementasikan pada file `listBuah.cpp`. Di dalamnya terdapat pendefinisian struktur `buah` untuk menyimpan informasi inventaris (nama, jumlah, dan harga), struktur `node` dan `linkedlist` untuk membentuk rantai *Singly Linked List*, serta kumpulan deklarasi modul pendukung seperti manajemen memori, manipulasi data (*insert*, *delete*, *update*), hingga fitur pencarian (*searching*).

### main.cpp
```
  #include "listBuah.h"

  #include<iostream>
  using namespace std;

  int main(){
      linkedlist List;
      address nodeA, nodeB, nodeC, nodeD, nodeE = Nil;
      createList(List);

      dataBuah dtBuah;

      nodeA = alokasi("Jeruk", 100, 3000);
      nodeB = alokasi("Apel", 75, 4000);
      nodeC = alokasi("Pir", 87, 5000);
      nodeD = alokasi("Semangka", 43, 11500);
      nodeE = alokasi("Durian", 15, 31450);

      insertFirst(List, nodeA);
      insertLast(List, nodeB);
      insertAfter(List, nodeC, nodeA);
      insertAfter(List, nodeD, nodeC);
      insertLast(List, nodeE);

      cout << "--- ISI LIST SETELAH DILAKUKAN INSERT ---" << endl;
      printList(List);
      cout << "jumlah node : " << nbList(List) << endl;
      cout << endl;

      updateFirst(List);
      printList(List);
      updateLast(List);
      printList(List);
      updateAfter(List, nodeD);
      printList(List);

      cout << "--- ISI LIST SETELAH DILAKUKAN UPDATE ---" << endl;
      printList(List);
      cout << "jumlah node : " << nbList(List) << endl;
      cout << endl;

      FindNodeByData(List, "kelapa");
      FindNodeByAddress(List, nodeC);
      FindNodeByRange(List, 5000, 10000);

      delFirst(List);
      printList(List);
      delLast(List);
      printList(List);
      delAfter(List, nodeD, nodeC);
      printList(List);

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

File `main.cpp` bertindak sebagai program utama (*driver*) untuk menguji dan menjalankan seluruh fungsi serta prosedur yang telah didefinisikan pada file header dan diimplementasikan di file `listBuah.cpp`. Program ini mendemonstrasikan siklus penggunaan *Singly Linked List* secara menyeluruh, mulai dari pembuatan list kosong, alokasi dan penyisipan data buah (`insertFirst`, `insertLast`, `insertAfter`), pembaruan isi data (*update*), pencarian berdasarkan data, alamat, maupun rentang harga (*searching*), penghapusan node secara selektif (`delFirst`, `delLast`, `delAfter`), hingga pembersihan total seluruh memori list melalui prosedur `deleteList`.

---

# Unguided
# 1. Searching
Searching merupakan operasi dasar list dengan melakukan aktivitas pencarian terhadap node tertentu. Proses ini berjalan dengan mengunjungi setiap node dan berhenti setelah node yang dicari ketemu. Dengan melakukan operasi searching, operasi-operasi seperti insert after, delete after, dan update akan lebih mudah. 

Semua fungsi dasar di atas merupakan bagian dari ADT dari singgle linked list, dan aplikasi pada bahasa pemrograman Cp semua ADT tersebut tersimpan dalam file *.c dan file *.h. 

```
/*file : list .h*/ 
/* contoh ADT list berkait dengan representasi fisik pointer*/ 
/* representasi address dengan pointer*/ 
/* info tipe adalah integer */ 
#ifndef list_H 
#define list_H 
#include "boolean.h" 
#define Nil NULL 
 
/*deklarasi record dan struktur data list*/ 
typedef int infotype; 
typedef struct elmlist *address; 
struct elmlist{ 
 infotype info; 
 address next; 
}; 
 
/* definisi list : */ 
/* list kosong jika L.first=Nil */ 
/* setiap elemen address P dapat diacu P→info atau P→next */ 
struct list { 
 address first; 
}; 
/********* pengecekan apakah list kosong ***********/ 
boolean ListEmpty(list L); 
/*mengembalikan nilai true jika list kosong*/ 
 
/********* pembuatan list kosong *********/ 
void CreateList(list &L); 
/* I.S. sembarang 
   F.S. terbentuk list kosong*/ 
    
/********* manajemen memori *********/ 
void dealokasi(address P); 
/* I.S. P terdefinisi 
   F.S. memori yang digunakan P dikembalikan ke sistem */ 
    
 
/********* pencarian sebuah elemen list *********/ 
address findElm(list L, infotype X); 
/* mencari apakah ada elemen list dengan P→info = X 
   jika ada, mengembalikan address elemen tab tsb, dan Nil jika sebaliknya 
*/ 
 
boolean fFindElm(list L, address P);
/* mencari apakah ada elemen list dengan alamat P 
   mengembalikan true jika ada dan false jika tidak ada */ 
 
address findBefore(list L, address P); 
/* mengembalikan address elemen sebelum P 
   jika prec berada pada awal list, maka mengembalikan nilai Nil */ 
    
/********* penambahan elemen **********/ 
void insertFirst(list &L, address P); 
/* I.S. sembarang, P sudah dialokasikan 
   F.S. menempatkan elemen beralamat P pada awal list */ 
    
void insertAfter(list &L, address P, address Prec); 
/* I.S. sembarang, P dan Prec alamt salah satu elemen list 
   F.S. menempatkan elemen beralamat P sesudah elemen beralamat Prec */ 
 
void insertLast(list &L, address P); 
/* I.S. sembarang, P sudah dialokasikan 
   F.S. menempatkan elemen beralamat P pada akhir list */ 
    
/********* penghapusan sebuah elemen *********/ 
void delFirst(list &L, adress &P); 
/* I.S. list tidak kosong 
   F.S. adalah alamat dari alamat elemen pertama list 
   sebelum elemen pertama list dihapus 
   elemen pertama list hilang dan list mungkin menjadi kosong 
   first elemen yang baru adalah successor first elemen yang lama */ 
 
void delLast(list &L, adress &P); 
/* I.S. list tidak kosong 
   F.S. adalah alamat dari alamat elemen terakhir list 
   sebelum elemen terakhir list dihapus 
   elemen terakhir list hilang dan list mungkin menjadi kosong 
   last elemen yang baru adalah successor last elemen yang lama */ 
 
void delAfter(list &L, address &P, address Prec); 
/* I.S. list tidak kosng, Prec alamat salah satu elemen list 
   F.S. P adalah alamat dari Prec→next, menghapus Prec→next dari list */ 
 
void delP (list &L, infotype X); 
/* I.S. sembarang 
   F.S. jika ada elemen list dengan alamat P, dimana P→info = X,  
        maka P dihapus dan P di-dealokasi,  
        jika tidak ada maka list tetap list mungkin akan menjadi kosong  
        karena penghapusan */ 
   
/********** proses semau elemen list *********/ 
void printInfo(list L); 
/* I.S. list mungkin kosong 
   F.S. jika list tidak kosong menampilkan semua info yang ada pada list */ 
 
int nbList(list L); 
/* mengembalikan jumlah elemen pada list */ 
 
/********** proses terhadap list **********/ 
void delAll(list &L); 
/* menghapus semua elemen list dan semua elemen di-dealokasi */ 
 
void invertList(list &L); 
/* I.S. sembarang 
   F.S. elemen - elemen list dibalik */ 
void copyList(list L1, list &L2) 
/* I.S. L1 sembarang 
   F.S. L1 = L2, L1 dan L2 menunjuk pada elemen yang sama */ 
 
list fCopyList(list L); 
/* mengembalikan list yang merupakan salinan dari L */ 
#endif
```

## 2. Latihan
### Soal 1
Buatlah ADT Singly Linked list sebagai berikut di dalam file “Singlylist.h”:
```
Type infotype : int 
Type address  : pointer to ElmList 
Type ElmList < 
info : infotype 
next : address 
> 
Type List : < First : address > 
procedure CreateList( input/output L : List ) 
function alokasi( x : infotype ) → address 
procedure dealokasi(input/output P : address ) 
procedure printInfo( input L : List ) 
procedure insertFirst(input/output L : List, input P :address) 
```
Kemudian buat implementasi ADT Singly Linked list pada file “Singlylist.cpp”. Adapun isi data  

![Soal 1](https://github.com/chypiez/Laporan-Praktikum-Struktur-Data/blob/9f758607790c3028ac2f151df48710d3cad38f22/Soal%201.png)

Cobalah hasil implementasi ADT pada file “main.cpp”

```
{ 
    List L; 
    address P1, P2, P3, P4, P5 = Nil; 
    createList(L); 
    P1 = alokasi(2); 
    insertFirst(L,P1); 
    P2 = alokasi(0); 
    insertFirst(L,P2); 
    P3 = alokasi(8); 
    insertFirst(L,P3); 
    P4 = alokasi(12); 
    insertFirst(L,P4); 
    P5 = alokasi(9); 
    insertFirst(L,P5); 
    printInfo(L) 
    return 0; 
}
```
![Soal 1.2](https://github.com/chypiez/Laporan-Praktikum-Struktur-Data/blob/e057c946ee40022342cdd7aed73b2056e9fa7dc9/Soal%201.2.png)

### Soal 2
Carilah elemen dengan info 8 dengan membuat fungsi baru. fungsi findElm( L : List, x : infotype ) : address 
![Soal 2](https://github.com/chypiez/Laporan-Praktikum-Struktur-Data/blob/e057c946ee40022342cdd7aed73b2056e9fa7dc9/Soal%202.png)

### Soal 3
Hitunglah jumlah total info seluruh elemen (9+12+8+0+2=31).
![Soal 3](https://github.com/chypiez/Laporan-Praktikum-Struktur-Data/blob/e057c946ee40022342cdd7aed73b2056e9fa7dc9/Soal%203.png)

### Singlylist.h
```
#ifndef SINGLYLIST_H
#define SINGLYLIST_H

#include <iostream>
using namespace std;

// Definisi tipe data
typedef int infotype;
typedef struct ElmList *address;

// Struktur Node / ElmList
struct ElmList {
    infotype info;
    address next;
};

// Struktur List
struct List {
    address First;
};

// Prototipe Fungsi dan Prosedur
void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);

// Tambahan untuk Soal 3 dan 4
address findElm(List L, infotype x);
int totalInfo(List L);

#endif
```
File header `Singlylist.h` berfungsi sebagai antarmuka (*interface*) untuk mendefinisikan seluruh struktur data dan prototipe fungsi dasar dari **Singly Linked List**. Di dalamnya mencakup deklarasi tipe data `infotype` sebagai integer, struktur `ElmList` (node) yang berisi informasi (`info`) dan pointer penerus (`next`), struktur `List` yang menampung pointer awal (`First`), serta kumpulan deklarasi prosedur dan fungsi penting seperti pembuatan list kosong, manajemen alokasi dan dealokasi memori, pencetakan elemen, hingga penyisipan data di awal list.

### Singlylist.cpp
```
#include "Singlylist.h"

// Membuat list kosong
void createList(List &L) {
    L.First = NULL;
}

// Alokasi memori untuk node baru
address alokasi(infotype x) {
    address P = new ElmList;
    if (P != NULL) {
        P->info = x;
        P->next = NULL;
    }
    return P;
}

// Dealokasi memori node
void dealokasi(address &P) {
    delete P;
    P = NULL;
}

// Menampilkan isi list
void printInfo(List L) {
    address P = L.First;
    while (P != NULL) {
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

// Fungsi untuk mencari elemen berdasarkan nilai (Soal 3)
address findElm(List L, infotype x) {
    address P = L.First;
    while (P != NULL) {
        if (P->info == x) {
            return P;
        }
        P = P->next;
    }
    return NULL;
}

// Fungsi untuk menghitung total jumlah info seluruh elemen (Soal 4)
int totalInfo(List L) {
    int total = 0;
    address P = L.First;
    while (P != NULL) {
        total += P->info;
        P = P->next;
    }
    return total;
}
```
File `Singlylist.cpp` berfungsi sebagai modul implementasi nyata yang berisi baris kode logika dari seluruh fungsi dan prosedur yang sebelumnya telah dideklarasikan di dalam file header `Singlylist.h`. Di dalam file ini, proses pengelolaan struktur data dilakukan secara dinamis melalui teknik manajemen memori, yang meliputi pembuatan list kosong (`createList`), pengalokasian dan dealokasi simpul memori (`alokasi` dan `dealokasi`), penambahan elemen baru di bagian awal list (`insertFirst`), serta penampilan seluruh isi informasi yang tersimpan di dalam list (`printInfo`).

### main.cpp
```
#include "Singlylist.h"

int main() {
    List L;
    address P1, P2, P3, P4, P5;
    P1 = P2 = P3 = P4 = P5 = NULL;

    createList(L);

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

    // Menampilkan isi list (Latihan No. 2)
    printInfo(L);

    // Pencarian elemen dengan nilai 8 (Latihan No. 3)
    address hasilCari = findElm(L, 8);
    if (hasilCari != NULL) {
        cout << "8 ditemukan dalam list" << endl;
    } else {
        cout << "8 tidak ditemukan dalam list" << endl;
    }

    // Menghitung jumlah total info seluruh elemen (Latihan No. 4)
    int jumlahTotal = totalInfo(L);
    cout << "Total info dari kelima elemen adalah " << jumlahTotal << endl;

    return 0;
}
```
File `main.cpp` bertindak sebagai program utama (*driver*) untuk menjalankan dan menguji keseluruhan modul *Singly Linked List* yang telah diimplementasikan sebelumnya. Di dalam file ini, program menginisialisasi list kosong, mengalokasikan data integer satu per satu dengan nilai `2`, `0`, `8`, `12`, dan `9` melalui prosedur *alokasi*, memasukkannya secara beruntun ke bagian awal list menggunakan fungsi *insertFirst*, serta mengeksekusi prosedur *printInfo* untuk mencetak dan menampilkan seluruh isi elemen list secara berurutan ke layar.

### Output
![Output](https://github.com/chypiez/Laporan-Praktikum-Struktur-Data/blob/78d4a90a46aa0b85c5881da43394539dfba99806/Output.png)


## Kesimpulan
Praktikum Modul 5 mengenai *Singly Linked List* ini memberikan pemahaman mendalam mengenai penerapan struktur data dinamis menggunakan pointer dalam bahasa pemrograman C++. Melalui latihan yang dilakukan, praktikan dapat memahami cara kerja alokasi memori, pembuatan simpul (*node*), serta pengoperasian fungsi dasar seperti pembentukan list kosong dan penambahan elemen di awal list (`insertFirst`).

Secara keseluruhan, penggunaan *Singly Linked List* terbukti sangat efektif untuk mengatasi keterbatasan memori statis karena ukuran struktur data dapat disesuaikan secara dinamis saat program berjalan. Implementasi yang terbagi ke dalam beberapa file modular (`Singlylist.h`, `Singlylist.cpp`, dan `main.cpp`) juga melatih kerapian penulisan kode, pemisahan antara antarmuka dan implementasi, serta kemampuan debugging dalam membangun sebuah program terstruktur.

## Referensi

1. Modul Praktikum Struktur Data. (2026). *Modul 5: Singly Linked List (Bagian Kedua)*. Fakultas Informatika, School of Computing, Telkom University.


2. Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C. (2009). *Introduction to Algorithms* (3rd ed.). MIT Press. (Referensi umum struktur data dan pointer).