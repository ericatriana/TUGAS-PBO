# 🖥️ Java GUI Login & Image Viewer

## 📖 Deskripsi
Aplikasi **Java GUI Login & Image Viewer** merupakan aplikasi desktop berbasis **Java Swing** yang dibuat menggunakan **BlueJ**.  
Aplikasi ini terdiri dari dua bagian utama:

1. **Login Frame**  
   Digunakan untuk melakukan autentikasi pengguna dengan username dan password.
2. **Image Viewer**  
   Digunakan untuk menampilkan gambar setelah pengguna berhasil login.

Aplikasi ini bertujuan untuk melatih pemahaman konsep **GUI (Graphical User Interface)**, **event handling**, serta **pemrograman berorientasi objek** pada Java.

---

## 🎯 Tujuan Pembuatan
- Memahami penggunaan komponen GUI Java Swing
- Mengimplementasikan event handling (ActionListener)
- Menghubungkan antar frame (Login → Image Viewer)
- Membuat aplikasi desktop sederhana di BlueJ

---

## 🧩 Struktur Kelas
<img width="429" height="300" alt="image" src="https://github.com/user-attachments/assets/6c36ef1e-a747-4be5-98b9-5d0a7860e594" />

### Kelas LoginFrame
``
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class LoginFrame extends JFrame implements ActionListener {

    JTextField txtUsername;
    JPasswordField txtPassword;
    JButton btnLogin;

    public LoginFrame() {
        setTitle("Login");
        setSize(350, 220);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        JPanel panel = new JPanel(new GridBagLayout());
        panel.setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 20));
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(5, 5, 5, 5);

        // ===== Judul =====
        JLabel title = new JLabel("USER LOGIN");
        title.setFont(new Font("Arial", Font.BOLD, 16));
        gbc.gridx = 0;
        gbc.gridy = 0;
        gbc.gridwidth = 2;
        panel.add(title, gbc);

        gbc.gridwidth = 1;

        // ===== Username =====
        gbc.gridx = 0;
        gbc.gridy = 1;
        gbc.anchor = GridBagConstraints.WEST;
        panel.add(new JLabel("Username"), gbc);

        txtUsername = new JTextField(15);
        gbc.gridx = 1;
        panel.add(txtUsername, gbc);

        // ===== Password =====
        gbc.gridx = 0;
        gbc.gridy = 2;
        panel.add(new JLabel("Password"), gbc);

        txtPassword = new JPasswordField(15);
        gbc.gridx = 1;
        panel.add(txtPassword, gbc);

        // ===== Button =====
        btnLogin = new JButton("Login");
        btnLogin.addActionListener(this);
        btnLogin.setPreferredSize(new Dimension(120, 30));

        gbc.gridx = 0;
        gbc.gridy = 3;
        gbc.gridwidth = 2;
        gbc.anchor = GridBagConstraints.CENTER;
        panel.add(btnLogin, gbc);

        add(panel);
        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        String user = txtUsername.getText();
        String pass = new String(txtPassword.getPassword());

        if (user.equals("admin") && pass.equals("123")) {
            JOptionPane.showMessageDialog(this, "Login Berhasil");
            dispose();
            new ImageViewer();
        } else {
            JOptionPane.showMessageDialog(this, "Username atau Password salah");
        }
    }

    public static void main(String[] args) {
        new LoginFrame();
    }
}
``

### Kelas ImagaeViewer
``
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.io.File;

public class ImageViewer extends JFrame implements ActionListener {

    JLabel imageLabel;
    JMenuItem openItem, exitItem;

    public ImageViewer() {
        setTitle("Simple Image Viewer");
        setSize(600, 500);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        imageLabel = new JLabel();
        imageLabel.setHorizontalAlignment(JLabel.CENTER);
        add(imageLabel, BorderLayout.CENTER);

        // Menu
        JMenuBar menuBar = new JMenuBar();
        JMenu fileMenu = new JMenu("File");

        openItem = new JMenuItem("Open Image");
        exitItem = new JMenuItem("Exit");

        openItem.addActionListener(this);
        exitItem.addActionListener(this);

        fileMenu.add(openItem);
        fileMenu.add(exitItem);
        menuBar.add(fileMenu);

        setJMenuBar(menuBar);
        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == openItem) {
            JFileChooser chooser = new JFileChooser();
            int result = chooser.showOpenDialog(this);

            if (result == JFileChooser.APPROVE_OPTION) {
                File file = chooser.getSelectedFile();
                ImageIcon icon = new ImageIcon(file.getAbsolutePath());

                Image img = icon.getImage();
                Image scaledImg = img.getScaledInstance(
                        getWidth() - 50,
                        getHeight() - 100,
                        Image.SCALE_SMOOTH
                );

                imageLabel.setIcon(new ImageIcon(scaledImg));
            }
        }

        if (e.getSource() == exitItem) {
            System.exit(0);
        }
    }

    public static void main(String[] args) {
        new ImageViewer();
    }
}
``

## Hasil
<img width="487" height="309" alt="image" src="https://github.com/user-attachments/assets/c6af4036-a31a-4941-9b9b-6505ac3ac118" />




