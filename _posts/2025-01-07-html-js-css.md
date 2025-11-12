---
title: Html + Js + Css
author: Chu Ying
date: 2025-01-06
category: java
layout: post
---
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>交互式动画按钮示例</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            padding: 20px;
        }
        
        .container {
            text-align: center;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            max-width: 500px;
            width: 100%;
        }
        
        h1 {
            color: white;
            margin-bottom: 10px;
            font-size: 2.5rem;
            text-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        }
        
        p {
            color: rgba(255, 255, 255, 0.8);
            margin-bottom: 30px;
            font-size: 1.1rem;
            line-height: 1.6;
        }
        
        .button-container {
            display: flex;
            flex-direction: column;
            gap: 25px;
            margin-top: 40px;
        }
        
        .animated-button {
            position: relative;
            padding: 15px 30px;
            font-size: 1.2rem;
            font-weight: 600;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            overflow: hidden;
            color: white;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            outline: none;
        }
        
        /* 按钮1 - 渐变背景 */
        .btn-1 {
            background: linear-gradient(90deg, #ff6b6b, #ff8e8e);
            background-size: 200% 100%;
            background-position: left bottom;
        }
        
        .btn-1:hover {
            background-position: right bottom;
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
        }
        
        .btn-1:active {
            transform: translateY(1px);
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2);
        }
        
        /* 按钮2 - 边框动画 */
        .btn-2 {
            background: transparent;
            border: 2px solid #4cd964;
            color: #4cd964;
        }
        
        .btn-2:hover {
            background: #4cd964;
            color: white;
            letter-spacing: 2px;
        }
        
        /* 按钮3 - 波纹效果 */
        .btn-3 {
            background: #5ac8fa;
        }
        
        .btn-3:hover {
            background: #007aff;
        }
        
        .btn-3::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 5px;
            height: 5px;
            background: rgba(255, 255, 255, 0.5);
            opacity: 0;
            border-radius: 100%;
            transform: scale(1, 1) translate(-50%);
            transform-origin: 50% 50%;
        }
        
        .btn-3:focus:not(:active)::after {
            animation: ripple 1s ease-out;
        }
        
        @keyframes ripple {
            0% {
                transform: scale(0, 0);
                opacity: 0.5;
            }
            100% {
                transform: scale(20, 20);
                opacity: 0;
            }
        }
        
        .result {
            margin-top: 30px;
            padding: 15px;
            background: rgba(255, 255, 255, 0.15);
            border-radius: 10px;
            color: white;
            min-height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
        }
        
        .counter {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            margin-top: 20px;
            color: white;
        }
        
        .counter button {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            border: none;
            background: rgba(255, 255, 255, 0.2);
            color: white;
            font-size: 1.5rem;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        
        .counter button:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: scale(1.1);
        }
        
        .counter span {
            font-size: 1.8rem;
            font-weight: bold;
            min-width: 60px;
        }
        
        .highlight {
            animation: highlight 0.5s ease;
        }
        
        @keyframes highlight {
            0% { background: rgba(255, 255, 255, 0.3); }
            100% { background: rgba(255, 255, 255, 0.15); }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>交互式动画按钮</h1>
        <p>这个示例展示了CSS动画和JavaScript交互的结合使用。尝试悬停或点击下面的按钮，体验不同的动画效果。</p>
        
        <div class="button-container">
            <button class="animated-button btn-1" id="btn1">渐变背景动画</button>
            <button class="animated-button btn-2" id="btn2">边框动画</button>
            <button class="animated-button btn-3" id="btn3">点击波纹效果</button>
        </div>
        
        <div class="result" id="result">
            点击按钮查看交互效果
        </div>
        
        <div class="counter">
            <button id="decrease">-</button>
            <span id="count">0</span>
            <button id="increase">+</button>
        </div>
    </div>

    <script>
        // 获取DOM元素
        const btn1 = document.getElementById('btn1');
        const btn2 = document.getElementById('btn2');
        const btn3 = document.getElementById('btn3');
        const result = document.getElementById('result');
        const countElement = document.getElementById('count');
        const increaseBtn = document.getElementById('increase');
        const decreaseBtn = document.getElementById('decrease');
        
        let count = 0;
        
        // 按钮1点击事件
        btn1.addEventListener('click', function() {
            result.textContent = "你点击了渐变背景按钮！";
            result.classList.remove('highlight');
            void result.offsetWidth; // 触发重排以重新播放动画
            result.classList.add('highlight');
        });
        
        // 按钮2点击事件
        btn2.addEventListener('click', function() {
            result.textContent = "你点击了边框动画按钮！";
            result.classList.remove('highlight');
            void result.offsetWidth;
            result.classList.add('highlight');
        });
        
        // 按钮3点击事件
        btn3.addEventListener('click', function() {
            result.textContent = "你点击了波纹效果按钮！";
            result.classList.remove('highlight');
            void result.offsetWidth;
            result.classList.add('highlight');
        });
        
        // 增加计数
        increaseBtn.addEventListener('click', function() {
            count++;
            countElement.textContent = count;
            updateCounterColor();
        });
        
        // 减少计数
        decreaseBtn.addEventListener('click', function() {
            count--;
            countElement.textContent = count;
            updateCounterColor();
        });
        
        // 根据计数值更新颜色
        function updateCounterColor() {
            if (count > 0) {
                countElement.style.color = '#4cd964'; // 绿色
            } else if (count < 0) {
                countElement.style.color = '#ff3b30'; // 红色
            } else {
                countElement.style.color = 'white'; // 白色
            }
        }
        
        // 初始更新颜色
        updateCounterColor();
    </script>
</body>
</html>
```
