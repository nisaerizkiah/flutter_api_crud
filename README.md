# flutter_api_crud
**Nama: Nisa Eka Kholifaturrizkiah
**NIM: 362458302018    

## Tujuan Praktikum
Praktikum ini bertujuan untuk memahami konsep CRUD(Create, Read, Update, Delete) menggunakan Bahasa pemrograman Dart dan framework Flutter. Mahasiswa diharapkan mampu mengimplementasikan komunikasi antara aplikasi mobile dengan API berbasis REST melalui package http.
## Dasar Teori
API (Application Programming Interface) adalah seperangkat definisi, protocol, dan tools untuk membangun perangkat lunak aplikasi. Dalam praktikum ini, API bertindak sebagai jembatan yang memungkinkan aplikasi Flutter (klien) Anda berkomunikasi dengan server (backend) untuk mengambil atau mengirim data.

REST (Representational State Transfer) adalah gaya arsitektur yang paling umum digunakan untuk membuat API berbasis web. REST API menggunakan metode HTTP standar untuk melakukan operasi pada resources.
Berikut adalah metode HTTP standar yang digunakan dalam operasi CRUD:
Method:GET	Operasi Crud:READ	untuk mengambil satu atau lebih resource.
Method:POST	Operasi CRUD:CREATE	untuk membuat resource baru.
Method:PUT	Operasi CRUD:UPDATE	untuk memperbarui seluruh resource.
Method:PATCH	Operasi CRUD:UPDATE	untuk memperbarui Sebagian resource.
Method:DELETE	Operasi CRUD:DELETE	untuk menghapus satu atau lebih resource.

JSON (JavaScript Object Notation)
JSON adalah format pertukaran data yang ringan dan mudah dibaca manusia serta di parsing oleh mesin. Hamper semua REST API menggunakan JSON sebagai format data utama.

Package HTTP adalah library yang direkomendasikan untuk melakukan permintaan HTTP di Dart dan Flutter. Package ini menyediakan fungsi-fungsi mudah digunakan seperti http.get(), http.post(), http.put(), dan http.delete().   
## Langkah-langkah Implementasi
1. Membuat project Flutter baru (flutter_api_crud), kemudian menambahkan dependency http di pubspec.yaml (http: ^1.2.1)
2. Membuat Model. Dengan membuat file user_model.dart di dalam folder lib. Model digunakan untuk merepresentasikan data user dari API.
3. Membuat ApiService (api_service.dart)
Didalamnya berisi fungsi CRUD:
•	fetchUsers() untuk mengambil daftar user
•	createUser() untuk tambah user
•	updateUser() untuk ubah user
•	deleteUser() untuk hapus user
4. Halaman Read (UserListPage)
Halaman ini berfungsi untuk menampilkan daftar pengguna (user) yang diambil dari API memnggunakan method GET.
Proses pengambilan data dilakukan menggunakan FutureBuilder, karena data dari API membutuhkan waktu untuk diambil melalui jaringan.
<img width="441" height="979" alt="image" src="https://github.com/user-attachments/assets/7e04ca48-b701-4a7a-8562-14e0556e1f90" />
5. Halaman Create (Tambah User)
Halaman create berfungsi untuk menambah data pengguna bar uke dalam database (melalui API). Halaman ini berisi form input untuk mengisi nama dan pekerjaan user, serta tombol “Tambahkan User”.
<img width="441" height="979" alt="image" src="https://github.com/user-attachments/assets/60a4b90c-436b-4657-9edc-e78ba7d91f72" />
6. Halaman Update (Edit User)
Halaman update digunakan untuk mengubah data pengguna yang sudah ada. Halaman ini mirip dengan halaman tambah user, tetapi form nya sudah terisi data lama, dan tombolnya berubah menjadi “Update User”.
<img width="442" height="982" alt="image" src="https://github.com/user-attachments/assets/f8abdcf0-8bcd-4c1d-bb48-91ba57b777be" />
7. Fitur Delete 
Fitur delete digunakan untuk menghapus data user dari daftar. Di implementasikan dengan ikon sampah berwarna merah di tiap item daftar user.
<img width="439" height="975" alt="image" src="https://github.com/user-attachments/assets/d433e40e-29db-48b6-9915-c34221ad268b" />
## Analisis Kode
1. File user_model.dart
File ini berfungsi untuk merepresentasikan struktur data user dari API ke dalam bentuk objek Dart agar mudah digunakan di aplikasi.
Class user menyimpan data satu pengguna.
Konstruktor fromJson() digunakan untuk mengubah data JSON yang diterima dari API menjadi objek User.
Model ini menjadi jembatan antara API dan tampilan (UI).
2. File api_service.dart
File ini berfungsi sebagai penghubung antara aplikasi Flutter dan API server.
Semua operasi CRUD dilakukan di sini menggunakan package http.
a.	Fungsi fetchUsers()
Mengambil data user dari endpoint API. Melakukan parsing JSON menjadi list objek User. Dan Jika status code bukan 200, dilempar Exception untuk ditangani di UI.
b.	Fungsi createUser()
Mengirim data user baru menggunakan method POST. Data dikirim dalam format JSON melalui header Content-Type. Jika berhasil, API mengembalikan status 201 Created.
c.	Fungsi updateUser()
Memperbarui data user berdasarkan ID menggunakan method PUT. Jika berhasil, API mengembalikan status 200 OK. Data yang diubah dikirim dalam format JSON.
d.	Fungsi deleteUser()
Menghapus data user berdasarkan ID dengan method DELETE. Jika berhasil, API membalas 204 No Content yang menandakan penghapusan sukses.
3. File UserListPage (Halaman Read)
Menampilkan daftar user menggunakan FutureBuilder. FutureBuilder menunggu data dari API sebelum membangun UI. Saat data diterima, setiap user ditampilkan dalam ListTile. Menampilkan indikator loading dan pesan error bila diperlukan.
4. File AddUserPage (Halaman Create)
Form untuk menambahkan user baru. Tombol ini menjalankan fungsi _createUser(), yang memanggil apiService.createUser(). Terdapat validasi input agar form tidak kosong. Jika sukses, tampil pesan melalui SnackBar dan navigasi kembali ke halaman utama.
5. File EditUserPage (Halaman Update)
Form ini menampilkan data lama user untuk diedit. Data awal diisi berdasarkan objek user yang dikirim dari halaman utama. Setelah diubah dan dikirim, updateUser() akan memperbarui data melalui API.
6. Fitur Delete
Menampilkan dialog konfirmasi sebelum menghapus user. Setelah konfirmasi, fungsi deleteUser() dijalankan. setState() dipanggil agar daftar user diperbarui tanpa reload seluruh aplikasi.
## Kesimpulan dan Saran
Dari hasil praktikum yang telah dilakukan, dapat disimpulkan bahwa proses pembuatan aplikasi Flutter dengan penerapan fungsi CRUD (Create, Read, Update, Delete) menggunakan REST API berjalan dengan baik, dan dapat mengembangkan kemampuan untuk membangun aplikasi mobile yang terhubung dengan data eksternal secara real time dan terstruktur. Namun masih terdapat beberapa kendala yang disebabkan oleh keterbatasan API ReqRes nya, yakni membatasi permintaan POST/PUT/DELETE dari beberapa jaringan. Pada bagian GET masih dapat dijalankan karena bersifat public, sedangkan POST, PUT, DELETE terdapat error 401 Unauthorized.
Agar pengembangan aplikasi lebih baik, mungkin beberapa saran yang dapat diberikan antara lain:
1.	Menambahkan autentikasi pengguna (login dan register) agar data lebih aman dan bersifat personal.
2.	Menambahkan fitur pencarian dan filter data agar pengguna dapat menemukan informasi dengan lebih cepat.
