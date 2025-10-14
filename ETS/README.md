
# 🧾  PROGRAM VENDING MACHINE

## 📖 Deskripsi
Program ini adalah simulasi **Vending Machine** menggunakan bahasa pemrograman **Java**.
Pengguna dapat melihat daftar snack yang tersedia, memilih produk, melakukan pembayaran, dan menerima kembalian.
Program juga mencatat semua aktivitas transaksi ke dalam log, serta memberikan peringatan apabila stok snack habis.

## 🏗️ Struktur Program
Program dibagi menjadi dua kelas utama:

### 1. `VendingMachine`  
Kelas ini merepresentasikan mesin penjual snack.  
Memiliki atribut dan method untuk menampilkan menu, memproses pembelian, mengatur stok, serta mencatat log transaksi.

**Atribut:**
- `snackTypes[]` → Menyimpan nama snack yang tersedia  
- `snackPrices[]` → Menyimpan harga tiap snack  
- `snackStock[]` → Menyimpan jumlah stok tiap produk  
- `transactionLog[]` → Menyimpan catatan transaksi  
- `logCount` → Menyimpan jumlah log transaksi  

### 2. `Main`  
Kelas ini berfungsi untuk menjalankan program dan berinteraksi dengan pengguna.  
Di dalamnya, pengguna dapat memilih snack, memasukkan uang, dan melihat hasil transaksi.

**Fungsi utama:**
- Membuat objek `VendingMachine`  
- Menampilkan menu produk kepada pengguna  
- Menerima input pilihan snack dan uang dari pengguna  
- Menjalankan proses pembelian melalui method `buySnack()`  
- Menampilkan semua log transaksi di akhir program
  
## 📜 Code
```java
import java.util.Scanner;

class VendingMachine { 
    // Atribut untuk menyimpan jenis snack, harga, dan stok
    String[] snackTypes = {"Chitato", "Tango Wafer", "KitKat", "Oreo", "SilverQueen", "Yupi Boolicious"}; 
    double[] snackPrices = {8000.0, 6000.0, 7000.0, 7500.0, 12000.0, 9000.0}; 
    int[] snackStock = {8, 8, 5, 3, 2, 10}; // stok awal setiap snack
    
    String[] transactionLog = new String[100]; // menyimpan riwayat transaksi
    int logCount = 0; // menghitung jumlah log

    // Menampilkan menu
    void showMenu() { 
        System.out.println("\n=== Selamat datang di Vending Machine ===");
        System.out.println("Menu Snack:");
        for (int i = 0 ; i < snackTypes.length; i++) {
            System.out.println((i + 1) + ". " + snackTypes[i] + " - Rp " + snackPrices[i] + " (Stok: " + snackStock[i] + ")");
        }
    }

    // Proses pembelian snack
    void buySnack(int choice, double money) {
        if (choice < 1 || choice > snackTypes.length) {
            System.out.println("Pilihan tidak valid. Silakan coba lagi.");
            return;
        }

        int index = choice - 1;
        String snack = snackTypes[index];
        double price = snackPrices[index];

        // Jika stok habis
        if (snackStock[index] <= 0) {
            System.out.println("Maaf, stok " + snack + " habis! Silakan pilih produk lain.");
            addLog("Gagal membeli " + snack + " - stok habis.");
            return;
        }

        // Tampilkan total harga
        System.out.println("Total harga " + snack + " adalah Rp " + price + ".");

        // Verifikasi pembayaran
        if (money >= price) {
            double change = money - price;
            snackStock[index]--; // kurangi stok
            System.out.println("Pembayaran berhasil! Anda membeli " + snack + ".");
            System.out.println("Kembalian Anda: Rp " + change);
            System.out.println("Terima kasih sudah membeli snack!");

            addLog("Berhasil membeli " + snack + " - Harga: Rp " + price + " | Kembalian: Rp " + change);

            // Jika stok jadi 0, beri peringatan admin
            if (snackStock[index] == 0) {
                System.out.println("Stok " + snack + " habis, harap refill!");
                addLog("Peringatan: stok " + snack + " habis, perlu refill!");
            }
        } else {
            System.out.println("Uang Anda tidak cukup untuk membeli " + snack + ". Harga: Rp " + price + ".");
            addLog("Gagal membeli " + snack + " - uang tidak cukup (uang: Rp " + money + ")");
        }
    }

    // Menambah log transaksi
    void addLog(String message) {
        transactionLog[logCount] = message;
        logCount++;
    }

    // Menampilkan semua log
    void showLogs() {
        System.out.println("\n=== Log Transaksi ===");
        if (logCount == 0) {
            System.out.println("Belum ada transaksi.");
        } else {
            for (int i = 0; i < logCount; i++) {
                System.out.println((i + 1) + ". " + transactionLog[i]);
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        VendingMachine vendingMachine = new VendingMachine();
        Scanner scanner = new Scanner(System.in);

        boolean lanjut = true;

        while (lanjut) {
            vendingMachine.showMenu();

            System.out.print("\nPilih snack (1-6) atau 0 untuk keluar: ");
            int choice = scanner.nextInt();

            if (choice == 0) {
                lanjut = false;
                break;
            }

            System.out.print("Masukkan uang Anda (Rp): ");
            double money = scanner.nextDouble();

            vendingMachine.buySnack(choice, money);

            System.out.println("\nIngin membeli lagi? (y/n): ");
            char ulang = scanner.next().charAt(0);
            if (ulang == 'n' || ulang == 'N') {
                lanjut = false;
            }
        }

        // Tampilkan semua log setelah selesai
        vendingMachine.showLogs();
        System.out.println("\nTerima kasih telah menggunakan mesin snack kami!");
        scanner.close();
    }
}
```
## 📤 Output Program



