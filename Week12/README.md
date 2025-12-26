# 🚗 Aplikasi Rental Kendaraan 🚲🏍️

## 📖 Deskripsi
Aplikasi **Rental Kendaraan** merupakan sebuah sistem manajemen sederhana yang digunakan untuk mengelola berbagai jenis kendaraan yang tersedia untuk disewa, seperti **Mobil**, **Motor**, dan **Sepeda**.  
Aplikasi ini menerapkan konsep **Object-Oriented Programming (OOP)** khususnya **inheritance (pewarisan)**, di mana setiap jenis kendaraan memiliki atribut dan karakteristik yang berbeda.

Fungsi utama aplikasi ini adalah:
1. Menampilkan daftar kendaraan yang tersedia untuk disewa.
2. Menyimpan dan menampilkan data penyewa beserta informasi detail kendaraan yang disewa.
3. Menerapkan konsep inheritance dan polymorphism dalam bahasa Java.

Aplikasi ini dibuat menggunakan **Java (BlueJ)**.

---

## 🏗️ Struktur Kelas (Class Diagram)
<img width="882" height="690" alt="image" src="https://github.com/user-attachments/assets/049ec8eb-08d3-4996-8267-f595d43fd5c5" />

### Kelas RentalApp
``
import java.util.ArrayList;

public class RentalApp {
    public static void main(String[] args) {

        ArrayList<Kendaraan> daftarKendaraan = new ArrayList<>();

        daftarKendaraan.add(new Mobil("Toyota", "Avanza", 2022, 4));
        daftarKendaraan.add(new Motor("Honda", "Vario", 2021, 2));
        daftarKendaraan.add(new Sepeda("Polygon", "Xtrada", 2020, "Gunung"));

        System.out.println("=== DAFTAR KENDARAAN TERSEDIA ===");
        for (Kendaraan k : daftarKendaraan) {
            System.out.println(k.getInfo());
        }

        ArrayList<Penyewa> daftarPenyewa = new ArrayList<>();
        daftarPenyewa.add(new Penyewa("Andi", daftarKendaraan.get(0)));
        daftarPenyewa.add(new Penyewa("Budi", daftarKendaraan.get(2)));

        System.out.println("\n=== DAFTAR PENYEWA ===");
        for (Penyewa p : daftarPenyewa) {
            p.tampilkanInfo();
        }
    }
}

``  

### Kelas Kendaraan
``
public class Kendaraan {
    protected String merk;
    protected String model;
    protected int tahunProduksi;

    public Kendaraan(String merk, String model, int tahunProduksi) {
        this.merk = merk;
        this.model = model;
        this.tahunProduksi = tahunProduksi;
    }

    public String getInfo() {
        return "Merk: " + merk +
               ", Model: " + model +
               ", Tahun: " + tahunProduksi;
    }
}
``

### Kelas Mobil
``
public class Mobil extends Kendaraan {
    private int jumlahRoda;

    public Mobil(String merk, String model, int tahunProduksi, int jumlahRoda) {
        super(merk, model, tahunProduksi);
        this.jumlahRoda = jumlahRoda;
    }

    @Override
    public String getInfo() {
        return "Mobil | " + super.getInfo() +
               ", Jumlah Roda: " + jumlahRoda;
    }
}
``

### Kelas Motor
``
public class Motor extends Kendaraan {
    private int jumlahRoda;

    public Motor(String merk, String model, int tahunProduksi, int jumlahRoda) {
        super(merk, model, tahunProduksi);
        this.jumlahRoda = jumlahRoda;
    }

    @Override
    public String getInfo() {
        return "Motor | " + super.getInfo() +
               ", Jumlah Roda: " + jumlahRoda;
    }
}
``

### Kelas Sepeda
``
public class Sepeda extends Kendaraan {
    private String jenisSepeda;

    public Sepeda(String merk, String model, int tahunProduksi, String jenisSepeda) {
        super(merk, model, tahunProduksi);
        this.jenisSepeda = jenisSepeda;
    }

    @Override
    public String getInfo() {
        return "Sepeda | " + super.getInfo() +
               ", Jenis: " + jenisSepeda;
    }
}
``

### Kelas Penyewa
``
public class Penyewa {
    private String nama;
    private Kendaraan kendaraanDisewa;

    public Penyewa(String nama, Kendaraan kendaraanDisewa) {
        this.nama = nama;
        this.kendaraanDisewa = kendaraanDisewa;
    }

    public void tampilkanInfo() {
        System.out.println("Nama Penyewa: " + nama);
        System.out.println("Kendaraan Disewa: " + kendaraanDisewa.getInfo());
        System.out.println("----------------------------------");
    }
}
``


