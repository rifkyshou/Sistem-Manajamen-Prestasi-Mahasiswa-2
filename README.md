# Sistem-Pengelolaan-Prestasi-Mahasiswa-2
Program sederhana dengan sistem login berbasis role (Admin &amp; Mahasiswa) untuk mengelola data prestasi mahasiswa menggunakan **Dictionary, Looping, Functions, Error Handling**, serta fitur CRUD.

## Identitas
- Nama : Awang Rifky Muhadzib
- Kelas : B
- NIM : 2509116059

## Deskripsi Program

Di dalam program, terdapat sistem login yang membedakan dua jenis pengguna:

- Admin → memiliki hak akses penuh, bisa menambahkan, melihat, mengubah, dan menghapus data (CRUD).

- Mahasiswa → hanya bisa menambahkan dan melihat data prestasi.

Beberapa konsep dasar pemrograman yang diterapkan di sini antara lain Dictionary, Looping, Functions, dan Error Handling supaya program lebih terstruktur, mudah dijalankan, serta mampu menangani kesalahan input dari pengguna.

Data prestasi mahasiswa yang bisa disimpan meliputi:
1. Nama mahasiswa
2. Nama lomba
3. Juara (1/2/3)
4. Tahun lomba
5. Tingkat lomba (Kabupaten/Provinsi/Nasional/Internasional)

## Flowchart Sistem Pengelolaan Prestasi Mahasiswa
<img width="1999" height="2503" alt="MINPRO 2 drawio (3)" src="https://github.com/user-attachments/assets/72792a2b-0c7b-461d-b643-3e0875e6ecce" />

## Program Sistem Pengelolaan Prestasi Mahasiswa

```python
# NAMA    : AWANG RIFKY MUHADZIB
# KELAS   : B
# NIM     : 2509116059
# - MINI PROJECT 2 DASAR DASAR PEMROGRAMAN -

data = []

users = {
    "Admin": "Admin@123",
    "Mahasiswa": "Mahasiswa@123"
}

print("+","-"*68,"+")
print("|        Selamat Datang di Sistem Pengelolaan Prestasi Mahasiswa       |")
print("|                           Halaman Login                              |")
print("+","-"*68,"+")

def login():
    kesempatan = 3
    while kesempatan > 0:
        username = input("--> Username: ")
        password = input("--> Password: ")

        if username in users and users[username] == password:
            print("+","-"*68,"+")
            print("|                          Login berhasil !                            |")
            print("+","-"*68,"+")
            return username
        else:
            kesempatan -= 1
            print(f"Login gagal. Sisa kesempatan: {kesempatan}")

    print("+","-"*68,"+")
    print("|              Login gagal setelah 3 kali. Keluar program.             |")
    print("+","-"*68,"+")
    exit()

def tambah_prestasi():
    print("\n+","-"*68,"+")
    print("|                    Tambahkan Prestasi Mahasiswa !                    |")
    print("+","-"*68,"+")
    nama = input("Nama Mahasiswa : ")
    lomba = input("Nama Lomba : ")
    juara = input("Juara Berapa (1/2/3) : ")
    tahun = input("Tahun Lomba : ")
    tingkat = input("Tingkat (Kabupaten/Provinsi/Nasional/Internasional) : ")
    
    data.append([nama, lomba, juara, tahun, tingkat])
    print("+","-"*68,"+")
    print(f"|            Prestasi atas nama {nama} berhasil ditambahkan!           |")
    print("+","-"*68,"+")

def lihat_prestasi():
    print("\n+","-"*68,"+")
    print("|                      Daftar Prestasi Mahasiswa                       |")
    print("+","-"*68,"+")
    if data == []:
        print("|                 Belum ada prestasi yang ditambahkan !                |")
        print("+","-"*68,"+")
    else:
        n = 0
        while n < len(data):
            a = data[n]
            print(f"{n+1}. {a[0]} - {a[1]} - Juara {a[2]} - Tahun {a[3]} - Tingkat {a[4]}")
            n = n + 1

def update_prestasi():
    lihat_prestasi()
    if data == []:
        return

    try:
        index = int(input("Pilih nomor untuk update: "))
        nama = input("Nama Mahasiswa baru: ")
        lomba = input("Nama Lomba baru: ")
        juara = input("Juara baru (1/2/3): ")
        tahun = input("Tahun Lomba baru: ")
        tingkat = input("Tingkat baru (Kabupaten/Provinsi/Nasional/Internasional): ")

        data[index - 1] = [nama, lomba, juara, tahun, tingkat]
        print("+","-"*68,"+")
        print("|                      Data berhasil diupdate !                        |")
        print("+","-"*68,"+")
    except (ValueError, IndexError, EOFError, KeyboardInterrupt):
        print("+","-"*68,"+")
        print("|                        ERROR, Ulangi Lagi !                          |")
        print("+","-"*68,"+")

def hapus_prestasi():
    lihat_prestasi()
    if data == []:
        return

    pilihan = input("Hapus semua (y) atau pilih nomor (g): ").strip().lower()

    if pilihan == 'y':
        data.clear()
        print("+","-"*68,"+")
        print("|                   Semua data berhasil dihapus!                       |")
        print("+","-"*68,"+")
    elif pilihan == "g" :
        try:
            indeks = int(input("--> Pilih nomor untuk hapus : "))
            nama = data[indeks - 1][0]
            del data[indeks - 1]
            print("+","-"*68,"+")
            print(f"|                Prestasi {nama} berhasil dihapus!                     |")
            print("+","-"*68,"+")
        except (ValueError, IndexError, EOFError, KeyboardInterrupt):
            print("+","-"*68,"+")
            print("|                        ERROR, Ulangi Lagi !                          |")
            print("+","-"*68,"+")
    else:
        print("+","-"*68,"+")
        print("|                       ERROR, Pilih (y)/(g) !                         |")
        print("+","-"*68,"+")

pengguna = login()

while True:
    if pengguna == "Admin":
        print("\n\n+","-"*68,"+")
        print("|                        Menu Prestasi Mahasiswa |                     |") 
        print("+","-"*68,"+")
        print("1. Tambahkan Prestasi Mahasiswa")
        print("2. Lihat Prestasi Mahasiswa")
        print("3. Update Prestasi Mahasiswa")
        print("4. Hapus Prestasi Mahasiswa")
        print("5. Keluar")

        pilihan = input("--> Pilih menu (1-5) : ")

        if pilihan == "1":
            tambah_prestasi()
        elif pilihan == "2":
            lihat_prestasi()
        elif pilihan == "3":
            update_prestasi()
        elif pilihan == "4":
            hapus_prestasi()
        elif pilihan == "5":
            print("+","-"*68,"+")
            print("| Terima kasih telah menggunakan Sistem Pengelolaan Prestasi Mahasiswa |")
            print("+","-"*68,"+")
            break
        else:
            print("+","-"*68,"+")
            print("|                    Menu tidak tersedia, coba lagi.                   |")
            print("+","-"*68,"+")

    elif pengguna == "Mahasiswa":
        print("\n\n+","-"*68,"+")
        print("|                        Menu Prestasi Mahasiswa |                     |") 
        print("+","-"*68,"+")
        print("1. Tambahkan Prestasi Mahasiswa")
        print("2. Lihat Prestasi Mahasiswa")
        print("3. Keluar")

        pilihan = input("--> Pilih menu (1-3) : ")

        if pilihan == "1":
            tambah_prestasi()
        elif pilihan == "2":
            lihat_prestasi()
        elif pilihan == "3":
            print("+","-"*68,"+")
            print("| Terima kasih telah menggunakan Sistem Pengelolaan Prestasi Mahasiswa |")
            print("+","-"*68,"+")
            break
        else:
            print("+","-"*68,"+")
            print("|                    Menu tidak tersedia, coba lagi.                   |")
            print("+","-"*68,"+")
```
## Kondisi
### Kondisi Login
#### 1. Jika username dan password benar
<img width="653" height="200" alt="image" src="https://github.com/user-attachments/assets/68926022-9828-4fc1-b10f-487bf35d5806" />

masuk ke menu sesuai role.

#### 3. Jika username dan password salah
<img width="661" height="155" alt="image" src="https://github.com/user-attachments/assets/492eb507-eab4-43bf-b5cd-5249445b0180" />

mendapat pesan error dan berkurang 3 kali kesempatan login.

#### 4. Jika salah sampai 3 kali
<img width="652" height="347" alt="image" src="https://github.com/user-attachments/assets/2bf4cbf4-c4c9-47e9-bd63-54032d1b721d" />

program otomatis berhenti.

### Kondisi Admin dan Mahasiswa
#### 1. Admin
Admin memiliki hak penuh untuk melakukan CRUD (Create, Read, Update, Delete)

<img width="656" height="198" alt="image" src="https://github.com/user-attachments/assets/5aded49e-640f-4014-a7ce-42cdfcc98886" />

#### -- Tambahkan Prestasi --
<img width="652" height="212" alt="image" src="https://github.com/user-attachments/assets/0b399870-7984-4c0b-9394-f0615b73c883" />

- Fungsi: Menambahkan data prestasi baru ke dalam list data.

Program akan meminta pengguna mengisi
  1. Nama mahasiswa
  2. Nama lomba
  3. Juara keberapa
  4. Tahun lomba
  5. Tingkat lomba
  
- Setelah diisi, data disimpan dan muncul pesan konfirmasi.

<img width="683" height="247" alt="image" src="https://github.com/user-attachments/assets/8785d275-4852-4a52-8b1f-6e76b5f1bbbd" />

Output ini menunjukkan bahwa data prestasi baru berhasil disimpan. Program tidak langsung berhenti, tapi kembali ke menu utama.

#### -- Lihat Prestasi --
<img width="658" height="202" alt="image" src="https://github.com/user-attachments/assets/752a12fc-9206-4d08-b170-3050f8309ed3" />

Tujuan: Menampilkan semua data prestasi yang sudah tersimpan.

Pada Kondisi ini Memungkinkan Akan Ada Dua Output yang Berbeda

- JIka `data` Masing Kosong :
<img width="656" height="107" alt="image" src="https://github.com/user-attachments/assets/980c5a57-0396-44e1-a55a-5202ec581c9e" />

Program mengecek if data == [], karena kosong, ditampilkan pesan bahwa belum ada data prestasi.

- Jika `data` Sudah Diisi Setelah Menambahkan : 
<img width="745" height="122" alt="image" src="https://github.com/user-attachments/assets/39b4411d-cbee-4034-b045-7887e06d890b" />

Program melakukan looping while n < len(data) untuk menampilkan seluruh data prestasi yang sudah ditambahkan lengkap dengan urutan nomornya.

#### -- Update Prestasi --
<img width="652" height="211" alt="image" src="https://github.com/user-attachments/assets/60f7d33f-e54a-414b-9bea-3e481b6f2e8f" />

Tujuan: Mengupdate data prestasi yang ingin diubah apabila ingin memperbarui atau terjadi kesalahan

Pada Kondisi Akan Ada Tiga Output yang Berbeda

- JIka `data` Masing Kosong :
<img width="656" height="107" alt="image" src="https://github.com/user-attachments/assets/980c5a57-0396-44e1-a55a-5202ec581c9e" />

Program mengecek if data == [], karena kosong, ditampilkan pesan bahwa belum ada data prestasi.
- Jika `data` Sudah Diisi lalu Update :
<img width="661" height="321" alt="image" src="https://github.com/user-attachments/assets/57e3399d-026a-4888-81a9-4159a5c27155" />
<img width="673" height="138" alt="image" src="https://github.com/user-attachments/assets/39da85c7-660c-46ab-b435-47a245046979" />

- Jika Tidak Memilih Yang Tersedia (Value Error, KeyboardInterrupt, EOFError, IndexError):
<img width="666" height="175" alt="image" src="https://github.com/user-attachments/assets/a0df32ba-eddb-418e-b13f-bd7036fb517f" />

Program menampilkan pesan error karena memilih yang tidak tersedia seperti CTRL+C, CTRL+Z, Enter, dan lain lain.

#### -- Delete Prestasi --
<img width="660" height="205" alt="image" src="https://github.com/user-attachments/assets/945c0fce-79e1-4fb7-ad16-fec349bc49fe" />

Tujuan: Menghapus data prestasi apabila sudah tidak diperlukan semuanya atau ingin menghapus salah satunya

Pada Kondisi Akan Ada 4 Output yang Berbeda

- JIka `data` Masing Kosong :
<img width="656" height="107" alt="image" src="https://github.com/user-attachments/assets/980c5a57-0396-44e1-a55a-5202ec581c9e" />

- Jika Memilih Menghapus Semua `data` (y):
<img width="660" height="572" alt="image" src="https://github.com/user-attachments/assets/c2f76d43-10fb-4789-a131-ed25b4f18642" />
Program menghapus semua data prestasi mahasiswa yang telah ditambahkan menggunakan data.clear()

- Jika Memilih Menghapus Salah Satu `data` (g):
<img width="671" height="609" alt="image" src="https://github.com/user-attachments/assets/ce8e214b-a6bd-4ead-bc48-c6cc2706a219" />
Program menghapus data yang telah dipilih

- Jika Tidak Memilih Yang Tersedia (Value Error, KeyboardInterrupt, EOFError, IndexError):
<img width="665" height="187" alt="image" src="https://github.com/user-attachments/assets/4cc99201-9719-4084-9d46-6bde10f13abb" />
<img width="655" height="202" alt="image" src="https://github.com/user-attachments/assets/edde097e-1306-4432-b8b2-60996a2776fd" />
Program menampilkan pesan error karena memilih yang tidak tersedia seperti CTRL+C, CTRL+Z, Enter, dan lain lain.

#### 2. Mahasiswa
Mahasiswa hanya bisa Create dan Read

<img width="655" height="158" alt="image" src="https://github.com/user-attachments/assets/b4489c7d-33c0-4461-a5f6-a7f8f8935457" />

#### -- Tambahkan Prestasi --
<img width="652" height="212" alt="image" src="https://github.com/user-attachments/assets/0b399870-7984-4c0b-9394-f0615b73c883" />

- Fungsi: Menambahkan data prestasi baru ke dalam list data.

Program akan meminta pengguna mengisi
  1. Nama mahasiswa
  2. Nama lomba
  3. Juara keberapa
  4. Tahun lomba
  5. Tingkat lomba
  
- Setelah diisi, data disimpan dan muncul pesan konfirmasi.

<img width="683" height="247" alt="image" src="https://github.com/user-attachments/assets/8785d275-4852-4a52-8b1f-6e76b5f1bbbd" />

Output ini menunjukkan bahwa data prestasi baru berhasil disimpan. Program tidak langsung berhenti, tapi kembali ke menu utama.

#### -- Lihat Prestasi --
<img width="745" height="122" alt="image" src="https://github.com/user-attachments/assets/d65e5705-a5d7-45f7-bb9a-a778535efc3f" />

Tujuan: Menampilkan semua data prestasi yang sudah tersimpan.

Pada Kondisi ini Memungkinkan Akan Ada Dua Output yang Berbeda

- JIka `data` Masing Kosong :
<img width="656" height="107" alt="image" src="https://github.com/user-attachments/assets/980c5a57-0396-44e1-a55a-5202ec581c9e" />

Program mengecek if data == [], karena kosong, ditampilkan pesan bahwa belum ada data prestasi.

- Jika `data` Sudah Diisi Setelah Menambahkan : 
<img width="745" height="122" alt="image" src="https://github.com/user-attachments/assets/39b4411d-cbee-4034-b045-7887e06d890b" />

Program melakukan looping while n < len(data) untuk menampilkan seluruh data prestasi yang sudah ditambahkan lengkap dengan urutan nomornya.


