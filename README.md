# Session 4 : Lab Activity 2 - State Management
---
### Nama: Chaiden Richardo Foanto  
### NIM: 0806022310023  
### Mata Kuliah: Visual Programming - Flutter  

---
# Ephemeral State Management & App State Management in Flutter

## Project Overview
Tugas ini terdiri dari dua bagian, yaitu:
1. **Ephemeral State Management** yang menggunakan `StatefulWidget`.
2. **App State Management** yang menggunakan `scoped_model` untuk menangani state di seluruh aplikasi.

### Notes
Di part 2, yaitu pada bagian App State Management, saya menggunakan package `scoped_model`. Pda saat menambahkan dependency `scoped_model` dengan versi `^5.0.0` di `pubspec.yaml`, kemudian menjalankan perintah `flutter pub get` terjadi error:

```plaintext
sh-3.2$ flutter pub get
Resolving dependencies... 
Because app_state_codelab depends on scoped_model ^5.0.0 which doesn't match any versions, version solving
  failed.


You can try the following suggestion to make the pubspec resolve:
* Consider downgrading your constraint on scoped_model: flutter pub add scoped_model:^2.0.0
```
Ini terjadi karena versi tertinggi untuk scoped_model saat ini adalah ^2.0.0, sehingga saya mengganti supaya menyesuaikan dependency menjadi scoped_model: ^2.0.0.

---

# Perbedaan Antara Ephemeral State Management dan App State Management

## Ephemeral State Management
Ephemeral state management menggunakan `StatefulWidget`, yang hanya cocok untuk state yang bersifat lokal atau sementara. Artinya, data ini hanya digunakan di dalam satu widget saja dan tidak perlu diakses oleh widget lain. Misalnya, pada aplikasi sederhana, kita menggunakan counter yang bertambah setiap kali tombol ditekan, dan data counter tersebut hanya dikelola di dalam widget `CounterWidget`.

### Kelebihan:
- **Sederhana** dan **mudah diimplementasikan** untuk kasus state yang hanya diperlukan di satu bagian kecil aplikasi.
- Cocok untuk aplikasi kecil yang hanya memiliki sedikit komponen dan tidak perlu berbagi data antar widget.

### Kekurangan:
- Tidak efisien jika aplikasi memiliki banyak komponen yang perlu berbagi state atau informasi. Jika banyak bagian aplikasi yang memerlukan data yang sama, maka setiap widget harus mengelola data itu sendiri. Ini bisa membuat aplikasi jadi rumit dan susah dikelola.
- Menjadi sulit untuk di-maintain jika state mulai tersebar di banyak widget, karena setiap widget harus mengelola state-nya sendiri.

## App State Management dengan Scoped Model
App State Management pada Part 2 menggunakan package `scoped_model`. Dengan pendekatan ini, state `counter` dideklarasikan dalam model (`CounterModel`) yang dapat diakses oleh widget mana saja dalam aplikasi. Model ini bisa diakses oleh semua widget di aplikasi. Jadi, ketika data berubah, seluruh widget yang membutuhkan data tersebut akan diperbarui secara otomatis.

### Kelebihan:
- **State dapat dibagikan** ke seluruh aplikasi, membuat model ini sangat efisien untuk aplikasi besar yang memiliki banyak komponen yang perlu berinteraksi.
- Cocok untuk aplikasi yang membutuhkan pengelolaan state yang kompleks seperti **user authentication**, **keranjang belanja**, atau **pengaturan profil pengguna**.
- Memudahkan **maintenance** dan **pengembangan** aplikasi besar karena state dikelola di satu tempat.

### Kekurangan:
- Lebih kompleks daripada `StatefulWidget` untuk aplikasi kecil yang tidak memerlukan pengelolaan state secara global.
- Menggunakan scoped_model berarti aplikasi bergantung pada package ini, yang mungkin perlu pembaruan atau penyesuaian di masa yang akan datang.

## Kesimpulannya
Pada aplikasi yang simple, **Ephemeral State Management** dengan `StatefulWidget` akan menjadi pilihan yang cukup baik, karena penggunaannya lebih gampang dan direct. Namun, pada aplikasi besar yang kompleks, **App State Management** dengan `scoped_model` jauh lebih efektif. Dengan scoped model, state dapat diakses di seluruh aplikasi dan disusun dengan lebih rapi, yang penting dalam mengelola fitur yang membutuhkan data konsisten di banyak bagian aplikasi.
