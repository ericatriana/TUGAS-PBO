# 📚 Latihan Grouping

## 📖 Deskripsi  
Pada pertemuan kali ini, kita mempelajari dan berlatih mengenai konsep grouping dengan beberapa proyek yang mencakup Personal Organizer, Library Catalog, Student Record System, dan Notebook. Tujuan dari latihan ini adalah untuk memahami cara mengelompokkan objek dalam pemrograman menggunakan konsep object-oriented programming (OOP).

---

## 📋 Project Personal Organizer
```
import java.util.ArrayList;
import java.util.Scanner;

class Task {
    private String title;
    private String description;

    // Constructor
    public Task(String title, String description) {
        this.title = title;
        this.description = description;
    }

    // Getter methods
    public String getTitle() {
        return title;
    }

    public String getDescription() {
        return description;
    }

    // Override toString() method to display task details
    @Override
    public String toString() {
        return "Judul: " + title + " | Deskripsi: " + description;
    }
}

public class PersonalOrganizer {
    public static void main(String[] args) {
        ArrayList<Task> tasks = new ArrayList<>();
        Scanner scanner = new Scanner(System.in);
        int choice;

        // Menu loop
        do {
            System.out.println("\n=== Personal Organizer ===");
            System.out.println("1. Tambah Tugas");
            System.out.println("2. Lihat Semua Tugas");
            System.out.println("3. Hapus Tugas");
            System.out.println("4. Keluar");
            System.out.print("Pilih menu: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // clear buffer

            switch (choice) {
                case 1:
                    // Add task
                    System.out.print("Masukkan judul tugas: ");
                    String title = scanner.nextLine();
                    System.out.print("Masukkan deskripsi tugas: ");
                    String description = scanner.nextLine();
                    tasks.add(new Task(title, description));
                    System.out.println("Tugas berhasil ditambahkan!");
                    break;

                case 2:
                    // View all tasks
                    System.out.println("\nDaftar Tugas:");
                    if (tasks.isEmpty()) {
                        System.out.println("Tidak ada tugas.");
                    } else {
                        for (int i = 0; i < tasks.size(); i++) {
                            System.out.println((i + 1) + ". " + tasks.get(i));
                        }
                    }
                    break;

                case 3:
                    // Remove task
                    System.out.print("Masukkan nomor tugas yang akan dihapus: ");
                    int index = scanner.nextInt();
                    if (index > 0 && index <= tasks.size()) {
                        tasks.remove(index - 1);
                        System.out.println("Tugas berhasil dihapus!");
                    } else {
                        System.out.println("Nomor tugas tidak valid.");
                    }
                    break;

                case 4:
                    // Exit the program
                    System.out.println("Terima kasih! Keluar dari aplikasi.");
                    break;

                default:
                    // Invalid choice
                    System.out.println("Pilihan tidak valid, coba lagi.");
            }
        } while (choice != 4);

        scanner.close();
    }
}
```
Project Personal Organizer dengan Java menggunakan collection (ArrayList) untuk
menyimpan data seperti Task (tugas/agenda).
Fitur Personal Organizer:
1. Menambahkan tugas baru
   <img width="504" height="221" alt="image" src="https://github.com/user-attachments/assets/2bd24826-54da-4add-9ebe-c5783f7221c8" />  
2. Menampilkan daftar tugas
   <img width="582" height="215" alt="image" src="https://github.com/user-attachments/assets/618f080a-cd2c-4f43-af47-c6d914d9516c" />  
3. Menghapus tugas berdasarkan nomor
   <img width="489" height="192" alt="image" src="https://github.com/user-attachments/assets/5047c2df-cadc-42b2-bd26-eb91c65583ff" />  
4. Keluar dari aplikasi  
   <img width="488" height="176" alt="image" src="https://github.com/user-attachments/assets/3e0d9e05-d63e-4d4f-a018-76f1cb7a5d19" />  

   

ArrayList<Task> → digunakan untuk menyimpan daftar tugas.  
Class Task → merepresentasikan objek tugas dengan atribut title dan description.  
Menu interaktif → menggunakan Scanner agar user bisa menambah, melihat, dan menghapus  
tugas.

## 📚Project Library Catalog 
```
import java.util.ArrayList;
import java.util.Scanner;

class Book {
    private String title;
    private String author;
    private int year;

    // Constructor
    public Book(String title, String author, int year) {
        this.title = title;
        this.author = author;
        this.year = year;
    }

    // Getter method
    public String getTitle() {
        return title;
    }

    // Override toString() method for displaying book details
    @Override
    public String toString() {
        return "Judul: " + title + " | Penulis: " + author + " | Tahun: " + year;
    }
}

public class LibraryCatalog {
    public static void main(String[] args) {
        ArrayList<Book> catalog = new ArrayList<>();
        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            // Display menu options
            System.out.println("\n=== Library Catalog ===");
            System.out.println("1. Tambah Buku");
            System.out.println("2. Lihat Semua Buku");
            System.out.println("3. Cari Buku");
            System.out.println("4. Hapus Buku");
            System.out.println("5. Keluar");
            System.out.print("Pilih menu: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // clear buffer

            switch (choice) {
                case 1:
                    // Add a new book
                    System.out.print("Masukkan judul buku: ");
                    String title = scanner.nextLine();
                    System.out.print("Masukkan nama penulis: ");
                    String author = scanner.nextLine();
                    System.out.print("Masukkan tahun terbit: ");
                    int year = scanner.nextInt();
                    catalog.add(new Book(title, author, year));
                    System.out.println("Buku berhasil ditambahkan!");
                    break;

                case 2:
                    // View all books
                    System.out.println("\nDaftar Buku:");
                    if (catalog.isEmpty()) {
                        System.out.println("Tidak ada buku dalam katalog.");
                    } else {
                        for (int i = 0; i < catalog.size(); i++) {
                            System.out.println((i + 1) + ". " + catalog.get(i));
                        }
                    }
                    break;

                case 3:
                    // Search for a book by title
                    System.out.print("Masukkan judul buku yang dicari: ");
                    String searchTitle = scanner.nextLine().toLowerCase();
                    boolean found = false;

                    for (Book book : catalog) {
                        if (book.getTitle().toLowerCase().contains(searchTitle)) {
                            System.out.println(book);
                            found = true;
                        }
                    }
                    if (!found) {
                        System.out.println("Buku tidak ditemukan.");
                    }
                    break;

                case 4:
                    // Delete a book by number
                    System.out.print("Masukkan nomor buku yang akan dihapus: ");
                    int index = scanner.nextInt();
                    if (index > 0 && index <= catalog.size()) {
                        catalog.remove(index - 1);
                        System.out.println("Buku berhasil dihapus!");
                    } else {
                        System.out.println("Nomor buku tidak valid.");
                    }
                    break;

                case 5:
                    // Exit the program
                    System.out.println("Keluar dari katalog. Terima kasih!");
                    break;

                default:
                    // Invalid choice
                    System.out.println("Pilihan tidak valid, coba lagi.");
            }
        } while (choice != 5);

        scanner.close();
    }
}

```
Project Library Catalog menggunakan Java Collection (ArrayList).
Fitur Library Catalog
1. Menambahkan buku baru  
   <img width="470" height="269" alt="image" src="https://github.com/user-attachments/assets/c333440a-e60a-4514-9ed5-6830aca49760" />  
2. Menampilkan semua buku  
   <img width="823" height="250" alt="image" src="https://github.com/user-attachments/assets/21501d6b-906f-462b-9673-2fde3cca724c" />   
3. Mencari buku berdasarkan judul  
   <img width="723" height="217" alt="image" src="https://github.com/user-attachments/assets/204559bd-9c18-42bb-928c-ed774556d08a" />  
4. Menghapus buku berdasarkan nomor  
   <img width="524" height="216" alt="image" src="https://github.com/user-attachments/assets/b878e03f-f05e-427c-911b-b2121ac5b1da" />  
   <img width="377" height="251" alt="image" src="https://github.com/user-attachments/assets/ef72f5e4-f8df-4322-8f60-87394a862408" />  
5. Keluar  
   <img width="451" height="188" alt="image" src="https://github.com/user-attachments/assets/ba0f2491-abc2-4b6e-9b4e-1d3205b83bfe" />  


ArrayList<Book> → menyimpan daftar buku.
Class Book → merepresentasikan objek buku dengan atribut title, author, dan year.  
Fitur Cari → menggunakan contains() agar pencarian tidak harus sama persis, cukup
sebagian judul.  
Fitur Hapus → hapus berdasarkan nomor indeks dari daftar.  

## Project Student Record System 
```
import java.util.ArrayList;
import java.util.Scanner;

class Student {
    private String nim;
    private String name;
    private String major;

    // Constructor
    public Student(String nim, String name, String major) {
        this.nim = nim;
        this.name = name;
        this.major = major;
    }

    // Getter methods
    public String getNim() {
        return nim;
    }

    public String getName() {
        return name;
    }

    public String getMajor() {
        return major;
    }

    // Override toString() method to display student details
    @Override
    public String toString() {
        return "NIM: " + nim + " | Nama: " + name + " | Jurusan: " + major;
    }
}

public class StudentRecordSystem {
    public static void main(String[] args) {
        ArrayList<Student> records = new ArrayList<>();
        Scanner scanner = new Scanner(System.in);
        int choice;

        // Menu loop
        do {
            System.out.println("\n=== Student Record System ===");
            System.out.println("1. Tambah Mahasiswa");
            System.out.println("2. Lihat Semua Mahasiswa");
            System.out.println("3. Cari Mahasiswa");
            System.out.println("4. Hapus Mahasiswa");
            System.out.println("5. Keluar");
            System.out.print("Pilih menu: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // clear buffer

            switch (choice) {
                case 1:
                    // Add a new student
                    System.out.print("Masukkan NIM: ");
                    String nim = scanner.nextLine();
                    System.out.print("Masukkan Nama: ");
                    String name = scanner.nextLine();
                    System.out.print("Masukkan Jurusan: ");
                    String major = scanner.nextLine();
                    records.add(new Student(nim, name, major));
                    System.out.println("Mahasiswa berhasil ditambahkan!");
                    break;

                case 2:
                    // View all students
                    System.out.println("\nDaftar Mahasiswa:");
                    if (records.isEmpty()) {
                        System.out.println("Belum ada data mahasiswa.");
                    } else {
                        for (Student s : records) {
                            System.out.println(s);
                        }
                    }
                    break;

                case 3:
                    // Search for a student by NIM
                    System.out.print("Masukkan NIM yang dicari: ");
                    String searchNim = scanner.nextLine();
                    boolean found = false;

                    for (Student s : records) {
                        if (s.getNim().equalsIgnoreCase(searchNim)) {
                            System.out.println("Data ditemukan: " + s);
                            found = true;
                            break;
                        }
                    }

                    if (!found) {
                        System.out.println("Mahasiswa dengan NIM " + searchNim + " tidak ditemukan.");
                    }
                    break;

                case 4:
                    // Delete a student by NIM
                    System.out.print("Masukkan NIM mahasiswa yang akan dihapus: ");
                    String deleteNim = scanner.nextLine();
                    boolean removed = records.removeIf(s -> s.getNim().equalsIgnoreCase(deleteNim));

                    if (removed) {
                        System.out.println("Data mahasiswa berhasil dihapus.");
                    } else {
                        System.out.println("Mahasiswa dengan NIM " + deleteNim + " tidak ditemukan.");
                    }
                    break;

                case 5:
                    // Exit the program
                    System.out.println("Keluar dari sistem. Terima kasih!");
                    break;

                default:
                    // Invalid choice
                    System.out.println("Pilihan tidak valid, coba lagi.");
            }
        } while (choice != 5);

        scanner.close();
    }
}

```
Project Student Record System menggunakan Java Collection (ArrayList).
Fitur Student Record System
1. Tambah data mahasiswa  
   <img width="445" height="269" alt="image" src="https://github.com/user-attachments/assets/29f685a8-638b-4edf-bc9c-0e6b8de83177" />  
2. Lihat semua mahasiswa  
   <img width="945" height="240" alt="image" src="https://github.com/user-attachments/assets/8cf794d0-229d-44fc-baa5-29c4f4116ad8" />  
3. Cari mahasiswa berdasarkan NIM
   <img width="1069" height="214" alt="image" src="https://github.com/user-attachments/assets/4e6ad9d8-5314-4a4a-ba58-602393c68428" />  
4. Hapus mahasiswa berdasarkan NIM
   <img width="630" height="218" alt="image" src="https://github.com/user-attachments/assets/05913417-dc35-44c4-a630-d5ff3fb4620a" />  
5. Keluar  
    <img width="493" height="189" alt="image" src="https://github.com/user-attachments/assets/d4e3dbdd-4279-49e2-a328-c06ea49bb917" />

ArrayList<Student> → menyimpan daftar mahasiswa.  
Class Student → merepresentasikan data mahasiswa (NIM, Nama, Jurusan).  
Cari Mahasiswa → dengan pencocokan NIM.  
Hapus Mahasiswa → menggunakan removeIf agar lebih ringkas.  

## 📓Project Notebook 
```
import java.util.ArrayList;
import java.util.Scanner;

class Note {
    private String title;
    private String content;

    // Constructor
    public Note(String title, String content) {
        this.title = title;
        this.content = content;
    }

    // Getter methods
    public String getTitle() {
        return title;
    }

    public String getContent() {
        return content;
    }

    // Override toString() method for displaying note details
    @Override
    public String toString() {
        return "Judul: " + title + "\nIsi: " + content;
    }
}

public class NotebookApp {
    public static void main(String[] args) {
        ArrayList<Note> notes = new ArrayList<>();
        Scanner scanner = new Scanner(System.in);
        int choice;

        // Menu loop
        do {
            System.out.println("\n=== Personal Notebook ===");
            System.out.println("1. Tambah Catatan");
            System.out.println("2. Lihat Semua Catatan");
            System.out.println("3. Cari Catatan");
            System.out.println("4. Hapus Catatan");
            System.out.println("5. Keluar");
            System.out.print("Pilih menu: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // clear buffer

            switch (choice) {
                case 1:
                    // Add a new note
                    System.out.print("Masukkan judul catatan: ");
                    String title = scanner.nextLine();
                    System.out.print("Masukkan isi catatan: ");
                    String content = scanner.nextLine();
                    notes.add(new Note(title, content));
                    System.out.println("Catatan berhasil ditambahkan!");
                    break;

                case 2:
                    // View all notes
                    System.out.println("\nDaftar Catatan:");
                    if (notes.isEmpty()) {
                        System.out.println("Belum ada catatan.");
                    } else {
                        for (int i = 0; i < notes.size(); i++) {
                            System.out.println((i + 1) + ". " + notes.get(i).getTitle());
                        }
                    }
                    break;

                case 3:
                    // Search for a note by title
                    System.out.print("Masukkan judul catatan yang dicari: ");
                    String searchTitle = scanner.nextLine().toLowerCase();
                    boolean found = false;

                    for (Note note : notes) {
                        if (note.getTitle().toLowerCase().contains(searchTitle)) {
                            System.out.println("\nCatatan ditemukan:\n" + note);
                            found = true;
                        }
                    }
                    if (!found) {
                        System.out.println("Catatan tidak ditemukan.");
                    }
                    break;

                case 4:
                    // Delete a note by title
                    System.out.print("Masukkan judul catatan yang akan dihapus: ");
                    String deleteTitle = scanner.nextLine().toLowerCase();
                    boolean removed = notes.removeIf(note -> note.getTitle().toLowerCase().equals(deleteTitle));

                    if (removed) {
                        System.out.println("Catatan berhasil dihapus.");
                    } else {
                        System.out.println("Catatan dengan judul tersebut tidak ditemukan.");
                    }
                    break;

                case 5:
                    // Exit the program
                    System.out.println("Keluar dari Notebook. Sampai jumpa!");
                    break;

                default:
                    // Invalid choice
                    System.out.println("Pilihan tidak valid, coba lagi.");
            }
        } while (choice != 5);

        scanner.close();
    }
}

```
Project Notebook (Personal Note App) menggunakan Java Collection (ArrayList).
Fitur Notebook
1. Tambah catatan baru
   <img width="861" height="241" alt="image" src="https://github.com/user-attachments/assets/211ef3ce-9784-4d7f-833e-ce455f677fa0" />  
2. Lihat semua catatan  
   <img width="399" height="239" alt="image" src="https://github.com/user-attachments/assets/f009fc9b-8d6b-406a-a2f8-3b2b394790a6" />  
3. Cari catatan berdasarkan judul  
   <img width="770" height="193" alt="image" src="https://github.com/user-attachments/assets/e86f6695-3943-4ff8-b0e0-8de9c0344374" />  
4. Hapus catatan berdasarkan judul  
   <img width="816" height="220" alt="image" src="https://github.com/user-attachments/assets/1ec2178c-1137-460c-9c00-ccedab2d43bf" />  
5. Keluar  
   <img width="498" height="193" alt="image" src="https://github.com/user-attachments/assets/df7e56c3-e524-4e51-9e01-f70c772ad923" />


Class Note → merepresentasikan catatan dengan title dan content.  
ArrayList<Note> → digunakan sebagai wadah koleksi catatan.  
Fitur cari → mencari berdasarkan judul (case-insensitive dan bisa sebagian).  
Fitur hapus → menghapus catatan berdasarkan judul menggunakan removeIf.  

---
