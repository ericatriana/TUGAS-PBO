# 🌱 Laporan Latihan Abstract Class Java

## 📖 Deskripsi
Laporan ini membahas implementasi **Abstract Class** dalam bahasa pemrograman **Java (BlueJ)** melalui dua latihan utama:

1. Implementasi abstract class **MakhlukHidup** yang diturunkan menjadi **Manusia**, **Hewan**, dan **Tumbuhan**.
2. Studi kasus simulasi **Foxes and Rabbits**, dengan mengubah struktur class umum menjadi **abstract class** untuk meningkatkan fleksibilitas dan penerapan konsep Object-Oriented Programming (OOP).

Tujuan dari latihan ini adalah untuk memahami penggunaan abstract class, inheritance, dan polymorphism dalam Java.

---

## 🔹 Latihan 1  
### Abstract Class Makhluk Hidup

### 🏗️ Struktur Kelas
<img width="800" height="688" alt="image" src="https://github.com/user-attachments/assets/b665794d-b9ba-4956-aeaf-407acd17e731" />

### Kelas MakhlukHidup
``
public abstract class MakhlukHidup {
    protected String nama;

    public MakhlukHidup(String nama) {
        this.nama = nama;
    }

    public void bernapas() {
        System.out.println(nama + " sedang bernapas");
    }

    public void tumbuh() {
        System.out.println(nama + " sedang tumbuh");
    }

    public abstract void bergerak();
}
``

### Kelas Hewan
``
public class Hewan extends MakhlukHidup {

    public Hewan(String nama) {
        super(nama);
    }

    @Override
    public void bergerak() {
        System.out.println(nama + " bergerak dengan berlari");
    }
}
``

### Kelas Manusia
``
public class Manusia extends MakhlukHidup {

    public Manusia(String nama) {
        super(nama);
    }

    @Override
    public void bergerak() {
        System.out.println(nama + " bergerak dengan berjalan");
    }
}
``

### Kelas Tumbuhan
``
public class Tumbuhan extends MakhlukHidup {

    public Tumbuhan(String nama) {
        super(nama);
    }

    @Override
    public void bergerak() {
        System.out.println(nama + " bergerak dengan tumbuh ke arah cahaya");
    }
}
``

### Kelas Main
``
public class Main {
    public static void main(String[] args) {

        MakhlukHidup manusia = new Manusia("Andi");
        MakhlukHidup hewan = new Hewan("Kucing");
        MakhlukHidup tumbuhan = new Tumbuhan("Pohon Mangga");

        manusia.bernapas();
        manusia.bergerak();

        hewan.bernapas();
        hewan.bergerak();

        tumbuhan.bernapas();
        tumbuhan.bergerak();
    }
}
``

