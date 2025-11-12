---
title: Java
author: Chu Ying
date: 2022-02-04
category: java
layout: post
---

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
