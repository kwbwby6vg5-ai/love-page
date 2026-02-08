# love-page
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <!-- 核心适配：微信/手机端禁止缩放，满屏显示 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>I Love You</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            min-height: 100vh;
            background: #000; /* 黑色背景，突出爱心和文字 */
            overflow: hidden; /* 隐藏溢出，避免滚动条 */
            font-family: Arial, sans-serif;
        }
        /* 中间大爱心：跳动+放大动画 */
        .big-heart {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(1);
            color: #ff3366; /* 玫红爱心，更浪漫 */
            font-size: 120px; /* 基础大小，自动适配 */
            z-index: 10; /* 大爱心在最上层 */
            animation: heartBeat 1.5s infinite ease-in-out;
        }
        /* 浮动的I love you字符：随机位置+颜色+大小+上浮动画 */
        .text-item {
            position: absolute;
            color: #fff;
            font-size: 16px;
            opacity: 0.8;
            z-index: 5;
            animation: floatUp 6s infinite linear;
        }
        /* 大爱心跳动动画 */
        @keyframes heartBeat {
            0%, 100% { transform: translate(-50%, -50%) scale(1); }
            50% { transform: translate(-50%, -50%) scale(1.2); }
        }
        /* 字符上浮+渐隐动画 */
        @keyframes floatUp {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 0;
            }
            10% { opacity: 0.9; }
            90% { opacity: 0.9; }
            100% {
                transform: translateY(-20px) rotate(10deg);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <!-- 中间大爱心 -->
    <div class="big-heart">❤️</div>

    <script>
        // 生成浮动的I love you字符
        function createLoveText() {
            const body = document.body;
            const colors = ['#ff3366', '#ff99cc', '#ffffff', '#ff6699', '#ff0066']; // 爱心色系，避免杂乱
            const text = 'I love you';

            // 循环生成字符，数量可改（30个足够满屏，不卡顿）
            for (let i = 0; i < 30; i++) {
                const item = document.createElement('div');
                item.className = 'text-item';
                item.innerText = text;

                // 随机位置（左右）、颜色、大小、动画延迟（避免同时出现）
                const randomLeft = Math.random() * 90 + 5; // 5%-95%，避免贴边
                const randomColor = colors[Math.floor(Math.random() * colors.length)];
                const randomSize = Math.random() * 8 + 14; // 14-22px，大小适中
                const randomDelay = Math.random() * 6; // 0-6s，动画错开

                // 赋值样式
                item.style.left = `${randomLeft}%`;
                item.style.color = randomColor;
                item.style.fontSize = `${randomSize}px`;
                item.style.animationDelay = `${randomDelay}s`;

                body.appendChild(item);

                // 字符消失后移除，避免内存占用
                setTimeout(() => {
                    item.remove();
                }, 6000);
            }
        }

        // 初始化生成，并且每3秒再生成一次，持续满屏
        createLoveText();
        setInterval(createLoveText, 3000);
    </script>
</body>
</html>

