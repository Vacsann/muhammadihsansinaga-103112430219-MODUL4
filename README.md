# muhammadihsansinaga-103112430219-MODUL4

# <h1 align="center">Laporan Praktikum Modul 4 <br> SINGLY LINKED LIST (BAGIAN PERTAMA)</h1>
<p align="center">MUHAMMAD IHSAN SINAGA - 103112430219 </p>

## Dasar Teori

Singly Linked List adalah struktur data dinamis yang terdiri dari beberapa simpul (node) yang saling terhubung secara searah. Tiap node memiliki dua bagian, yaitu bagian yang menyimpan nilai data dan bagian yang berisi pointer menuju node berikutnya. Node terakhir memiliki pointer bernilai NULL sebagai tanda akhir dari list. Dengan bentuk berantai ini, operasi seperti menambah atau menghapus elemen dapat dilakukan dengan efisien tanpa perlu menggeser elemen lain. Beberapa operasi penting yang biasa dilakukan meliputi memasukkan data baru, menghapus node, menelusuri isi list, serta memperbarui data menggunakan pointer penghubung antar node.
## Guided

### LINKEDLIST.CPP
```go
#include <iostream>
using namespace std;

// Struktur Node
struct Node {
    int data;
    Node* next;
};

// Pointer awal
Node* head = nullptr;

// Fungsi untuk membuat node baru
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}

// Fungsi untuk menambah data di depan
void insertDepan(int data) {
    Node* newNode = createNode(data);
    newNode->next = head;
    head = newNode;
    cout << "Data " << data << " berhasil ditambahkan di depan.\n";
}

// Fungsi untuk menambah data di belakang
void insertBelakang(int data) {
    Node* newNode = createNode(data);
    if (head == nullptr) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

// Fungsi untuk menyisipkan data setelah data tertentu
void insertSetelah(int target, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != target) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << target << " tidak ditemukan!\n";
    } else {
        Node* newNode = createNode(dataBaru);
        newNode->next = temp->next;
        temp->next = newNode;
        cout << "Data " << dataBaru << " berhasil disisipkan setelah " << target << ".\n";
    }
}

// Fungsi hapus node
void hapusNode(int data) {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    Node* prev = nullptr;

    if (temp != nullptr && temp->data == data) {
        head = temp->next;
        delete temp;
        cout << "Data " << data << " berhasil dihapus.\n";
        return;
    }

    while (temp != nullptr && temp->data != data) {
        prev = temp;
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << data << " tidak ditemukan!\n";
        return;
    }

    prev->next = temp->next;
    delete temp;
    cout << "Data " << data << " berhasil dihapus.\n";
}

// Fungsi update node
void updateNode(int dataLama, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != dataLama) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << dataLama << " tidak ditemukan!\n";
    } else {
        temp->data = dataBaru;
        cout << "Data " << dataLama << " berhasil diupdate menjadi " << dataBaru << ".\n";
    }
}

// Fungsi tampilkan seluruh list
void tampilkanList() {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    cout << "Isi Linked List: ";
    while (temp != nullptr) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

// Program utama
int main() {
    int pilihan, data, target, dataBaru;

    do {
        cout << "\n=== MENU SINGLE LINKED LIST ===\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah\n";
        cout << "4. Hapus Data\n";
        cout << "5. Update Data\n";
        cout << "6. Tampilkan List\n";
        cout << "0. Keluar\n";
        cout << "Pilih: ";
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
                cin >> dataBaru;
                insertSetelah(target, dataBaru);
                break;
            case 4:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> data;
                hapusNode(data);
                break;
            case 5:
                cout << "Masukkan data lama: ";
                cin >> data;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                updateNode(data, dataBaru);
                break;
            case 6:
                tampilkanList();
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 0);

    return 0;
}


```

## Unguided

### Soal 1

buatlah single linked list untuk Antrian yang menyimpan data pembeli( nama dan pesanan). program memiliki beberapa menu seperti tambah antrian,  layani antrian(hapus), dan tampilkan antrian. \*antrian pertama harus yang pertama dilayani

```go
#include <iostream>
#include <string>
using namespace std;

struct Node {
    string nama;
    string pesanan;
    Node* next;
};

Node* front = nullptr;
Node* rear = nullptr;

bool isEmpty() {
    return front == nullptr;
}

void tambahAntrian(const string& nama, const string& menu) {
    Node* baru = new Node{nama, menu, nullptr};
    if (isEmpty()) {
        front = rear = baru;
    } else {
        rear->next = baru;
        rear = baru;
    }
    cout << "[OK] Pembeli berhasil masuk ke antrian.\n";
}

void layaniAntrian() {
    if (isEmpty()) {
        cout << "[!] Tidak ada pembeli dalam antrian.\n";
        return;
    }

    Node* temp = front;
    cout << "[LAYANI] Pembeli: " << temp->nama
         << " - Pesanan: " << temp->pesanan << endl;

    front = front->next;
    if (front == nullptr) {
        rear = nullptr;
    }

    delete temp;
}

void tampilAntrian() {
    if (isEmpty()) {
        cout << "[INFO] Antrian kosong.\n";
        return;
    }

    cout << "\n=== Daftar Antrian Pembeli ===\n";
    Node* bantu = front;
    int nomor = 1;
    while (bantu != nullptr) {
        cout << nomor++ << ". " << bantu->nama
             << " - " << bantu->pesanan << endl;
        bantu = bantu->next;
    }
    cout << "===============================\n";
}

int main() {
    system("chcp 65001 > nul"); // ubah ke UTF-8 otomatis

    int pilihan;
    string nama, pesanan;

    do {
        cout << "\n==============================\n";
        cout << "     SISTEM ANTRIAN PEMBELI   \n";
        cout << "==============================\n";
        cout << "1. Tambah Antrian\n";
        cout << "2. Layani Pembeli\n";
        cout << "3. Lihat Antrian\n";
        cout << "4. Keluar\n";
        cout << "==============================\n";
        cout << "Pilih menu: ";
        cin >> pilihan;
        cin.ignore();

        switch (pilihan) {
            case 1:
                cout << "Masukkan Nama Pembeli   : ";
                getline(cin, nama);
                cout << "Masukkan Menu Pesanan   : ";
                getline(cin, pesanan);
                tambahAntrian(nama, pesanan);
                break;
            case 2:
                layaniAntrian();
                break;
            case 3:
                tampilAntrian();
                break;
            case 4:
                cout << "[EXIT] Program selesai. Terima kasih.\n";
                break;
            default:
                cout << "[ERROR] Pilihan tidak valid.\n";
        }
    } while (pilihan != 4);

    return 0;
}

```

> Output
> ![Screenshot bagian x](ssmodul4unguided1.png)
 
Program ini merupakan implementasi struktur data antrian (queue) menggunakan singly linked list dalam bahasa C++. Setiap pembeli direpresentasikan sebagai node yang menyimpan nama dan menu pesanan, serta pointer yang menunjuk ke node berikutnya. Program ini memiliki empat fitur utama, yaitu menambah antrian baru, melayani pembeli terdepan, menampilkan seluruh antrian, dan keluar dari program. Proses penambahan dilakukan di bagian belakang antrian, sedangkan pelayanan menghapus data pembeli dari bagian depan. Dengan pendekatan linked list, ukuran antrian dapat berubah secara dinamis tanpa perlu menggeser data, sehingga efisien untuk mengelola data pembeli yang datang dan dilayani secara bergantian.

### Soal 2

buatlah program kode untuk membalik (reverse) singly linked list (1-2-3 menjadi 3-2-1) 

```go
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

Node* head = nullptr;

// Menambahkan node ke akhir linked list
void tambahNode(int nilai) {
    Node* baru = new Node{nilai, nullptr};

    if (head == nullptr) {
        head = baru;
    } else {
        Node* temp = head;
        while (temp->next) {
            temp = temp->next;
        }
        temp->next = baru;
    }
}

// Menampilkan isi linked list
void tampilList() {
    if (!head) {
        cout << "List kosong.\n";
        return;
    }

    Node* temp = head;
    while (temp) {
        cout << temp->data;
        if (temp->next) cout << " -> ";
        temp = temp->next;
    }
    cout << endl;
}

// Membalik urutan elemen dalam linked list
void balikkanList() {
    Node* prev = nullptr;
    Node* curr = head;
    Node* next = nullptr;

    while (curr) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }

    head = prev;
}

int main() {
    tambahNode(10);
    tambahNode(20);
    tambahNode(30);

    cout << "Linked List sebelum dibalik:\n";
    tampilList();

    balikkanList();

    cout << "\nLinked List setelah dibalik:\n";
    tampilList();

    return 0;
}

```

> Output
> ![Screenshot bagian x](ssmodul4unguided2.png)

Program ini merupakan implementasi singly linked list dalam bahasa C++ yang berfungsi untuk menambahkan data, menampilkan isi list, dan membalik urutan elemen di dalamnya. Setiap elemen disimpan dalam node yang memiliki dua bagian, yaitu data dan pointer ke node berikutnya. Fungsi tambahNode() digunakan untuk menambah data baru di akhir list, tampilList() menampilkan seluruh isi list secara berurutan, dan balikkanList() membalik arah pointer antar node sehingga urutan list menjadi terbalik. Dengan memanfaatkan pointer secara dinamis, program ini mampu mengelola data secara efisien tanpa batasan ukuran array.

## Referensi

1. https://www.w3schools.com/cpp/cpp_for_loop_nested.asp
2. https://www.w3schools.com/cpp/cpp_arrays.asp
7. https://www.w3schools.com/cpp/cpp_function_array.asp
8. https://www.geeksforgeeks.org/dsa/linked-list-data-structure/
9. https://en.wikipedia.org/wiki/Linked_list
