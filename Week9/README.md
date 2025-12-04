# 📚 Sales Item Unit Testing 🧪

## 📖 Deskripsi
Aplikasi **Sales Item Unit Testing** ini bertujuan untuk menguji kelas **SalesItem** yang mengelola item yang dijual. Aplikasi ini mencakup fungsionalitas dasar seperti menambahkan item, menghitung total harga berdasarkan kuantitas dan harga satuan, serta menghapus item. Unit testing dilakukan untuk memastikan bahwa metode pada kelas **SalesItem** berfungsi dengan baik.

Unit testing dilakukan dengan menggunakan **JUnit** untuk memverifikasi:
1. Perhitungan total harga.
2. Penghapusan item dari sistem.
3. Validasi atribut `name`, `unitPrice`, dan `quantity`.

---

## 🏗️ Struktur Kelas  
<img width="619" height="304" alt="image" src="https://github.com/user-attachments/assets/e3d84053-d748-40f6-af56-1216f1b6f6a9" />  

### 1. Kelas SalesItem 🏷️
Kelas ini mendeskripsikan item yang dijual dengan atribut seperti nama item, harga per unit, dan jumlah kuantitas yang terjual. Kelas ini juga memiliki metode untuk menghitung total harga berdasarkan kuantitas dan harga per unit.

#### Kode:
```java
public class SalesItem {
    private String name;
    private double unitPrice;
    private int quantity;

    // Konstruktor
    public SalesItem(String name, double unitPrice, int quantity) {
        this.name = name;
        this.unitPrice = unitPrice;
        this.quantity = quantity;
    }

    // Getter untuk nama item
    public String getName() {
        return name;
    }

    // Getter untuk harga per unit
    public double getUnitPrice() {
        return unitPrice;
    }

    // Getter untuk kuantitas
    public int getQuantity() {
        return quantity;
    }

    // Method untuk menghitung total harga
    public double calculateTotal() {
        return unitPrice * quantity;
    }

    // Method untuk menghapus item
    public void removeItem() {
        this.name = null;
        this.unitPrice = 0;
        this.quantity = 0;
    }
}
```
### 2. Kelas SalesItemTest 🧪
Kelas ini berfungsi untuk melakukan unit testing terhadap kelas SalesItem. Di dalamnya, kita akan menguji apakah metode-metode yang ada di kelas SalesItem berfungsi dengan baik.  
```
import org.junit.Test;
import static org.junit.Assert.*;

public class SalesItemTest {

    // Test untuk menghitung total harga
    @Test
    public void testCalculateTotal() {
        SalesItem item = new SalesItem("Laptop", 5000000, 2);
        assertEquals("Total harga harusnya 10000000", 10000000.0, item.calculateTotal(), 0.01);
    }

    // Test untuk menghapus item
    @Test
    public void testRemoveItem() {
        SalesItem item = new SalesItem("Laptop", 5000000, 2);
        item.removeItem();
        assertNull("Nama item setelah dihapus harus null", item.getName());
        assertEquals("Harga per unit setelah dihapus harus 0", 0, item.getUnitPrice(), 0.01);
        assertEquals("Kuantitas setelah dihapus harus 0", 0, item.getQuantity());
    }

    // Test untuk memastikan nama item yang benar
    @Test
    public void testGetName() {
        SalesItem item = new SalesItem("Laptop", 5000000, 2);
        assertEquals("Nama item harusnya Laptop", "Laptop", item.getName());
    }

    // Test untuk memastikan harga per unit yang benar
    @Test
    public void testGetUnitPrice() {
        SalesItem item = new SalesItem("Laptop", 5000000, 2);
        assertEquals("Harga per unit harusnya 5000000", 5000000, item.getUnitPrice(), 0.01);
    }

    // Test untuk memastikan kuantitas yang benar
    @Test
    public void testGetQuantity() {
        SalesItem item = new SalesItem("Laptop", 5000000, 2);
        assertEquals("Kuantitas harusnya 2", 2, item.getQuantity());
    }
}

```
### 3. Kelas Main 🚀
Kelas Main adalah kelas utama untuk menjalankan aplikasi. Di sini kita mendemonstrasikan penggunaan kelas SalesItem dan menguji penghapusan item serta perhitungan harga total.
```
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Inisialisasi SalesItem
        SalesItem item1 = new SalesItem("Laptop", 5000000, 2);
        SalesItem item2 = new SalesItem("Smartphone", 3000000, 5);

        // Menampilkan informasi item pertama
        System.out.println("Nama Item: " + item1.getName());
        System.out.println("Harga per Unit: " + item1.getUnitPrice());
        System.out.println("Total Harga: " + item1.calculateTotal());

        // Menghapus item setelah diprint
        item1.removeItem();
        System.out.println("Item 1 setelah dihapus: ");
        System.out.println("Nama: " + item1.getName());
        System.out.println("Harga: " + item1.getUnitPrice());
        System.out.println("Kuantitas: " + item1.getQuantity());

        scanner.close();
    }
}

```
