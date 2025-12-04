# 📚 World of Zuul - Game Petualangan Berbasis Teks 🎮

## 📖 Deskripsi
**World of Zuul** adalah permainan petualangan berbasis teks yang konsepnya mirip dengan game eksplorasi zaman dulu, tetapi sepenuhnya dikendalikan melalui perintah yang diketik oleh pemain. Game ini tidak menggunakan tampilan grafis atau visual, melainkan seluruh interaksi dilakukan lewat terminal atau console.

Pemain dapat menjelajahi berbagai ruangan yang saling terhubung, dan latar permainan ini digambarkan seperti area universitas. Untuk bergerak atau berinteraksi, pemain hanya perlu memasukkan perintah tertentu seperti:
- **"go"** untuk berpindah ruangan,
- **"help"** untuk melihat daftar perintah yang bisa digunakan,
- **"quit"** untuk keluar dari permainan.

Setiap ruangan dalam game memiliki kemungkinan arah perpindahan ke ruangan lain, seperti **north**, **east**, **south**, dan **west**. Jadi, saat pemain mengetik perintah seperti **"go north"**, permainan akan memindahkan pemain ke ruangan yang berada di arah utara jika tersedia.

Meskipun konsep eksplorasinya sederhana, game ini cukup efektif untuk memahami struktur logika pemrograman berbasis objek.

---

## 🏗️ Struktur Kelas

### 1. **Kelas `Game`**
Kelas **`Game`** adalah pusat dari permainan ini. Kelas ini menangani jalannya permainan, menerima input dari pemain, dan menentukan aksi yang harus dilakukan berdasarkan perintah yang diberikan oleh pemain. Bisa dibilang, kelas ini adalah otak utama dari permainan.

### 2. **Kelas `Room`**
Kelas **`Room`** digunakan untuk merepresentasikan setiap ruangan dalam permainan. Setiap ruangan bisa memiliki koneksi ke ruangan lain melalui arah **north**, **east**, **south**, atau **west**. Di sinilah struktur peta permainan ditentukan.

### 3. **Kelas `Command`**
Kelas **`Command`** digunakan untuk menyimpan perintah yang dimasukkan oleh pemain. Perintah-perintah ini dikemas dalam bentuk objek agar lebih mudah diolah oleh sistem. Misalnya, perintah **"go north"** akan dipisah antara kata utama (**"go"**) dan argumennya (**"north"**).

### 4. **Kelas `Parser`**
Kelas **`Parser`** bertugas membaca input yang dimasukkan oleh pemain di console dan mengubahnya menjadi objek **`Command`**. Kelas ini dapat diibaratkan sebagai penerjemah dari teks yang dimasukkan pemain ke dalam format yang bisa dipahami oleh program.

### 5. **Kelas `CommandWords`**
Kelas **`CommandWords`** menyimpan daftar kata perintah yang valid dalam permainan, seperti **"go"**, **"quit"**, dan **"help"**. Dengan adanya kelas ini, **`Parser`** dapat mengecek apakah input pemain termasuk perintah yang valid atau tidak.

---

