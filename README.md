# Majulah Shop Mobile

Repositori ini berisi sebuah aplikasi Football Shop sederhana menggunakan Flutter yang dibuat untuk memenuhi tugas individu mata kuliah Pemrograman Berbasis Platform.

<details> 
<summary>Tugas Individu 7</summary>

## 1\. Widget Tree dan Hubungan Parent-Child

**Widget Tree** adalah representasi struktur dari seluruh UI (User Interface) di Flutter. Karena di Flutter semuanya adalah widget, UI dibangun dengan menyusun widget di dalam widget lain. Susunan bersarang (nested) inilah yang membentuk sebuah struktur pohon (tree).

**Hubungan Parent-Child** adalah inti dari widget tree:

- **Parent:** Adalah widget yang berisi widget lain.
- **Child:** Adalah widget yang berada di dalam widget lain.

Hubungan ini sangat penting karena **parent sering kali mengontrol atau memengaruhi child-nya**.

**Contoh:**

```dart
Center( // <-- PARENT
  child: Text( // <-- CHILD
    'Hello, Flutter!',
  ),
)

// Hubungannya: Center (parent) memberi instruksi kepada Text (child) untuk diposisikan di tengah layar. Text sendiri hanya menampilkan teks 'Hello, Flutter!'.
```

## 2\. Widget yang digunakan

### a\. Widget Kustom (Custom Widgets)

- **`MyApp`** (`StatelessWidget`):
  - **Fungsi:** _root widget_ untuk membungkus seluruh aplikasi dengan `MaterialApp` dan mengatur tema global (primary color: Merah).
- **`MyHomePage`** (`StatelessWidget`):
  - **Fungsi:** widget halaman utama untuk membangun seluruh tampilan halaman, termasuk `AppBar`, kartu informasi (NPM, Nama, Kelas), dan `GridView` yang berisi menu (`ItemCard`).
- **`InfoCard`** (`StatelessWidget`):
  - **Fungsi:** Widget kustom untuk menampilkan kartu informasi kecil (seperti NPM, Nama, dan Kelas). Isinya adalah `Card` yang memiliki `Column` untuk menyusun `Text` judul dan `Text` konten.
- **`ItemCard`** (`StatelessWidget`):
  - **Fungsi:** Widget kustom untuk menampilkan satu item menu di dalam `GridView`. Isinya adalah `Material` (untuk warna dan sudut melengkung) yang dibungkus `InkWell` (agar bisa diklik) dan menampilkan `Icon` serta `Text` di dalamnya.

### b\. Widget Struktur & Navigasi

- **`MaterialApp`**:
  - **Fungsi:** Widget utama di `main.dart`, menyediakan banyak fungsionalitas dasar seperti tema (`theme`), navigasi, dan `home` aplikasi ke `MyHomePage`.
- **`Scaffold`**:
  - **Fungsi:** Struktur dasar halaman di `MyHomePage`, menyediakan "kerangka" halaman yang memiliki slot untuk `appBar` dan `body`.
- **`AppBar`**:
  - **Fungsi:** _Bar_ atas berwarna (diambil dari tema) yang ditampilkan di dalam `Scaffold`. Dalam kode ini, fungsinya adalah menampilkan `Text` judul 'Majulah Shop'.
- **`ScaffoldMessenger`**:
  - **Fungsi:** Digunakan (melalui `ScaffoldMessenger.of(context)`) di dalam `ItemCard` untuk menampilkan `SnackBar` (pesan pop-up) di bagian bawah layar ketika sebuah item menu diklik.

### c\. Widget Tata Letak (Layout)

- **`Column`**:
  - **Fungsi:** Menyusun widget-widget child secara **vertikal** (dari atas ke bawah).
  - **Penggunaan:**
    1.  Di `MyHomePage`: Menyusun `Row` (info card), `SizedBox` (jarak), dan `Center` (grid) secara vertikal.
    2.  Di `Center`: Menyusun `Text` sambutan dan `GridView` secara vertikal.
    3.  Di `InfoCard`: Menyusun `Text` judul dan `Text` konten secara vertikal.
    4.  Di `ItemCard`: Menyusun `Icon` dan `Text` nama item secara vertikal.
- **`Row`**:
  - **Fungsi:** Menyusun widget-widget child secara **horizontal** (dari kiri ke kanan).
  - **Penggunaan:** Di `MyHomePage`, digunakan untuk menyusun ketiga `InfoCard` (NPM, Nama, Kelas) secara berdampingan.
- **`Center`**:
  - **Fungsi:** Memosisikan widget child di tengah-tengah area yang tersedia.
  - **Penggunaan:**
    1.  Di `MyHomePage`: Memastikan `Column` (yang berisi teks sambutan dan grid) berada di tengah layar.
    2.  Di `ItemCard`: Memastikan `Column` (ikon dan teks) berada di tengah kartu.
- **`Padding`**:
  - **Fungsi:** Memberikan ruang kosong (jarak) di sekeliling widget child.
  - **Penggunaan:**
    1.  Membungkus `body` utama untuk memberi jarak 16.0 di semua sisi.
    2.  Membungkus `Text` sambutan untuk memberi jarak 16.0 di atasnya.
    3.  Di dalam `ItemCard`, memberi jarak 3.0 antara ikon dan teks.
- **`SizedBox`**:
  - **Fungsi:** Membuat sebuah kotak dengan ukuran tertentu. Sering digunakan sebagai pemberi jarak (spacer).
  - **Penggunaan:**
    1.  Di `MyHomePage`: Memberi jarak vertikal 16.0 antara `Row` info dan `Center`.
    2.  Di `InfoCard`: Memberi jarak vertikal 8.0 antara `Text` judul dan `Text` konten.
- **`GridView`** (via `GridView.count`):
  - **Fungsi:** Menyusun widget-widget child dalam bentuk _grid_. `GridView.count` secara spesifik memungkinkan untuk menentukan jumlah kolom (`crossAxisCount: 3`).

### d\. Widget Kontainer & Tampilan (Containers & Display)

- **`Container`**:
  - **Fungsi:** Sebuah kotak yang bisa diatur `padding`, `width`, `height`, dekorasi, dll.
  - **Penggunaan:**
    1.  Di `InfoCard`: Membungkus `Column` untuk memberi `padding` 16.0 dan mengatur lebarnya (`width`) secara responsif menggunakan `MediaQuery`.
    2.  Di `ItemCard`: Membungkus `Column` (ikon dan teks) untuk memberi `padding` 8.0.
- **`Card`**:
  - **Fungsi:** Membuat sebuah panel (kartu) dengan gaya Material Design, lengkap dengan sudut melengkung dan bayangan (`elevation`).
  - **Penggunaan:** Di `InfoCard`, ini adalah widget dasar yang membungkus konten informasi.
- **`Material`**:
  - **Fungsi:** Menyediakan "permukaan" Material Design.
  - **Penggunaan:** Di `ItemCard`, ini digunakan untuk memberi warna latar belakang (`item.color`) dan membuat sudut melengkung (`borderRadius`) pada kartu menu.
- **`Text`**:
  - **Fungsi:** Menampilkan string (teks) di layar.
  - **Penggunaan:** Digunakan di banyak tempat: menampilkan judul `AppBar`, teks sambutan, judul dan konten di `InfoCard`, serta nama item di `ItemCard`.
- **`Icon`**:
  - **Fungsi:** Menampilkan sebuah ikon grafis.
  - **Penggunaan:** Di `ItemCard`, untuk menampilkan ikon menu (seperti `Icons.shopping_bag`).

### e\. Widget Interaktif (Interactive)

- **`InkWell`**:
  - **Fungsi:** Membuat widget anaknya menjadi interaktif (bisa diklik) dan memberikan _ripple effect_ khas Material Design saat disentuh.
  - **Penggunaan:** Di `ItemCard`, ini membungkus `Container` agar seluruh area kartu bisa diklik (`onTap`) untuk memunculkan `SnackBar`.

## 3\. Fungsi MaterialApp

`MaterialApp` adalah widget fundamental yang membungkus banyak fungsionalitas inti yang dibutuhkan oleh sebagian besar aplikasi. Widget ini mengimplementasikan **Material Design**, yaitu sistem desain visual dari Google.

**Fungsi utamanya adalah menyediakan:**

1.  **Navigasi (Routing):** Mengelola tumpukan layar (pages/routes) sehingga bisa berpindah antar halaman (misalnya, `Navigator.push`).
2.  **Theming (Tema):** Menyediakan data tema (seperti warna primer, jenis font, tema mode gelap/terang) ke seluruh widget di bawahnya.
3.  **Lokalisasi (i18n):** Dukungan untuk berbagai bahasa dan format regional.
4.  **Builder Dasar:** Menyediakan fungsionalitas dasar yang diharapkan oleh widget Material lain (seperti `Scaffold`, `AppBar`, `Dialog`).

**Mengapa sering jadi Root Widget?**
`MaterialApp` digunakan sebagai _root_ dari aplikasi karena widget-widget lain di dalam aplikasi (seperti `Scaffold` atau `TextButton`) perlu "mencari ke atas" (lookup) di dalam widget tree untuk menemukan dan menggunakan fungsionalitas inti ini (seperti `Navigator` atau `ThemeData`).

Jika aplikasi tidak dibungkus dengan `MaterialApp` (atau `CupertinoApp` untuk gaya iOS), banyak widget umum tidak akan berfungsi dengan benar.

## 4\. StatelessWidget vs. StatefulWidget

Ini adalah perbedaan paling mendasar dalam membangun widget di Flutter.

### StatelessWidget

- **Apa itu?** Widget yang **tidak dapat diubah (immutable)**. Setelah dibuat, properti dan tampilannya tidak bisa berubah _dari dalam dirinya sendiri_.
- **Karakteristik:** Tidak memiliki "State" (keadaan) internal. Tampilannya murni ditentukan oleh konfigurasi yang diterimanya dari parent-nya.
- **Metode Utama:** `build()`.
- **Kapan digunakan?** Gunakan **StatelessWidget** saat UI _tidak perlu berubah_ berdasarkan interaksi pengguna atau data internal. Contoh: Ikon, label teks statis, atau tombol yang hanya melaporkan klik tapi tidak mengubah tampilannya sendiri.

### StatefulWidget

- **Apa itu?** Widget yang **dapat diubah (mutable)** dan dinamis. Tampilannya bisa berubah selama _runtime_ (saat aplikasi berjalan).
- **Karakteristik:** Memiliki objek `State` internal yang bisa menyimpan data. Ketika data di dalam `State` berubah (dengan memanggil `setState()`), Flutter akan **membangun ulang (rebuild)** widget tersebut dengan data baru.
- **Metode Utama:** `createState()` (untuk membuat objek State) dan `build()` (di dalam kelas State).
- **Kapan digunakan?** Gunakan **StatefulWidget** saat UI perlu berubah. Contoh: Checkbox yang bisa dicentang, slider yang bisa digeser, _text field_ tempat pengguna mengetik, atau layar yang menampilkan data yang sedang di-load dari internet.

**Singkatnya:** Jika widget perlu "mengingat" sesuatu (seperti dicentang atau tidak, teks yang sedang diketik, atau data yang sedang dimuat), gunakan `StatefulWidget`. Jika tidak, gunakan `StatelessWidget`.

## 5\. BuildContext

**Apa itu BuildContext?**
`BuildContext` adalah "lokasi" atau "alamat" dari sebuah widget di dalam widget tree. Setiap widget mendapatkan `BuildContext`-nya sendiri sebagai parameter di dalam metode `build(BuildContext context)`.

**Mengapa Penting?**
`BuildContext` sangat penting karena inilah cara sebuah widget berinteraksi dengan widget lain di dalam tree, terutama dengan **ancestors (parent-parent di atasnya)**.

Ia digunakan untuk "meminta" atau "mencari" layanan atau data dari widget yang berada _di atasnya_ dalam tree.

**Bagaimana Penggunaannya di Metode `build`?**
Di dalam metode `build`, menggunakan `context` digunakan untuk:

1.  **Mendapatkan Tema:**
    `Theme.of(context).primaryColor`
2.  **Navigasi:**
    `Navigator.of(context).push(newPage)`
3.  **Menampilkan SnackBar:**
    `ScaffoldMessenger.of(context).showSnackBar(...)`

Tanpa `BuildContext`, sebuah widget akan terisolasi dan tidak tahu di mana posisinya atau bagaimana cara mengakses layanan utama seperti Tema atau Navigator.

## 6\. Hot Reload vs. Hot Restart

Ini adalah dua fitur produktivitas utama di Flutter.

### Hot Reload

- **Apa itu?** Proses menginjeksikan file kode Dart yang sudah diperbarui ke dalam **Dart Virtual Machine (VM)** yang sedang berjalan.
- **Bagaimana cara kerjanya?** Flutter akan **membangun ulang (rebuild)** widget tree dengan cepat.
- **Apa yang terjadi?**
  - UI diperbarui secara instan (biasanya dalam \< 1 detik).
  - **State (keadaan) aplikasi tetap terjaga.** Jika sedang mengisi formulir di halaman ketiga, tampilan akan tetap di halaman ketiga dan teks di formulir itu tidak hilang.
- **Kapan digunakan?** Sempurna untuk mengubah UI, memperbaiki layout, mengubah warna, atau logika tampilan.

### Hot Restart

- **Apa itu?** Proses memuat ulang seluruh kode aplikasi dan **memulai ulang Dart VM**.
- **Bagaimana cara kerjanya?** Ini seperti menghentikan dan menjalankan ulang aplikasi, tetapi jauh lebih cepat daripada "Full Restart" (menutup paksa aplikasi).
- **Apa yang terjadi?**
  - UI diperbarui dengan kode terbaru.
  - **State (keadaan) aplikasi di-reset.** Aplikasi akan kembali ke keadaan awal (halaman utama), dan semua data di memori hilang.
- **Kapan digunakan?** Ini digunakan ketika perubahan terlalu besar untuk Hot Reload, misalnya:
  - Mengubah data `static` atau global.
  - Mengubah konstruktor widget yang sudah ada.
  - Jika Hot Reload gagal atau aplikasi menjadi janggal setelah Hot Reload.

**Ringkasan Perbedaan:**

| Fitur           | Kecepatan              | State Aplikasi     | Kapan Digunakan                                              |
| :-------------- | :--------------------- | :----------------- | :----------------------------------------------------------- |
| **Hot Reload**  | Sangat Cepat (\< 1d)   | **Tetap Terjaga**  | Perubahan UI, layout, logika minor.                          |
| **Hot Restart** | Cepat (beberapa detik) | **Direset/Hilang** | Perubahan besar, mengubah state, atau saat Hot Reload gagal. |

</details>

<details> 
<summary>Tugas Individu 8</summary>

### 1. Perbedaan `Navigator.push()` dan `Navigator.pushReplacement()`

Kedua metode ini digunakan untuk berpindah antar halaman (Route), namun memiliki perilaku yang berbeda terhadap _stack_ (tumpukan) navigasi.

- **`Navigator.push()`**: Menambahkan rute baru ke _atas_ stack navigasi saat ini. Pengguna dapat kembali ke halaman sebelumnya dengan menekan tombol _back_ (di Android) atau tombol kembali di `AppBar`.

  - **Kapan digunakan di Majulah Shop?** Gunakan ini ketika pengguna bisa kembali ke halaman sebelumnya. Contohnya, jika pengguna menekan salah satu produk untuk melihat detailnya, gunakan `push()` agar mereka bisa kembali ke daftar produk setelah selesai melihat detail.

- **`Navigator.pushReplacement()`**: Mengganti rute saat ini dengan rute baru di stack navigasi. Halaman sebelumnya dibuang dari stack, sehingga pengguna _tidak bisa_ kembali ke halaman tersebut dengan tombol _back_.
  - **Kapan digunakan di Majulah Shop?** Ini sangat tepat digunakan untuk navigasi menu utama seperti yang sudah diimplementasikan di `LeftDrawer` dan `ItemCard` untuk "Create Product". Saat berpindah dari halaman "Home" ke "Create Product" melalui drawer, tombol _back_ membawa pengguna kembali ke menu drawer yang terbuka, melainkan langsung keluar aplikasi atau ke halaman utama yang sebenarnya.

### 2. Pemanfaatan Hierarchy Widget untuk Konsistensi

Dalam aplikasi Majulah Shop, kombinasi `Scaffold`, `AppBar`, dan `Drawer` digunakan untuk menciptakan kerangka (skeleton) halaman yang seragam:

- **`Scaffold`**: Ini adalah fondasi utama setiap halaman. Baik `MyHomePage` maupun `ProductFormPage` menggunakan widget ini sebagai root dari tampilan. `Scaffold` menyediakan struktur dasar visual Material Design yang secara otomatis mengatur penempatan `AppBar`, `body`, dan `drawer`.
- **`AppBar`**: Dengan menggunakan `AppBar` di dalam `Scaffold` pada setiap halaman memastikan setiap layar memiliki judul di posisi yang sama. Di `menu.dart`, `AppBar` menampilkan judul "Majulah Shop", sedangkan di `product_form.dart` menampilkan "Add Product Form". Konsistensi ini memudahkan pengguna mengenali konteks halaman.
- **`Drawer` (LeftDrawer)**: Dengan menggunakan widget yang sama pada properti `drawer` di kedua halaman (`MyHomePage` dan `ProductFormPage`) menjamin menu navigasi selalu sama dimanapun pengguna berada.

### 3. Kelebihan Layout Widget pada Form

Dalam desain antarmuka, khususnya form, widget layout berikut sangat penting:

- **`Padding`**: Memberikan jarak antara elemen dengan elemen lain atau dengan tepi layar agar tampilan tidak terkesan padat dan lebih mudah dibaca.
  - _Contoh di aplikasi:_ Setiap `TextFormField` (seperti Name, Price, Description) dengan `Padding(padding: const EdgeInsets.all(8.0), ...)` agar input field tidak menempel satu sama lain dan memiliki ruang.
- **`SingleChildScrollView`**: Memungkinkan konten untuk di-_scroll_ jika ukurannya melebihi tinggi layar. Ini sangat krusial untuk form, karena saat keyboard muncul di ponsel, area layar yang terlihat menjadi kecil. Tanpa widget ini, akan muncul error _overflow_ (garis kuning-hitam).
  - _Contoh di aplikasi:_ Seluruh isi form di `ProductFormPage` dengan `SingleChildScrollView` agar pengguna tetap bisa mengisi form meski menggunakan perangkat berlayar kecil.
- **`ListView`**: Mirip dengan `SingleChildScrollView` tetapi lebih optimal untuk daftar item yang panjang atau dinamis.
  - _Contoh di aplikasi:_ `LeftDrawer` untuk menyusun daftar menu navigasi (`ListTile` untuk Home dan Create Product) secara vertikal.

### 4. Penyesuaian Warna Tema (Branding)

Penyesuaian warna tema agar aplikasi memiliki identitas visual yang konsisten dilakukan secara terpusat melalui widget `MaterialApp` di file `main.dart`.

- **Tema Global:** Warna tema didefinisikan melalui `ThemeData` di `main.dart` dengan menggunakan `ColorScheme.fromSwatch(primarySwatch: Colors.red)` yang menjadi warna dasar brand toko.
- **Penerapan pada Widget:**
  - **AppBar:** Di `menu.dart`, `AppBar` dikonfigurasi untuk mengambil warna langsung dari skema tema utama menggunakan `Theme.of(context).colorScheme.primary`.
  - **Drawer:** Bagian header pada `LeftDrawer` juga diatur langsung dari tema global, memastikan untuk selalu selaras jika warna brand utama berubah.
  - **Form Halaman:** Halaman `ProductFormPage` menyesuaikan identitas visual dengan menggunakan `Colors.redAccent` pada `AppBar` untuk tetap memberikan nuansa merah yang konsisten.
  </details>
