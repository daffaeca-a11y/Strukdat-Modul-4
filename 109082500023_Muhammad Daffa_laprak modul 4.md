# <h1 align="center">Laporan Praktikum Modul 4 - Singly Linked List</h1>
<p align="center">Muhammad Daffa Sha'ib Nandana - 109082500023</p>

## Dasar Teori
Di dalam konsep ini, elemen-elemen data (yang disebut node) tidak disimpan pada alamat memori yang bersebelahan, melainkan saling terhubung menggunakan sebuah penunjuk atau pointer. Setiap node, yang pada kode direpresentasikan sebagai ElmList, memiliki dua komponen utama, yaitu info untuk menyimpan nilai datanya (dalam hal ini berupa bilangan bulat atau integer), serta next yang berisi alamat atau pointer untuk menunjuk ke node selanjutnya. Untuk mengetahui titik awal dari rentetan data tersebut, digunakanlah struktur List yang menyimpan pointer First sebagai penanda kepala atau elemen pertama senarai. Jika suatu node berada di posisi paling akhir, maka pointer next-nya tidak akan menunjuk ke mana-mana atau bernilai Nil.



## Guided

### 1. Menampilkan Nama, Nim dan Usia dari mahasiswa

#include "list.h"
#include <iostream>
using namespace std;

// fungsi untuk cek apakah list kosong atau tidak
bool isEmpty(linkedList List) {
    if (List.first == Nil) {
        return true;
    } else {
        return false;
    }
}

// pembuatan linked list kosong
void createList(linkedList &List) {
    List.first = Nil;
}

// pembuatan node baru dengan menerapkan manajemen memori
address alokasi(string nama, string nim, int umur) {
    address nodeBaru = new node;
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.nim = nim;
    nodeBaru->isidata.umur = umur;
    nodeBaru->next = Nil;
    return nodeBaru;
}

// penghapusan node dengan menerapkan manajemen memori
void dealokasi(address &node) {
    node->next = Nil;
    delete node;
    node = Nil;
}

// prosedur untuk insert node pada awal list
void insertFirst(linkedList &List, address nodeBaru) {
    nodeBaru->next = List.first;
    List.first = nodeBaru;
}

// prosedur untuk insert node setelah node tertentu
void insertAfter(linkedList &List, address nodeBaru, address Prev) {
    if (Prev != Nil) {
        nodeBaru->next = Prev->next;
        Prev->next = nodeBaru;
    } else {
        cout << "Node sebelumnya tidak valid!" << endl;
    }
}

// prosedur untuk insert node pada akhir list
void insertLast(linkedList &List, address nodeBaru) {
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

// prosedur untuk menghapus node pertama
void delFirst(linkedList &List) {
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

// prosedur untuk menghapus node terakhir
void delLast(linkedList &List) {
    address nodeHapus, nodePrev;

    if (isEmpty(List) == false) {
        nodeHapus = List.first;

        if (nodeHapus->next == Nil) {
            List.first->next = Nil;
            dealokasi(nodeHapus);
            List.first = Nil;
        } else {
            while (nodeHapus->next != Nil) {
                nodePrev = nodeHapus;
                nodeHapus = nodeHapus->next;
            }
            nodePrev->next = Nil;
            dealokasi(nodeHapus);
        }
    } else {
        cout << "List kosong" << endl;
    }
}

// prosedur untuk menghapus node setelah node tertentu
void delAfter(linkedList &List, address nodeHapus, address nodePrev) {
    if (isEmpty(List) == true) {
        cout << "List kosong!" << endl;
    } else {
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

// prosedur untuk menampilkan isi list
void printList(linkedList List) {
    if (isEmpty(List)) {
        cout << "List kosong." << endl;
    } else {
        address nodeBantu = List.first;

        while (nodeBantu != Nil) {
            cout << "Nama : " << nodeBantu->isidata.nama
                 << ", NIM : " << nodeBantu->isidata.nim
                 << ", Usia : " << nodeBantu->isidata.umur
                 << endl;

            nodeBantu = nodeBantu->next;
        }
    }
}

// fungsi untuk menampilkan jumlah node di dalam list
int nbList(linkedList List) {
    int count = 0;
    address nodeBantu = List.first;

    while (nodeBantu != Nil) {
        count++;
        nodeBantu = nodeBantu->next;
    }

    return count;
}

// prosedur untuk menghapus semua node di dalam list
void deleteList(linkedList &List) {
    address nodeHapus;
    address nodeBantu = List.first;

    while (nodeBantu != Nil) {
        nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus);
    }

    List.first = Nil;
    cout << "List sudah terhapus!" << endl;
}


## Unguided

### 1. Soal 1

#ifndef SINGLYLIST_H_INCLUDED
#define SINGLYLIST_H_INCLUDED

typedef int infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address first;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(const List &L);
void insertFirst(List &L, address P);
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);
int nbList(const List &L);
void deleteList(List &L);

#endif


##### Output 1
![Screenshot Output Unguided 2_1] https://github.com/daffaeca-a11y/Strukdat-Modul-4/blob/main/output%20soal%201.jpeg 

Program menampilkan susunan senarai awal berupa angka 9, 12, 8, 0, dan 2, yang menandakan operasi penyisipan data berfungsi dengan baik.

### 2. Soal 2

#include <iostream>
#include "Singlylist.h"
using namespace std;

int main() {
    List L;
    address P1, P2, P3, P4, P5;
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

    cout << "List awal: ";
    printInfo(L);

    address Hapus;
    deleteFirst(L, Hapus);
    dealokasi(Hapus);

    deleteLast(L, Hapus);
    dealokasi(Hapus);

    // Node 8 dihapus dengan menghapus node setelah node 12.
    address Prec = L.first;
    deleteAfter(L, Prec, Hapus);
    dealokasi(Hapus);

    cout << "List setelah penghapusan: ";
    printInfo(L);
    cout << "Jumlah node : " << nbList(L) << endl;

    deleteList(L);
    cout << "- List Berhasil Terhapus -" << endl;
    cout << "Jumlah node : " << nbList(L) << endl;

    return 0;
}

##### Output 2
![Screenshot Output Unguided 3_1] https://github.com/daffaeca-a11y/Strukdat-Modul-4/blob/main/output%20soal%202.jpeg

Setelah dilakukan operasi penghapusan beberapa node tertentu, program juga berhasil memperbarui isi senarai dan menampilkannya menjadi hanya tersisa angka 12 dan 0.

## Kesimpulan
pada modul kali ini saya belajar bahwa Singly Linked List menyimpan data dalam node yang saling terhubung melalui pointer next, lalu first menunjuk node pertama.
 
## Referensi


