# 📚 Sistem Pengambilan Mata Kuliah  

## 📖 Deskripsi  
Program ini adalah simulasi sistem akademik sederhana menggunakan bahasa pemrograman **Java**.  
Mahasiswa dapat mengambil mata kuliah yang diampu oleh dosen tertentu, lalu menampilkan daftar mata kuliah yang diambil.  

---

## 🏗️ Struktur Program  
- **Dosen.java** → menyimpan data dosen.  
- **MataKuliah.java** → menyimpan data mata kuliah.  
- **Mahasiswa.java** → menyimpan data mahasiswa dan daftar mata kuliah yang diambil.  
- **App.java** → kelas utama untuk menjalankan program.  

---

## 🔹 Diagram Kelas  
```text
+-----------+         +--------------+        +----------+
|   Dosen   |         |  MataKuliah  |        | Mahasiswa|
+-----------+         +--------------+        +----------+
| - nama    |         | - kodeMK     |        | - nama   |
| - nip     |         | - namaMK     |        | - nim    |
+-----------+         | - sks        |        | - listMK |
| +getInfo()|         | - dosen      |        +----------+
+-----------+         +--------------+       
