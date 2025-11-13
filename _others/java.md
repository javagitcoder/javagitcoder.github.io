---
title: Java
author: Chu Ying
date: 2022-02-04
category: java
layout: post
---
<h2>一、Java基础</h2> 
<h3>1. Java中基本数据类型有哪些？</h3> 
<p>Java有8种基本数据类型，分为4类：</p> 
<ul>
 <li><strong>整数类型</strong>：byte（1字节）、short（2字节）、int（4字节）、long（8字节）。</li>
 <li><strong>浮点类型</strong>：float（4字节）、double（8字节）。</li>
 <li><strong>字符类型</strong>：char（2字节）。</li>
 <li><strong>布尔类型</strong>：boolean（理论上1位，实际实现中通常是1字节）。</li>
</ul> 
<h3>2. 请解释一下自动装箱和拆箱</h3> 
<ul>
 <li><strong>自动装箱</strong>：是指将基本数据类型自动转换为对应的包装类对象。例如，<code>int i = 10; Integer integer = i;</code> 这里<code>int</code>类型的<code>i</code>自动装箱成了<code>Integer</code>类型的<code>integer</code>。</li>
 <li><strong>自动拆箱</strong>：是指将包装类对象自动转换为对应的基本数据类型。例如，<code>Integer integer = 20; int j = integer;</code> 这里<code>Integer</code>类型的<code>integer</code>自动拆箱成了<code>int</code>类型的<code>j</code>。</li>
</ul> 
<h3>3. 简述String、StringBuilder和StringBuffer的区别</h3> 
<ul>
 <li><strong>可变性</strong>：
  <ul>
   <li><code>String</code>是不可变的，一旦创建，其值不能被修改。每次对<code>String</code>进行操作都会创建一个新的<code>String</code>对象。例如，<code>String s = "hello"; s = s + "world";</code> 在执行<code>s = s + "world";</code>时，会创建一个新的<code>String</code>对象，内容为<code>"helloworld"</code>，原来的<code>"hello"</code>对象依然存在于内存中，只是<code>String</code>类型的变量<code>s</code>指向了新的对象。</li>
   <li><code>StringBuilder</code>和<code>StringBuffer</code>是可变的，它们可以在原对象上进行修改，不会创建新对象。例如，<code>StringBuilder sb = new StringBuilder("hello"); sb.append("world");</code> 这里<code>sb</code>对象本身被修改，其内容变为<code>"helloworld"</code>，而不是创建一个新的对象。</li>
  </ul> </li>
 <li><strong>线程安全性</strong>：
  <ul>
   <li><code>String</code>是线程安全的，因为它是不可变的，多个线程同时访问同一个<code>String</code>对象时，不会出现数据不一致的问题。</li>
   <li><code>StringBuffer</code>是线程安全的，它的方法都使用了<code>synchronized</code>关键字进行同步。例如，<code>StringBuffer sb = new StringBuffer(); sb.append("a");</code> 当多个线程同时调用<code>sb.append("a");</code>时，由于<code>synchronized</code>的存在，同一时间只有一个线程能够执行该方法，保证了线程安全。</li>
   <li><code>StringBuilder</code>是非线程安全的，但其性能比<code>StringBuffer</code>高，因为不需要进行同步操作。在单线程环境下，使用<code>StringBuilder</code>进行字符串操作可以获得更好的性能。例如，在一个只在单线程中执行的方法中，频繁进行字符串拼接操作，使用<code>StringBuilder</code>会比<code>StringBuffer</code>更高效。</li>
  </ul> </li>
 <li><strong>应用场景</strong>：
  <ul>
   <li>如果字符串操作较少，使用<code>String</code>。例如，只是定义一个固定的字符串常量，如<code>String message = "This is a message";</code></li>
   <li>如果是单线程环境下进行大量字符串拼接，使用<code>StringBuilder</code>。比如在一个单线程的日志记录方法中，需要不断拼接日志信息，使用<code>StringBuilder</code>能提高效率。</li>
   <li>如果是多线程环境下进行大量字符串拼接，使用<code>StringBuffer</code>。例如在一个多线程的网络通信模块中，多个线程需要向同一个字符串缓冲区中追加数据，就需要使用<code>StringBuffer</code>来保证线程安全。</li>
  </ul> </li>
</ul> 
```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;

public class GoBoard extends JPanel {
    private static final int BOARD_SIZE = 19; // 19x19 标准围棋棋盘
    private static final int CELL_SIZE = 30; // 每个格子的像素大小
    private static final int MARGIN = 30; // 边距

    // 棋子状态: 0=空, 1=黑子, 2=白子
    private int[][] boardState = new int[BOARD_SIZE][BOARD_SIZE];

    // 当前玩家: 1=黑, 2=白
    private int currentPlayer = 1;

    public GoBoard() {
        setPreferredSize(new Dimension(
                BOARD_SIZE * CELL_SIZE + 2 * MARGIN,
                BOARD_SIZE * CELL_SIZE + 2 * MARGIN
        ));

        // 添加鼠标监听器处理落子
        addMouseListener(new MouseAdapter() {
            @Override
            public void mouseClicked(MouseEvent e) {
                handleClick(e.getX(), e.getY());
            }
        });
    }

    private void handleClick(int x, int y) {
        // 转换为棋盘坐标
        int boardX = (x - MARGIN + CELL_SIZE / 2) / CELL_SIZE;
        int boardY = (y - MARGIN + CELL_SIZE / 2) / CELL_SIZE;

        // 检查是否在棋盘范围内
        if (boardX >= 0 && boardX < BOARD_SIZE && boardY >= 0 && boardY < BOARD_SIZE) {
            // 检查该位置是否已有棋子
            if (boardState[boardX][boardY] == 0) {
                // 落子
                boardState[boardX][boardY] = currentPlayer;

                // 切换玩家
                currentPlayer = (currentPlayer == 1) ? 2 : 1;

                // 重绘棋盘
                repaint();
            } else {
                // 位置已有棋子，可以添加提示音或消息
                Toolkit.getDefaultToolkit().beep();
            }
        }
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);

        // 设置抗锯齿
        Graphics2D g2d = (Graphics2D) g;
        g2d.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);

        // 绘制棋盘背景
        g2d.setColor(new Color(220, 179, 92)); // 木质颜色
        g2d.fillRect(0, 0, getWidth(), getHeight());

        // 绘制网格线
        g2d.setColor(Color.BLACK);
        for (int i = 0; i < BOARD_SIZE; i++) {
            // 横线
            g2d.drawLine(
                    MARGIN,
                    MARGIN + i * CELL_SIZE,
                    MARGIN + (BOARD_SIZE - 1) * CELL_SIZE,
                    MARGIN + i * CELL_SIZE
            );
            // 竖线
            g2d.drawLine(
                    MARGIN + i * CELL_SIZE,
                    MARGIN,
                    MARGIN + i * CELL_SIZE,
                    MARGIN + (BOARD_SIZE - 1) * CELL_SIZE
            );
        }

        // 绘制天元和星位
        int[] starPoints = {3, 9, 15}; // 19路棋盘的星位坐标
        for (int x : starPoints) {
            for (int y : starPoints) {
                g2d.fillOval(
                        MARGIN + x * CELL_SIZE - 4,
                        MARGIN + y * CELL_SIZE - 4,
                        8, 8
                );
            }
        }

        // 绘制棋子
        for (int i = 0; i < BOARD_SIZE; i++) {
            for (int j = 0; j < BOARD_SIZE; j++) {
                if (boardState[i][j] != 0) {
                    if (boardState[i][j] == 1) {
                        g2d.setColor(Color.BLACK); // 黑子
                    } else {
                        g2d.setColor(Color.WHITE); // 白子
                    }

                    // 绘制棋子
                    g2d.fillOval(
                            MARGIN + i * CELL_SIZE - CELL_SIZE / 2,
                            MARGIN + j * CELL_SIZE - CELL_SIZE / 2,
                            CELL_SIZE, CELL_SIZE
                    );

                    // 为白子添加黑色边框
                    if (boardState[i][j] == 2) {
                        g2d.setColor(Color.BLACK);
                        g2d.drawOval(
                                MARGIN + i * CELL_SIZE - CELL_SIZE / 2,
                                MARGIN + j * CELL_SIZE - CELL_SIZE / 2,
                                CELL_SIZE, CELL_SIZE
                        );
                    }
                }
            }
        }

        // 显示当前玩家
        g2d.setColor(Color.BLACK);
        g2d.setFont(new Font("Arial", Font.BOLD, 16));
        String playerText = (currentPlayer == 1) ? "Player: Black" : "Player: White";
        g2d.drawString(playerText, MARGIN, 20);
    }

    // 重置棋盘
    public void resetBoard() {
        boardState = new int[BOARD_SIZE][BOARD_SIZE];
        currentPlayer = 1;
        repaint();
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            JFrame frame = new JFrame("围棋棋盘");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

            GoBoard board = new GoBoard();
            frame.add(board, BorderLayout.CENTER);

            // 添加重置按钮
            JButton resetButton = new JButton("重置棋盘");
            resetButton.addActionListener(e -> board.resetBoard());

            JPanel buttonPanel = new JPanel();
            buttonPanel.add(resetButton);
            frame.add(buttonPanel, BorderLayout.SOUTH);

            frame.pack();
            frame.setLocationRelativeTo(null);
            frame.setVisible(true);
        });
    }
}
```

