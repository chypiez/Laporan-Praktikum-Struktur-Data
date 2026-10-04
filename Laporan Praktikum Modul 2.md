# <h1 align="center">Laporan Praktikum Modul 2 - Eksplorasi Array dan Pointer Menggunakan Bahasa C++</h1>

<p align="center">Assyifa Zahra - 109082500196</p>

## Dasar Teori
C++ adalah salah satu bahasa pemrograman tingkat tinggi yang dikembangkan sebagai pengembangan dari bahasa C [1]. Di dalam pemrograman terstruktur, array dan pointer memegang peran yang sangat penting untuk mengelola data di memori komputer [2]. Array digunakan untuk menyimpan sekumpulan elemen data dengan tipe yang sama secara berurutan, sementara pointer adalah variabel khusus yang menyimpan alamat memori dari variabel lain [2]. Melalui pemanfaatan operator alamat dan dereferensi pada pointer, serta penerapan struktur array multi-dimensi, program dapat melakukan manipulasi data dan perhitungan matriks secara lebih efisien [1, 2].
## Guided
### Array 1
```C++
#include <iostream>
using namespace std;

int main() {
    int nilai[5];

    nilai[0] = 80;
    nilai[1] =85;
    nilai[2]=90;
    nilai[3] = 75;
    nilai[4] = 95;

    for (int i=0; i < 5; i++) {
    cout << "index ke-" << i << "=" << nilai[i] << endl;
    }

    return 0;
}
```
Program di atas adalah contoh dasar bagaimana cara menggunakan array atau larik dalam C++ untuk menyimpan sekumpulan data dengan tipe yang sama, yaitu bilangan bulat. Di awal, program menyiapkan sebuah wadah bernama nilai yang memiliki kapasitas untuk menampung lima angka sekaligus. Angka-angka tersebut kemudian dimasukkan satu per satu ke dalam kotak penyimpanan atau indeks yang ada, mulai dari indeks ke-0 sampai indeks ke-4. Setelah semua data tersimpan dengan rapi di dalam array tersebut, program menggunakan perulangan for untuk membaca dan menampilkan kembali isi dari setiap kotak secara berurutan. Melalui proses ini, program akan mencetak teks ke layar yang berisi nomor indeks beserta nilai yang tersimpan di dalamnya secara otomatis sebelum akhirnya program selesai dan ditutup.
### Array 2
```C++
#include <iostream>
using namespace std;

int main() {
    int nilai[3][3] = {
        {80, 85, 90},
        {75, 80, 85},
        {90, 95, 100}
    };

    // for (int i = 0; i < 3; i++) {
    //      for (int j = 0; j < 3; j++) {
    //          cout << nilai[i][j] << " ";
    //     }
    //     cout << endl;
    // }

    cout << nilai[0][0] << endl; //80
    cout << nilai[1][1] << endl; //80
    cout << nilai[2][2] << " "; //100

    return 0;
}
```
Program ini merupakan kelanjutan dari materi array sebelumnya, tetapi kali ini menggunakan array dua dimensi yang bentuknya mirip seperti tabel atau matriks dengan ukuran tiga baris dan tiga kolom. Di bagian awal, kita langsung mendeklarasikan sekaligus mengisi nilai ke dalam matriks tersebut menggunakan kurung kurawal berlapis, di mana setiap baris berisi tiga buah angka. Bagian kode yang ada di dalam komentar sebenarnya adalah cara umum menggunakan perulangan bertingkat untuk mencetak seluruh isi tabel secara otomatis. Namun, pada kode yang aktif, program hanya mengambil dan menampilkan beberapa titik data spesifik saja berdasarkan koordinat baris dan kolomnya. Program mencetak angka yang berada di baris pertama kolom pertama, lalu baris kedua kolom kedua, dan terakhir baris ketiga kolom ketiga, sebelum akhirnya program ditutup dengan mengembalikan nilai nol.
### Array 3
```C++
#include <iostream>
using namespace std;

int main() {
    int data[2][3][3] = {
        {
            {1, 2, 3},
            {4, 5, 6},
            {7, 8, 9}
        },
        {
            {10, 11, 12},
            {13, 14, 15},
            {16, 17, 18}
        }
    };

    // for (int i = 0; i < 2; i++) {
    //      for (int j = 0; j < 3; j++) {
    //          for (int k = 0; k < 3; k++) {
    //              cout << data[1][j][k] << " ";
    //          }
    //          cout << endl;
    //      }
    //      cout << endl;
    // }

    cout << data[0][1][1] << " ";// 5

    return 0;
}
```
Program ini melangkah satu tingkat lebih jauh dengan menggunakan array tiga dimensi, yang bisa dibayangkan seperti tumpukan beberapa tabel atau lembaran matriks. Di awal kode, kita menyiapkan variabel bernama `data` yang berisi dua buah blok tabel, di mana masing-masing tabel memiliki ukuran tiga baris dan tiga kolom dengan angka yang berurutan dari satu sampai delapan belas. Blok komentar di bawahnya memperlihatkan contoh bagaimana kita bisa menggunakan tiga perulangan bersarang sekaligus untuk menelusuri setiap lapis, baris, dan kolom secara menyeluruh, meskipun bagian itu sengaja dimatikan. Pada akhirnya, program hanya mengeksekusi perintah untuk mencetak satu angka spesifik saja berdasarkan koordinat lengkapnya, yaitu mengambil data yang ada pada lapisan pertama, baris kedua, dan kolom kedua, yang menghasilkan angka lima sebelum program berhenti.
### Array 4
```C++
#include <iostream>
using namespace std;

int main() {
    int data[2][2][2][2] = {
        {
            {
                {1, 2},
                {3, 4}
            },
            {
                {5, 6},
                {7, 8}
            }
        },
        {
            {
                {9, 10},
                {11, 12}
            },
            {
                {13, 14},
                {15, 16}
            }
        }
    };

    cout << data[0][0][0][0] << endl; // 1
    cout << data[1][1][1][1] << endl; //16

    return 0;
}
```
Program ini membawa konsep array ke tingkat yang lebih tinggi lagi dengan menggunakan array empat dimensi, yang sudah mulai sulit dibayangkan secara fisik karena strukturnya berlapis-lapis seperti kubus di dalam kubus atau tumpukan dimensi ruang. Di bagian awal, variabel bernama `data` dideklarasikan dengan kapasitas dua bagian utama, yang masing-masing berisi dua sub-bagian lagi, dengan total enam belas angka yang tersusun rapi dari angka satu sampai enam belas. Berbeda dari contoh sebelumnya yang sempat menggunakan banyak perulangan, kali ini program dibuat sangat simpel dan langsung fokus mengambil dua titik data ekstrem menggunakan koordinat lengkapnya. Baris pertama mencetak angka paling awal yang berada di lapisan terluar pertama, sub-bagian pertama, baris pertama, dan kolom pertama, sedangkan baris berikutnya langsung melompat untuk mengambil angka terakhir di lapisan paling ujung, sebelum akhirnya program ditutup.
### Pointer 1
```C++
#include <iostream>
using namespace std;

int main() {
    char a;
    int j;
    char arr[6];

    arr[3] = 'b';
    a = 'u';
    j = 10;

    cout << a << endl; //u
    cout << &a << endl; //alamat memory atau address

    cout << j << endl; //10
    cout << &j << endl; //alamat memory atau address

    cout << arr[3] << endl; //value
    cout << &(arr[4]) << endl; //alamat memory atau address

    return 0;
}
```
Program ini memperkenalkan konsep baru yang penting dalam pemrograman C++, yaitu penggunaan tanda ampersand `&` untuk melihat alamat memori tempat suatu variabel atau data disimpan di dalam komputer. Di awal kode, kita menyiapkan beberapa wadah dengan tipe data yang berbeda-beda, yaitu variabel karakter tunggal bernama `a`, variabel angka bulat `j`, serta sebuah array karakter berukuran enam kotak bernama `arr`. Setelah masing-masing wadah tersebut diisi dengan nilai tertentu seperti huruf `u`, angka sepuluh, dan huruf `b` pada indeks ketiga, program mulai mencetak nilainya ke layar. Yang menarik adalah ketika program memanggil tanda `&` di depan nama variabel, layar tidak lagi menampilkan isi datanya, melainkan kode unik berupa alamat memori fisik tempat data tersebut bernaung di dalam komputer, termasuk ketika melihat alamat dari salah satu indeks array yang bahkan belum diisi nilainya secara khusus.
### Pointer 2
```C++
#include <iostream>
using namespace std;

int main() {
    int x, y;
    int *px;

    x = 87;
    px = &x;
    y = *px;

    cout << "Alamat x= " << &x << endl;
    cout << "Isi px= " << px << endl;
    cout << "Isi X=" << x << endl;
    cout << "Nilai yang ditunjuk px=" << *px << endl;
    cout << "Nilai y=" << y << endl;

    return 0;
}
```
Program ini memperkenalkan konsep pointer dalam C++, yaitu sebuah variabel khusus yang tugas utamanya bukan menyimpan angka atau huruf, melainkan menyimpan alamat memori tempat variabel lain berada. Di awal kode, kita menyiapkan dua variabel biasa bertipe angka bulat bernama `x` dan `y`, serta sebuah variabel pointer bernama `px` yang ditandai dengan simbol bintang. Variabel `x` kemudian diisi dengan angka delapan puluh tujuh, lalu pointer `px` diarahkan ke `x` dengan cara mengambil alamat memorinya menggunakan tanda ampersand, sehingga `px` sekarang 'mengenal' posisi `x` di dalam komputer. Melalui proses dereferensi menggunakan tanda bintang pada `*px`, program bisa mengambil atau menyalin nilai yang ada di dalam alamat tersebut untuk diberikan kepada variabel `y`. Pada bagian akhir, program mencetak berbagai informasi ke layar, mulai dari alamat memori asli milik `x`, nilai yang disimpan di dalam pointer `px`, isi dari variabel `x` itu sendiri, nilai yang ditunjuk oleh pointer, hingga nilai akhir dari variabel `y`, yang semuanya memperlihatkan bagaimana sebuah pointer bisa memantau dan mengakses data secara langsung dari tempat penyimpanannya.
### Pointer 3
```C++
#include <iostream>
#define MAX 5
using namespace std;

int main() {
    int i, j;
    float nilai_total, rata_rata;
    float nilai[MAX];

    static int nilai_tahun[MAX][MAX] = {
        {0, 2, 2, 0, 0},
        {0, 1, 1, 1, 0},
        {0, 3, 3, 3, 0},
        {4, 4,0,0,4},
        {5,0,0,0,5}
    };

    // inisialisasi array satu dimensi
    for (i = 0; i < MAX; i++) {
        cout << "masukkan nilai ke-" << i + 1 << endl;
        cin >> nilai[i];
    }

    cout << "\ndata nilai siswa :\n";

    // menampilkan array satu dimensi
    for (i = 0; i < MAX; i++)
        cout << "nilai k-" << i + 1 << "=" << nilai[i] << endl;
        
    cout << "\n nilai tahunan : \n";

    // menampilkan array dua dimensi
    for (i = 0; i < MAX; i++) {
        for (j = 0; j < MAX; j++)
            cout << nilai_tahun[i][j];

        cout << "\n";
    }
    
    return 0;
}
```
Program ini menggabungkan beberapa konsep yang sudah dipelajari sebelumnya, mulai dari penggunaan konstanta makro untuk menentukan ukuran batas maksimal, pengolahan array satu dimensi yang diisi langsung oleh pengguna lewat keyboard, hingga penggunaan array dua dimensi statis yang sudah ditentukan datanya sejak awal. Di bagian atas, program menyiapkan konstanta bernama `MAX` bernilai lima untuk mempermudah pengaturan ukuran array, lalu mendeklarasikan beberapa variabel pendukung termasuk array dua dimensi bernama `nilai_tahun` yang membentuk pola matriks lima kali lima. Pada tahap awal eksekusi, program meminta pengguna untuk memasukkan lima buah nilai satu per satu secara interaktif melalui perintah `cin`, yang kemudian langsung disimpan dan dicetak kembali ke layar agar bisa dilihat hasilnya. Setelah itu, program melanjutkan tugasnya dengan menampilkan isi dari matriks dua dimensi `nilai_tahun` baris demi baris menggunakan perulangan bertingkat, sehingga seluruh angka yang tersusun di dalamnya tercetak rapi di layar sebelum akhirnya program ditutup dengan sukses.
### Pointer 4
```C++
#include <iostream>
using namespace std;

int main() {
    char nama[] = "strukdat";

    cout << nama << endl;
    cout << nama[3] << endl;

    return 0;
}
```
Program ini memperlihatkan cara C++ memperlakukan string atau teks sederhana, yaitu sebagai sebuah array karakter yang tersusun berderet. Di awal kode, kita mendeklarasikan sebuah variabel bertipe karakter berupa array bernama `nama` yang langsung diisi dengan kata `strukdat`. Secara internal, komputer menyimpan setiap huruf dari kata tersebut ke dalam kotak terpisah secara berurutan, lengkap dengan penanda khusus di ujungnya untuk menandai akhir dari sebuah kata. Pada saat perintah cetak pertama dijalankan, program menampilkan seluruh kata tersebut secara utuh ke layar karena C++ tahu cara membaca rangkaian karakter sampai selesai. Sementara itu, pada perintah cetak kedua, program mengambil salah satu huruf spesifik berdasarkan nomor indeksnya, yaitu menghitung dari huruf pertama, sehingga berhasil memunculkan huruf `k` yang berada di posisi keempat sebelum akhirnya program selesai.

<br>

## Unguided

### 1. Buatlah program yang dapat melakukan operasi penjumlahan, pengurangan, dan perkalian matriks 3x3
```C++
#include <iostream>
using namespace std;

int main() {
    int mat1[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };
    int mat2[3][3] = {
        {9, 8, 7},
        {6, 5, 4},
        {3, 2, 1}
    };
    int hasil[3][3];

    // Menampilkan Matriks Awal (Soal)
    cout << "Matriks 1:\n";
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << mat1[i][j] << " ";
        }
        cout << endl;
    }

    cout << "\nMatriks 2:\n";
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << mat2[i][j] << " ";
        }
        cout << endl;
    }

    // Penjumlahan Matriks
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            hasil[i][j] = mat1[i][j] + mat2[i][j];
        }
    }

    cout << "\nHasil Penjumlahan Matriks (Matriks 1 + Matriks 2):\n";
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << hasil[i][j] << " ";
        }
        cout << endl;
    }

    // Pengurangan Matriks
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            hasil[i][j] = mat1[i][j] - mat2[i][j];
        }
    }

    cout << "\nHasil Pengurangan Matriks (Matriks 1 - Matriks 2):\n";
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << hasil[i][j] << " ";
        }
        cout << endl;
    }

    // Perkalian Matriks
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            hasil[i][j] = 0;
            for (int k = 0; k < 3; k++) {
                hasil[i][j] += mat1[i][k] * mat2[k][j];
            }
        }
    }

    cout << "\nHasil Perkalian Matriks (Matriks 1 x Matriks 2):\n";
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << hasil[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
} 
```
Program ini menampilkan rincian data awal secara lengkap ke layar konsol sebelum melakukan operasi matriks. Di awal eksekusi, program langsung mencetak bentuk tabel dari matriks pertama dan matriks kedua sebagai representasi soal yang dikerjakan. Setelah itu, program menggunakan perulangan bertingkat untuk menghitung sekaligus menampilkan hasil penjumlahan dari kedua matriks baris demi baris, dilanjutkan dengan proses pengurangan dengan pola penelusuran yang serupa. Pada tahap akhir, program menerapkan tiga perulangan bersarang untuk mengalikan isi baris dan kolom sesuai kaidah matematika matriks, lalu mencetak matriks hasil perkalian tersebut secara rapi sebelum akhirnya program ditutup.

### Output Unguided 1 :

##### Output 1

![Output Soal 1](https://raw.githubusercontent.com/chypiez/Laporan-Praktikum-Struktur-Data/51cdd425d864d27c0252429233a518ca9f1126e9/Laprak%20Strukdat_Output%20Soal%201.png)

Tampilan terminal di atas menunjukkan bahwa program berhasil dijalankan dengan menampilkan data awal Matriks 1 dan Matriks 2 secara lengkap. Setelah itu, program langsung mencetak hasil dari tiga operasi hitung secara berurutan, mulai dari penjumlahan, pengurangan, hingga perkalian matriks dengan format tabel yang sangat rapi dan mudah dibaca

### 2. Berdasarkan guided pointer dan reference sebelumnya, buatlah keduanya dapat menukar nilai dari 3 variabel

```C++
#include <iostream>
using namespace std;

void tukarNilai(int *a, int *b, int *c) {
    int temp = *a;
    *a = *b;
    *b = *c;
    *c = temp;
}

int main() {
    int x, y, z;
    int *px, *py, *pz;

    x = 10;
    y = 20;
    z = 30;

    px = &x;
    py = &y;
    pz = &z;

    cout << "\nsebelum ditukar:\n";
    cout << "x = " << *px << endl;
    cout << "y = " << *py << endl;
    cout << "z = " << *pz << endl;

    tukarNilai(&x, &y, &z);

    cout << "\nsesudah ditukar:\n";
    cout << "x = " << *px << endl;
    cout << "y = " << *py << endl;
    cout << "z = " << *pz << endl;

    return 0;
}
```
Program ini dirancang khusus untuk menyelesaikan soal nomor 2 dengan menerapkan gaya pemrograman pointer dan reference yang persis seperti contoh-contoh sebelumnya. Di awal kode, kita menyiapkan tiga variabel biasa bertipe angka bulat bernama `x`, `y`, dan `z`, serta tiga buah variabel pointer bernama `px`, `py`, dan `pz` yang ditandai dengan simbol bintang. Variabel-variabel tersebut masing-masing diisi nilai sepuluh, dua puluh, dan tiga puluh, lalu pointernya diarahkan ke alamat memori variabel utama menggunakan tanda ampersand. Melalui fungsi `tukarNilai` yang menerima parameter pointer, program mengakses dan menggeser isi nilai asli yang berada di dalam memori komputer secara langsung menggunakan teknik dereferensi. Pada bagian akhir, program mencetak informasi ke layar baik sebelum maupun sesudah pertukaran terjadi dengan format biasa dan tambahan baris kosong agar tampilannya lebih rapi, sehingga terlihat jelas bagaimana pointer berhasil memantau, mengakses, dan mengubah posisi nilai dari ketiga variabel tersebut dari tempat penyimpanannya.

##### Output 1

![Output Soal 2](https://raw.githubusercontent.com/chypiez/Laporan-Praktikum-Struktur-Data/51cdd425d864d27c0252429233a518ca9f1126e9/Laprak%20Strukdat_Output%20Soal%202.png)

Tampilan terminal di atas menunjukkan bahwa program penukar nilai variabel berhasil dijalankan dengan menampilkan kondisi sebelum dan sesudah pertukaran. Sebelum ditukar, nilai variabel x bernilai 10, y bernilai 20, dan z bernilai 30. Setelah fungsi pointer dieksekusi, nilai ketiga variabel tersebut berhasil bergeser secara berurutan, di mana x menjadi 20, y menjadi 30, dan z menjadi 10
### 3.  Diketahui sebuah array 1 dimensi sebagai berikut :  
### arrA = {11, 8, 5, 7, 12, 26, 3, 54, 33, 55} 
### Buatlah program yang dapat mencari nilai minimum, maksimum, dan rata – rata dari array tersebut! Gunakan function cariMinimum() untuk mencari nilai minimum dan function cariMaksimum() untuk mencari nilai maksimum, serta gunakan prosedur hitungRataRata() untuk menghitung nilai rata – rata! Buat program menggunakan menu switch-case seperti berikut ini : 
### --- Menu Program Array --- 
### 1. Tampilkan isi array 
### 2. cari nilai maksimum 
### 3. cari nilai minimum 
### 4. Hitung nilai rata - rata
```C++
#include <iostream>
using namespace std;

void tampilkanArray(int arr[], int ukuran) {
    cout << "Isi array: ";
    for (int i = 0; i < ukuran; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

void cariMinimum(int arr[], int ukuran) {
    int min = arr[0];
    for (int i = 1; i < ukuran; i++) {
        if (arr[i] < min) {
            min = arr[i];
        }
    }
    cout << "Nilai minimum: " << min << endl;
}

void cariMaksimum(int arr[], int ukuran) {
    int max = arr[0];
    for (int i = 1; i < ukuran; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    cout << "Nilai maksimum: " << max << endl;
}

void hitungRataRata(int arr[], int ukuran) {
    float total = 0;
    for (int i = 0; i < ukuran; i++) {
        total += arr[i];
    }
    float rata = total / ukuran;
    cout << "Nilai rata - rata: " << rata << endl;
}

int main() {
    int arrA[] = {11, 8, 5, 7, 12, 26, 3, 54, 33, 55};
    int ukuran = 10;
    int pilihan;

    do {
        cout << "\n--- Menu Program Array ---\n";
        cout << "1. Tampilkan isi array\n";
        cout << "2. cari nilai maksimum\n";
        cout << "3. cari nilai minimum\n";
        cout << "4. Hitung nilai rata - rata\n";
        cout << "5. Keluar\n";
        cout << "Pilihan: ";
        cin >> pilihan;
        cout << endl;

        switch (pilihan) {
            case 1:
                tampilkanArray(arrA, ukuran);
                break;
            case 2:
                cariMaksimum(arrA, ukuran);
                break;
            case 3:
                cariMinimum(arrA, ukuran);
                break;
            case 4:
                hitungRataRata(arrA, ukuran);
                break;
            case 5:
                cout << "Keluar dari program.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 5);

    return 0;
}
```
Program di atas dibuat untuk mengolah array satu dimensi berisi sepuluh angka yang sudah ditentukan, lengkap dengan menu interaktif menggunakan struktur perulangan `do-while` dan percabangan `switch-case`. Di bagian atas, program memecah tugas menjadi beberapa fungsi terpisah: `tampilkanArray` untuk menampilkan seluruh isi data array, `cariMaksimum` untuk mencari angka terbesar, `cariMinimum` untuk mencari angka terkecil, serta `hitungRataRata` untuk menjumlahkan seluruh elemen array lalu membaginya dengan jumlah total data. Di dalam fungsi utama (`main`), array `arrA` disiapkan bersama menu pilihan yang terus berulang hingga pengguna memilih opsi keluar, sehingga program dapat membaca input pilihan pengguna dan mengeksekusi fungsi yang sesuai secara akurat.

### Output Unguided 3 :

##### Output 1
![Output Soal 3 Bagian 1](https://raw.githubusercontent.com/chypiez/Laporan-Praktikum-Struktur-Data/51cdd425d864d27c0252429233a518ca9f1126e9/Laprak%20Strukdat_Output%20Soal%203%20%281%29.png)

![Output Soal 3 Bagian 2](https://raw.githubusercontent.com/chypiez/Laporan-Praktikum-Struktur-Data/51cdd425d864d27c0252429233a518ca9f1126e9/Laprak%20Strukdat_Output%20Soal%203%20%282%29.png)

Tampilan terminal di atas menunjukkan jalannya menu interaktif untuk mengolah data array satu dimensi. Ketika pengguna memilih opsi pertama, program menampilkan seluruh isi elemen array secara berurutan. Pada pilihan kedua, program berhasil mendeteksi dan menampilkan nilai maksimum sebesar 55, sedangkan pada pilihan ketiga program menampilkan nilai minimum sebesar 3. Selanjutnya, ketika pengguna memasukkan opsi keempat, program menghitung dan menampilkan nilai rata-rata sebesar 21.4, dan terakhir program berhasil ditutup dengan aman saat pengguna memilih opsi kelima.

## Kesimpulan
Berikut adalah kesimpulan untuk laporan praktikum ini:

Praktikum modul ini membahas pemanfaatan array dan pointer di dalam bahasa pemrograman C++ untuk menyelesaikan berbagai kasus pengolahan data. Berdasarkan hasil percobaan yang telah dilakukan, dapat disimpulkan bahwa:

* Array multidimensi, khususnya array dua dimensi, sangat efektif digunakan untuk merepresentasikan dan mengolah data berbentuk tabel, seperti melakukan operasi aritmatika matriks (penjumlahan, pengurangan, dan perkalian) secara terstruktur.


* Pointer dan reference memungkinkan program untuk mengakses serta memanipulasi alamat memori secara langsung, sehingga proses pertukaran nilai antar variabel dapat dilakukan dengan efisien tanpa harus menduplikasi data aslinya.


* Penggunaan fungsi terstruktur yang dikombinasikan dengan menu interaktif berbasis `switch-case` dan perulangan `do-while` memudahkan pengguna dalam mengelola berbagai operasi array seperti menampilkan data, mencari nilai maksimum dan minimum, hingga menghitung rata-rata dalam satu program yang utuh.
## Referensi

[1] B. Stroustrup, The C++ Programming Language, 4th ed. Boston: Addison-Wesley, 2013.

[2] H. M. Deitel and P. J. Deitel, C++ How to Program, 10th ed. Hoboken: Pearson, 2017.