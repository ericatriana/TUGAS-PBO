# 📚 Technical Support System

## 📖 Deskripsi
Aplikasi **Technical Support System** ini bertujuan untuk memberikan bantuan teknis kepada pengguna dengan menyediakan solusi untuk masalah teknis yang sering dihadapi. Aplikasi ini memungkinkan pengguna untuk menambah, melihat, mencari, dan menghapus masalah teknis yang telah tercatat dalam sistem. 

Fungsi utama aplikasi ini mencakup:
1. Menambah masalah teknis baru
2. Menampilkan daftar semua masalah teknis
3. Mencari masalah berdasarkan ID
4. Memberikan solusi untuk masalah yang terdaftar

---

## 🏗️ Struktur Kelas  
<img width="651" height="304" alt="image" src="https://github.com/user-attachments/assets/02ba7ffe-d0e2-4214-991e-bb24821b8745" />  

### 1. Kelas TechnicalIssue
Kelas ini digunakan untuk mendeskripsikan masalah teknis dengan atribut seperti ID masalah, deskripsi, dan solusi. 
```
public class TechnicalIssue {
    private String issueId;
    private String description;
    private String solution;

    // Konstruktor
    public TechnicalIssue(String issueId, String description, String solution) {
        this.issueId = issueId;
        this.description = description;
        this.solution = solution;
    }

    // Getter untuk ID masalah
    public String getIssueId() {
        return issueId;
    }

    // Getter untuk deskripsi masalah
    public String getDescription() {
        return description;
    }

    // Getter untuk solusi masalah
    public String getSolution() {
        return solution;
    }

    // Method untuk menampilkan informasi tentang masalah dan solusinya
    public void displayIssueInfo() {
        System.out.println("Masalah ID: " + issueId);
        System.out.println("Deskripsi: " + description);
        System.out.println("Solusi: " + solution);
    }
}
```
### Penjelasan
**Atribut:**
- issueId: ID masalah, digunakan untuk mengidentifikasi masalah secara unik. Ini memungkinkan sistem untuk membedakan masalah satu dengan yang lainnya.
- description: Deskripsi masalah yang dihadapi oleh pengguna. Menyediakan rincian tentang masalah yang dihadapi untuk mempermudah penyelesaian.
- solution: Solusi yang disarankan atau diberikan untuk masalah tersebut. Ini adalah langkah atau panduan yang diberikan untuk mengatasi masalah yang terjadi.

**Method:**
- displayIssueInfo(): Metode ini digunakan untuk menampilkan informasi lengkap mengenai masalah, termasuk ID, deskripsi, dan solusi yang diberikan. Hal ini membantu pengguna atau teknisi untuk mengetahui masalah secara keseluruhan.

### 2. Kelas TechnicalSupportSystem
Kelas ini digunakan untuk mendeskripsikan masalah teknis dengan atribut seperti ID masalah, deskripsi, dan solusi. 
```
import java.util.ArrayList;

public class TechnicalSupportSystem {
    private ArrayList<TechnicalIssue> issues;

    // Konstruktor untuk menginisialisasi daftar masalah teknis
    public TechnicalSupportSystem() {
        issues = new ArrayList<>();
    }

    // Menambahkan masalah teknis baru ke dalam sistem
    public void addIssue(String issueId, String description, String solution) {
        TechnicalIssue issue = new TechnicalIssue(issueId, description, solution);
        issues.add(issue);
    }

    // Menampilkan semua masalah yang ada dalam sistem
    public void displayAllIssues() {
        if (issues.isEmpty()) {
            System.out.println("Tidak ada masalah dalam sistem.");
        } else {
            for (TechnicalIssue issue : issues) {
                issue.displayIssueInfo();
                System.out.println("----------------------------");
            }
        }
    }

    // Mencari masalah berdasarkan ID dan menampilkan solusi
    public void searchIssueById(String issueId) {
        boolean found = false;
        for (TechnicalIssue issue : issues) {
            if (issue.getIssueId().equalsIgnoreCase(issueId)) {
                issue.displayIssueInfo();
                found = true;
                break;
            }
        }
        if (!found) {
            System.out.println("Masalah dengan ID " + issueId + " tidak ditemukan.");
        }
    }

    // Memberikan solusi untuk masalah tertentu
    public void provideSolution(String issueId) {
        boolean found = false;
        for (TechnicalIssue issue : issues) {
            if (issue.getIssueId().equalsIgnoreCase(issueId)) {
                System.out.println("Solusi untuk masalah ID " + issueId + ": " + issue.getSolution());
                found = true;
                break;
            }
        }
        if (!found) {
            System.out.println("Solusi untuk masalah ID " + issueId + " tidak ditemukan.");
        }
    }
}

```
### Penjelasan
**Atribut:**
- issues: Sebuah ArrayList yang menyimpan semua objek TechnicalIssue, yang merupakan daftar masalah teknis yang tercatat dalam sistem.
**Metode:**
- addIssue(): Menambahkan masalah teknis baru ke dalam daftar masalah yang disimpan dalam issues.
- displayAllIssues(): Menampilkan semua masalah yang ada dalam sistem, menggunakan displayIssueInfo() dari masing-masing objek TechnicalIssue.
- searchIssueById(): Mencari masalah berdasarkan ID dan menampilkan informasi terkait masalah yang ditemukan.
- provideSolution(): Menampilkan solusi untuk masalah tertentu berdasarkan ID yang dicari.

### 3. Kelas Main
Kelas ini digunakan untuk mendeskripsikan masalah teknis dengan atribut seperti ID masalah, deskripsi, dan solusi. 
```
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        TechnicalSupportSystem system = new TechnicalSupportSystem();

        int choice;
        do {
            // Menampilkan menu aplikasi
            System.out.println("\n=== Technical Support System ===");
            System.out.println("1. Tambah Masalah Teknis");
            System.out.println("2. Lihat Semua Masalah");
            System.out.println("3. Cari Masalah Berdasarkan ID");
            System.out.println("4. Dapatkan Solusi Masalah");
            System.out.println("5. Keluar");
            System.out.print("Pilih menu: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // clear buffer

            switch (choice) {
                case 1:
                    // Menambahkan masalah teknis baru
                    System.out.print("Masukkan ID Masalah: ");
                    String issueId = scanner.nextLine();
                    System.out.print("Masukkan Deskripsi Masalah: ");
                    String description = scanner.nextLine();
                    System.out.print("Masukkan Solusi: ");
                    String solution = scanner.nextLine();
                    system.addIssue(issueId, description, solution);
                    System.out.println("Masalah berhasil ditambahkan!");
                    break;

                case 2:
                    // Menampilkan semua masalah
                    system.displayAllIssues();
                    break;

                case 3:
                    // Mencari masalah berdasarkan ID
                    System.out.print("Masukkan ID Masalah yang dicari: ");
                    String searchId = scanner.nextLine();
                    system.searchIssueById(searchId);
                    break;

                case 4:
                    // Mendapatkan solusi untuk masalah
                    System.out.print("Masukkan ID Masalah untuk mendapatkan solusi: ");
                    String solutionId = scanner.nextLine();
                    system.provideSolution(solutionId);
                    break;

                case 5:
                    // Keluar dari aplikasi
                    System.out.println("Terima kasih telah menggunakan Technical Support System!");
                    break;

                default:
                    // Pilihan tidak valid
                    System.out.println("Pilihan tidak valid, coba lagi.");
            }
        } while (choice != 5);

        scanner.close();
    }
}

```
### Penjelasan
- Menu Interaktif: Menyediakan pilihan bagi pengguna untuk menambah masalah, mencari masalah, melihat semua masalah, atau keluar.
- Scanner: Digunakan untuk menerima input dari pengguna untuk memilih menu.
- Pengulangan: Program akan terus berjalan sampai pengguna memilih untuk keluar.

## 📋 Fitur Aplikasi
1. Tambah Masalah Teknis: Menambahkan masalah baru ke dalam sistem   
   <img width="452" height="266" alt="image" src="https://github.com/user-attachments/assets/6eff8698-8506-4b62-8ad7-48e1d3f22504" />  
2. Lihat Semua Masalah: Menampilkan daftar masalah yang ada  
   <img width="530" height="251" alt="image" src="https://github.com/user-attachments/assets/d403f117-2268-4e0f-900a-1fe287d19982" />  
3. Cari Masalah Berdasarkan ID: Mencari masalah tertentu berdasarkan ID  
   <img width="482" height="264" alt="image" src="https://github.com/user-attachments/assets/a13792a1-1a5a-4d46-af97-f9b0a2c9f49a" />  
4. Dapatkan Solusi Masalah: Menampilkan solusi untuk masalah berdasarkan ID yang dicari  
   <img width="561" height="216" alt="image" src="https://github.com/user-attachments/assets/b3f2c0b3-4566-4cea-a591-b6e6189982a1" />  
5. Keluar  
   <img width="721" height="195" alt="image" src="https://github.com/user-attachments/assets/b7ee33e7-d441-4500-9fef-d1689a5c8597" />  

