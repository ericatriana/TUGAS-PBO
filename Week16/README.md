# 📚 Aplikasi CRUD Manajemen Buku Perpustakaan

## 📖 Deskripsi
Aplikasi **Manajemen Buku Perpustakaan** ini dibangun menggunakan **Java Swing** dan menerapkan konsep **CRUD (Create, Read, Update, Delete)** untuk mengelola data buku di perpustakaan. Aplikasi ini memungkinkan pengguna untuk:
- Menambah buku baru
- Melihat daftar buku yang ada
- Mengubah informasi buku
- Menghapus buku yang sudah tidak diperlukan

Aplikasi ini juga menggunakan **ArrayList** untuk menyimpan data buku secara sementara (bisa dikembangkan untuk menyimpan data secara permanen ke file atau database).

---

## 🎯 Tujuan Pembuatan
Tujuan utama pembuatan aplikasi ini adalah:
1. Memahami konsep dasar operasi CRUD.
2. Mengimplementasikan GUI dengan **Java Swing**.
3. Menerapkan prinsip **Object-Oriented Programming (OOP)** dalam pengelolaan data.

---

## 🧩 Struktur Kelas
<img width="667" height="382" alt="image" src="https://github.com/user-attachments/assets/ee4b5293-7bda-4826-8548-535da992fbad" />

### 🔹 **Book.java**
Kelas ini merupakan **model** untuk data buku, yang memiliki atribut `kode`, `judul`, dan `penulis`.
``
public class Book {
    private String kode;
    private String judul;
    private String penulis;

    public Book(String kode, String judul, String penulis) {
        this.kode = kode;
        this.judul = judul;
        this.penulis = penulis;
    }

    public String getKode() {
        return kode;
    }

    public String getJudul() {
        return judul;
    }

    public String getPenulis() {
        return penulis;
    }

    public void setJudul(String judul) {
        this.judul = judul;
    }

    public void setPenulis(String penulis) {
        this.penulis = penulis;
    }
}
``

### 🔹 **LibraryManager.java**
Kelas ini bertugas untuk **mengelola data buku**, dan memiliki fungsi-fungsi CRUD:
- **Tambah buku**
- **Baca daftar buku**
- **Ubah data buku**
- **Hapus buku**
``
import java.util.ArrayList;

public class LibraryManager {

    private ArrayList<Book> daftarBuku;

    public LibraryManager() {
        daftarBuku = new ArrayList<>();
    }

    // Create: Menambahkan buku baru
    public void tambahBuku(String kode, String judul, String penulis) {
        Book buku = new Book(kode, judul, penulis);
        daftarBuku.add(buku);
    }

    // Read: Mengambil daftar buku
    public ArrayList<Book> getDaftarBuku() {
        return daftarBuku;
    }

    // Update: Mengubah buku berdasarkan index
    public void ubahBuku(int index, String judul, String penulis) {
        if (index >= 0 && index < daftarBuku.size()) {
            Book buku = daftarBuku.get(index);
            buku.setJudul(judul);
            buku.setPenulis(penulis);
        }
    }

    // Delete: Menghapus buku berdasarkan index
    public void hapusBuku(int index) {
        if (index >= 0 && index < daftarBuku.size()) {
            daftarBuku.remove(index);
        }
    }
}
``

### 🔹 **LibraryCRUD.java**
Kelas ini adalah **GUI** aplikasi yang digunakan untuk:
- Menampilkan **form input** data buku
- Menampilkan **tabel daftar buku**
- Menghubungkan antara **fungsi CRUD** dan GUI
``
import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import java.awt.*;
import java.awt.event.*;
import java.util.ArrayList;

public class LibraryCRUD extends JFrame implements ActionListener {

    JTextField txtKode, txtJudul, txtPenulis;
    JButton btnTambah, btnUbah, btnHapus;
    JTable table;
    DefaultTableModel model;

    LibraryManager manager = new LibraryManager();

    public LibraryCRUD() {
        setTitle("Manajemen Buku Perpustakaan");
        setSize(600, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        // Panel Input
        JPanel panelInput = new JPanel(new GridLayout(4, 2, 5, 5));
        panelInput.setBorder(BorderFactory.createTitledBorder("Input Data Buku"));

        panelInput.add(new JLabel("Kode Buku"));
        txtKode = new JTextField();
        panelInput.add(txtKode);

        panelInput.add(new JLabel("Judul Buku"));
        txtJudul = new JTextField();
        panelInput.add(txtJudul);

        panelInput.add(new JLabel("Penulis"));
        txtPenulis = new JTextField();
        panelInput.add(txtPenulis);

        btnTambah = new JButton("Tambah");
        btnUbah = new JButton("Ubah");
        btnHapus = new JButton("Hapus");

        panelInput.add(btnTambah);
        panelInput.add(btnUbah);

        // Table
        model = new DefaultTableModel(new String[]{"Kode", "Judul", "Penulis"}, 0);
        table = new JTable(model);
        JScrollPane scrollPane = new JScrollPane(table);

        // Panel bawah
        JPanel panelBottom = new JPanel();
        panelBottom.add(btnHapus);

        add(panelInput, BorderLayout.NORTH);
        add(scrollPane, BorderLayout.CENTER);
        add(panelBottom, BorderLayout.SOUTH);

        btnTambah.addActionListener(this);
        btnUbah.addActionListener(this);
        btnHapus.addActionListener(this);

        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == btnTambah) {
            tambahBuku();
        } else if (e.getSource() == btnUbah) {
            ubahBuku();
        } else if (e.getSource() == btnHapus) {
            hapusBuku();
        }
    }

    // Create: Tambah Buku
    private void tambahBuku() {
        manager.tambahBuku(txtKode.getText(), txtJudul.getText(), txtPenulis.getText());
        tampilkanBuku();
        clearForm();
    }

    // Read: Tampilkan Buku di Table
    private void tampilkanBuku() {
        ArrayList<Book> daftarBuku = manager.getDaftarBuku();
        model.setRowCount(0); // Clear table

        for (Book buku : daftarBuku) {
            model.addRow(new Object[]{
                    buku.getKode(),
                    buku.getJudul(),
                    buku.getPenulis()
            });
        }
    }

    // Update: Ubah Buku
    private void ubahBuku() {
        int row = table.getSelectedRow();
        if (row >= 0) {
            String judul = txtJudul.getText();
            String penulis = txtPenulis.getText();

            manager.ubahBuku(row, judul, penulis);
            tampilkanBuku();
        }
    }

    // Delete: Hapus Buku
    private void hapusBuku() {
        int row = table.getSelectedRow();
        if (row >= 0) {
            manager.hapusBuku(row);
            tampilkanBuku();
        }
    }

    // Clear input form
    private void clearForm() {
        txtKode.setText("");
        txtJudul.setText("");
        txtPenulis.setText("");
    }

    public static void main(String[] args) {
        new LibraryCRUD();
    }
}
``

---

## 📸 Tampilan Aplikasi
<img width="735" height="486" alt="image" src="https://github.com/user-attachments/assets/b0af5e0a-e1b0-4da8-83af-5c2346542253" />



✨ **Aplikasi ini dibuat untuk latihan pemrograman CRUD menggunakan Java Swing dan BlueJ.**

