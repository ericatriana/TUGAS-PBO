# 🕹️ Game Pong Java

## 📖 Deskripsi
**Game Pong Java** adalah permainan klasik dua dimensi yang dibuat menggunakan bahasa pemrograman **Java**.  
Game ini mensimulasikan permainan tenis meja sederhana, di mana pemain mengontrol paddle untuk memantulkan bola agar tidak keluar dari area permainan.

Aplikasi ini dibuat sebagai latihan pemrograman **Java GUI**, **event handling**, serta **logika game dasar**.

---

## 🎯 Tujuan Pembuatan
- Memahami konsep game loop sederhana
- Mengimplementasikan event keyboard pada Java
- Menggunakan Java Swing dan AWT
- Melatih logika pergerakan objek dan collision detection

---

## 🎮 Aturan Permainan
- Bola bergerak secara otomatis di layar
- Pemain mengontrol paddle untuk memantulkan bola
- Jika bola keluar dari sisi pemain, permainan berakhir
- Skor bertambah setiap kali bola berhasil dipantulkan

---

## 🧩 Struktur Kelas
<img width="661" height="531" alt="image" src="https://github.com/user-attachments/assets/7d1b6932-cec7-4f66-ab68-0ff484531e97" />


### 🔹 PongGame
Kelas utama yang menjalankan game.

**Fungsi utama:**
- Membuat frame game
- Menjalankan GamePanel
- Menjadi entry point program (`main`)
``
import javax.swing.JFrame;

public class PongGame {

    public static void main(String[] args) {
        JFrame frame = new JFrame("Pong Game");
        GamePanel game = new GamePanel();

        frame.add(game);
        frame.setSize(800, 600);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setResizable(false);
        frame.setVisible(true);
    }
}
``
---

### 🔹 GamePanel
Kelas inti permainan.

**Fungsi:**
- Menggambar paddle dan bola
- Mengatur game loop
- Mengecek tabrakan (collision)
- Mengatur skor
``
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class GamePanel extends JPanel implements ActionListener, KeyListener {

    private Timer timer;
    private Paddle paddle1, paddle2;
    private Ball ball;

    private int scoreLeft = 0;
    private int scoreRight = 0;

    private final Color bgColor = new Color(255, 228, 235);
    private final Color scoreColor = new Color(255, 105, 180);

    public GamePanel() {
        paddle1 = new Paddle(20, 250);
        paddle2 = new Paddle(760, 250);
        ball = new Ball(400, 300);

        timer = new Timer(10, this);
        timer.start();

        setFocusable(true);
        addKeyListener(this);
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);

        setBackground(bgColor);

        // Garis tengah
        g.setColor(new Color(255, 180, 200));
        for (int y = 0; y < getHeight(); y += 20) {
            g.fillRect(getWidth() / 2 - 2, y, 4, 10);
        }

        // Score
        g.setFont(new Font("Arial", Font.BOLD, 36));
        g.setColor(scoreColor);
        g.drawString(String.valueOf(scoreLeft), 350, 50);
        g.drawString(String.valueOf(scoreRight), 430, 50);

        paddle1.draw(g);
        paddle2.draw(g);
        ball.draw(g);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        paddle1.move();
        paddle2.move();
        ball.move();

        ball.checkCollision(paddle1);
        ball.checkCollision(paddle2);

        // Cek skor
        if (ball.isOutLeft()) {
            scoreRight++;
            ball.reset();
        }

        if (ball.isOutRight()) {
            scoreLeft++;
            ball.reset();
        }

        repaint();
    }

    @Override
    public void keyPressed(KeyEvent e) {
        paddle1.keyPressed(e);
        paddle2.keyPressed(e);
    }

    @Override
    public void keyReleased(KeyEvent e) {
        paddle1.keyReleased(e);
        paddle2.keyReleased(e);
    }

    @Override
    public void keyTyped(KeyEvent e) {}
}
``
---

### 🔹 Paddle
Mewakili paddle pemain.

**Fitur:**
- Bergerak ke atas dan ke bawah
- Dikontrol menggunakan keyboard
- Memantulkan bola
``
import java.awt.*;
import java.awt.event.KeyEvent;

public class Paddle {

    private int x, y;
    private int ySpeed;
    private final int WIDTH = 12;
    private final int HEIGHT = 100;

    private final Color paddleColor = new Color(255, 105, 180);

    public Paddle(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public void move() {
        y += ySpeed;
        if (y < 0) y = 0;
        if (y > 500) y = 500;
    }

    public void draw(Graphics g) {
        g.setColor(paddleColor);
        g.fillRoundRect(x, y, WIDTH, HEIGHT, 20, 20);
    }

    public Rectangle getBounds() {
        return new Rectangle(x, y, WIDTH, HEIGHT);
    }

    public void keyPressed(KeyEvent e) {
        if (x < 400) {
            if (e.getKeyCode() == KeyEvent.VK_W) ySpeed = -5;
            if (e.getKeyCode() == KeyEvent.VK_S) ySpeed = 5;
        } else {
            if (e.getKeyCode() == KeyEvent.VK_UP) ySpeed = -5;
            if (e.getKeyCode() == KeyEvent.VK_DOWN) ySpeed = 5;
        }
    }

    public void keyReleased(KeyEvent e) {
        ySpeed = 0;
    }
}
``
---

### 🔹 Ball
Mewakili bola permainan.

**Fitur:**
- Bergerak otomatis
- Memantul saat mengenai paddle atau dinding
- Mengakhiri permainan jika keluar area
``
import java.awt.*;

public class Ball {

    private int x, y;
    private int xSpeed = 4;
    private int ySpeed = 4;
    private final int SIZE = 16;

    public Ball(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public void move() {
        x += xSpeed;
        y += ySpeed;

        if (y <= 0 || y >= 584) {
            ySpeed *= -1;
        }
    }

    public void draw(Graphics g) {
        g.setColor(Color.WHITE);
        g.fillOval(x, y, SIZE, SIZE);
    }

    public void checkCollision(Paddle paddle) {
        if (getBounds().intersects(paddle.getBounds())) {
            xSpeed *= -1;
        }
    }

    public boolean isOutLeft() {
        return x <= 0;
    }

    public boolean isOutRight() {
        return x >= 784;
    }

    public void reset() {
        x = 400;
        y = 300;
        xSpeed *= -1;
    }

    public Rectangle getBounds() {
        return new Rectangle(x, y, SIZE, SIZE);
    }
}
``
---

## ⌨️ Kontrol Pemain

| Tombol | Fungsi |
|------|--------|
| W | Paddle ke atas |
| S | Paddle ke bawah |
| ↑ | Paddle ke atas (Player 2) |
| ↓ | Paddle ke bawah (Player 2) |

---

## Hasil
<img width="985" height="744" alt="image" src="https://github.com/user-attachments/assets/ef968c73-4fe1-42bd-9f88-c53a5b478dc9" />

