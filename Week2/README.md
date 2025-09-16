# 🎟️ TUGAS MEMBUAT CODE STRUKTUR TICKET MACHINE

## 📖 Deskripsi
Program ini adalah **simulasi mesin tiket konser** sederhana menggunakan bahasa pemrograman **Java**.  
Pengguna dapat memilih kategori tiket, menentukan jumlah tiket, menghitung total harga, melakukan pembayaran, hingga menerima kembalian.

## 🏗️ Struktur Program
Program dibagi menjadi beberapa kelas:
1. **Ticket**  
   - Menyimpan data kategori dan harga tiket.  
   - Memiliki method `getCategory()` dan `getPrice()` untuk mengambil data.  

2. **TicketMachine**  
   - Menyimpan daftar tiket yang tersedia (Regular, VIP, VVIP).  
   - Menampilkan daftar tiket dengan `displayTickets()`.  
   - Mengambil tiket berdasarkan pilihan pengguna dengan `getTicket()`.  

3. **ConcertTicketMachine (Main Class)**  
   - Menjalankan program utama.  
   - Interaksi dengan pengguna (input kategori tiket, jumlah tiket, pembayaran).  
   - Menghitung total harga dan menampilkan hasil transaksi.  

## 📜 Code
import java.util.Scanner;

// Kelas untuk tiket
class Ticket {
    private String category;
    private int price;

    public Ticket(String category, int price) {
        this.category = category;
        this.price = price;
    }

    public String getCategory() {
        return category;
    }

    public int getPrice() {
        return price;
    }
}

// Kelas untuk mesin tiket
class TicketMachine {
    private Ticket[] tickets;

    public TicketMachine() {
        // Inisialisasi kategori tiket dan harga
        tickets = new Ticket[] {
                new Ticket("Regular", 500000),
                new Ticket("VIP", 1000000),
                new Ticket("VVIP", 1500000)
        };
    }

    public void displayTickets() {
        System.out.println("Daftar Kategori Tiket:");
        for (int i = 0; i < tickets.length; i++) {
            System.out.printf("%d. %s - Rp %,d%n", i + 1, tickets[i].getCategory(), tickets[i].getPrice());
        }
    }

    public Ticket getTicket(int choice) {
        if (choice >= 1 && choice <= tickets.length) {
            return tickets[choice - 1];
        }
        return null; // Jika pilihan tidak valid
    }
}

// Kelas utama
public class ConcertTicketMachine {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        TicketMachine machine = new TicketMachine();

        System.out.println("Selamat datang di Ticket Machine Konser!");

        // Tampilkan tiket
        machine.displayTickets();

        // Pilih kategori tiket
        System.out.print("Masukkan nomor kategori tiket pilihan Anda: ");
        int choice = scanner.nextInt();
        Ticket selectedTicket = machine.getTicket(choice);

        if (selectedTicket == null) {
            System.out.println("Pilihan tidak valid. Silakan coba lagi.");
            return;
        }

        // Jumlah tiket
        System.out.print("Masukkan jumlah tiket yang ingin dibeli: ");
        int ticketCount = scanner.nextInt();

        if (ticketCount <= 0) {
            System.out.println("Jumlah tiket tidak valid.");
            return;
        }

        // Hitung total
        int totalPrice = selectedTicket.getPrice() * ticketCount;
        System.out.printf("Total harga: Rp %,d%n", totalPrice);

        // Pembayaran
        System.out.print("Masukkan jumlah uang pembayaran: Rp ");
        int payment = scanner.nextInt();

        if (payment < totalPrice) {
            System.out.println("Uang Anda tidak mencukupi. Transaksi dibatalkan.");
        } else {
            int change = payment - totalPrice;
            System.out.printf("Pembayaran berhasil! Kembalian Anda: Rp %,d%n", change);
            System.out.println("Terima kasih telah membeli tiket konser!");
        }

        scanner.close();
    }
}
