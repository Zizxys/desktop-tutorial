<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday</title>
    <!-- 引入字体 -->
    <link href="https://fonts.googleapis.com/css?family=Montez" rel="stylesheet">
    <style>
        * {
            padding: 0;
            margin: 0;
        }
        html {
            height: 100%;
        }
        body {
            background-color: mistyrose;
            font-family: 'Montez', cursive;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100%;
            width: 100%;
            /* 背景渐变 */
            background-image: linear-gradient(-225deg, #231557 0%, #43107a 29%, #FF1361 100%);
            position: relative; /* 让子元素绝对定位 */
            overflow: hidden; /* 防止出现滚动条 */
        }
        canvas {
            position: fixed;
            width: 100%;
            height: 100%;
        }
        .shell {
            display: block;
            width: 1024px;
            height: 200px;
            margin:  auto;
        }
        span {
            color: transparent;
        }
        .left {
            display: block;
            float: left;
            height: 100%;
            width: 50%;
            /* 定义形状左半圆 */
            shape-outside: polygon(29.67% 13px, 99.08% 2.68%, 99.08% 19.57%, 94.58% 18.47%, 90.15% 15.59%, 76.89% 11.65%, 67.74% 13.97%, 61.33% 16.73%, 56.6% 23.07%, 52.94% 29.8%, 53.59% 44.23%, 61.86% 57.33%, 73.33% 68.73%, 99.6% 87%, -3px 84.73%);
        }
        .right {
            display: block;
            float: right;
            height: 100%;
            width: 50%;
            /* 定义形状右半圆 */
            shape-outside: polygon(70.33% 13px, 0.92% 2.68%, 0.92% 19.57%, 5.42% 18.47%, 9.85% 15.59%, 23.11% 11.65%, 32.26% 13.97%, 38.67% 16.73%, 43.4% 23.07%, 47.06% 29.8%, 46.41% 44.23%, 38.14% 57.33%, 26.67% 68.73%, 0.4% 87%, 353px 84.73%);
        }
        p {
            text-align: justify;
            text-justify: inter-word;
            font-size: 2vw;
            line-height: 1.5;
            color: #fff;
            position: relative;
            padding: 0 50px;
        }
        /* 媒体查询 */
        @media only screen and (orientation: landscape) {
            p {
                text-align: justify;
                text-justify: inter-word;
                font-size: 1.8vw;
                line-height: 1.5;
                color: #fff;
                position: relative;
            }
            .shell {
                display: block;
                width: 100%;
                height: 100%;
                margin:  auto;
            }

        }

        p:before {
            content: "Happy Birthday";
            position: absolute;
            font-size: 3vw;
            top: -1vh;
            right: 0;
            left: 20px;
            letter-spacing: 10px; /* 空隙 */
            word-spacing: 11px;
            text-align: center;
        }

        #span2 {
            color: inherit;
        }

    </style>
</head>
<body>
<canvas></canvas>
<div class="shell">
    <div class="left"></div>
    <div class="right"></div>
    <p >
         Today marks a significant milestone in your life as you officially step into adulthood. It’s a time full of possibilities and new adventures, and I hope you embrace every moment with enthusiasm and courage.

        As you embark on this exciting journey, remember that it’s okay to dream big and explore the world around you. This is the time to discover your passions, challenge yourself, and grow. I believe you have incredible potential, and I can't wait to see what you achieve in the coming years.

        With your high school exams just around the corner, I want to wish you complete focus and confidence. May you study hard, but also remember to take breaks and take care of yourself. You’ve worked so hard to get to this point, and I have no doubt that you will perform brilliantly. Trust in yourself and your abilities, and the results will reflect your dedication.

        As you celebrate this special day, enjoy the love and support of your friends and family. We are all cheering you on as you step into this new chapter of your life.


        <span id="span2"></span>
    </p>
</div>
</body>
<script>
    // 定义星星的颜色
    const STAR_COLOR = '#fff';
    // 定义星星的大小
    const STAR_SIZE = 3;
    // 定义星星的最小缩放比例
    const STAR_MIN_SCALE = 0.2;
    // 定义溢出阈值
    const OVERFLOW_THRESHOLD = 50;
    // 定义星星的数量
    const STAR_COUNT = (window.innerWidth + window.innerHeight) / 8;

    // 获取canvas元素
    const canvas = document.querySelector('canvas');
    // 获取canvas的绘图上下文
    const context = canvas.getContext('2d');
    // 定义缩放比例
    let scale = 1; // device pixel ratio
    // 定义宽度和高度
    let width;
    let height;
    // 定义星星数组
    let stars = [];
    // 定义鼠标指针的位置
    let pointerX;
    let pointerY;
    // 定义速度对象
    let velocity = { x: 0, y: 0, tx: 0, ty: 0, z: 0.0009 };
    // 定义触摸输入标志
    let touchInput = false;

    // 生成星星
    generate();
    // 调整大小
    resize();
    // 运行动画
    step();
    // 当窗口大小改变时，重新调整大小
    window.onresize = resize;
    // 当鼠标在canvas上移动时，更新鼠标指针位置
    canvas.onmousemove = onMouseMove;
    // 当触摸屏在canvas上移动时，更新鼠标指针位置
    canvas.ontouchmove = onTouchMove;
    // 当触摸屏离开canvas时，更新鼠标指针位置
    canvas.ontouchend = onMouseLeave;
    // 当鼠标离开文档时，更新鼠标指针位置
    document.onmouseleave = onMouseLeave;

    // 生成星星
    function generate() {
        for (let i = 0; i < STAR_COUNT; i++) {
            stars.push({
                x: 0,
                y: 0,
                z: STAR_MIN_SCALE + Math.random() * (1 - STAR_MIN_SCALE),
            });
        }
    }

    // 将星星放置到随机位置
    function placeStar(star) {
        star.x = Math.random() * width;
        star.y = Math.random() * height;
    }

    // 回收星星并重新放置到新的位置
    function recycleStar(star) {
        // 初始化方向为 'z'
        let direction = 'z';
        // 获取速度的绝对值
        let vx = Math.abs(velocity.x);
        let vy = Math.abs(velocity.y);

        // 如果速度的绝对值大于1，则根据速度的大小随机确定方向
        if (vx > 1 || vy > 1) {
            let axis;
            // 如果水平速度大于垂直速度，则根据水平速度的比例随机确定水平或垂直方向
            if (vx > vy) {
                axis = Math.random() < vx / (vx + vy) ? 'h' : 'v';
            } else {
                axis = Math.random() < vy / (vx + vy) ? 'v' : 'h';
            }

            // 根据方向确定具体的移动方向
            if (axis === 'h') {
                direction = velocity.x > 0 ? 'l' : 'r';
            } else {
                direction = velocity.y > 0 ? 't' : 'b';
            }
        }

        // 随机设置星星的缩放比例
        star.z = STAR_MIN_SCALE + Math.random() * (1 - STAR_MIN_SCALE);

        // 根据方向设置星星的位置
        if (direction === 'z') {
            // 如果方向为 'z'，则将星星放置在屏幕中心
            star.z = 0.1;
            star.x = Math.random() * width;
            star.y = Math.random() * height;
        } else if (direction === 'l') {
            // 如果方向为 'l'，则将星星放置在屏幕左侧
            star.x = -OVERFLOW_THRESHOLD;
            star.y = height * Math.random();
        } else if (direction === 'r') {
            // 如果方向为 'r'，则将星星放置在屏幕右侧
            star.x = width + OVERFLOW_THRESHOLD;
            star.y = height * Math.random();
        } else if (direction === 't') {
            // 如果方向为 't'，则将星星放置在屏幕顶部
            star.x = width * Math.random();
            star.y = -OVERFLOW_THRESHOLD;
        } else if (direction === 'b') {
            // 如果方向为 'b'，则将星星放置在屏幕底部
            star.x = width * Math.random();
            star.y = height + OVERFLOW_THRESHOLD;
        }
    }

    // 调整大小
    function resize() {
        // 获取设备像素比例
        scale = window.devicePixelRatio || 1;
        // 设置画布的宽度和高度
        width = window.innerWidth * scale;
        height = window.innerHeight * scale;
        canvas.width = width;
        canvas.height = height;
        // 将所有星星重新放置到屏幕上
        stars.forEach(placeStar);
    }

    // 动画的每一帧
    function step() {
        // 清空画布
        context.clearRect(0, 0, width, height);
        // 更新星星的位置和速度
        update();
        // 绘制星星
        render();
        // 请求下一帧动画
        requestAnimationFrame(step);
    }

    // 更新星星的位置和速度
    function update() {
        // 缓动速度
        velocity.tx *= 0.96;
        velocity.ty *= 0.96;
        // 更新速度
        velocity.x += (velocity.tx - velocity.x) * 0.8;
        velocity.y += (velocity.ty - velocity.y) * 0.8;

        // 遍历所有星星
        stars.forEach((star) => {
            // 根据速度和缩放比例更新星星的位置
            star.x += velocity.x * star.z;
            star.y += velocity.y * star.z;
            // 根据速度和缩放比例更新星星的位置（使星星围绕屏幕中心旋转）
            star.x += (star.x - width / 2) * velocity.z * star.z;
            star.y += (star.y - height / 2) * velocity.z * star.z;
            // 更新星星的缩放比例
            star.z += velocity.z;

            // 如果星星超出屏幕范围，则重新放置到屏幕上
            if (
                star.x < -OVERFLOW_THRESHOLD ||
                star.x > width + OVERFLOW_THRESHOLD ||
                star.y < -OVERFLOW_THRESHOLD ||
                star.y > height + OVERFLOW_THRESHOLD
            ) {
                recycleStar(star);
            }
        });
    }

    // 绘制星星
    function render() {
        // 遍历所有星星
        stars.forEach((star) => {
            // 设置绘制星星的样式
            context.beginPath();
            context.lineCap = 'round';
            context.lineWidth = STAR_SIZE * star.z * scale;
            context.globalAlpha = 0.5 + 0.5 * Math.random();
            context.strokeStyle = STAR_COLOR;

            // 绘制星星的路径
            context.beginPath();
            context.moveTo(star.x, star.y);
            // 计算星星的尾巴坐标
            let tailX = velocity.x * 2;
            let tailY = velocity.y * 2;

            // 如果尾巴坐标的绝对值小于0.1，则设置为0.5
            if (Math.abs(tailX) < 0.1) tailX = 0.5;
            if (Math.abs(tailY) < 0.1) tailY = 0.5;

            // 绘制星星的尾巴
            context.lineTo(star.x + tailX, star.y + tailY);
            context.stroke();
        });
    }

    // 移动鼠标指针
    function movePointer(x, y) {
        // 如果之前有记录鼠标指针的位置，则计算鼠标指针的移动距离，并更新速度
        if (typeof pointerX === 'number' && typeof pointerY === 'number') {
            let ox = x - pointerX;
            let oy = y - pointerY;
            velocity.tx = velocity.tx + (ox / 8) * scale * (touchInput ? 1 : -1);
            velocity.ty = velocity.ty + (oy / 8) * scale * (touchInput ? 1 : -1);
        }
        // 更新鼠标指针的位置
        pointerX = x;
        pointerY = y;
    }

    // 当鼠标在canvas上移动时的事件处理函数
    function onMouseMove(event) {
        touchInput = false;
        movePointer(event.clientX, event.clientY);
    }

    // 当触摸屏在canvas上移动时的事件处理函数
    function onTouchMove(event) {
        touchInput = true;
        movePointer(event.touches[0].clientX, event.touches[0].clientY, true);
        event.preventDefault();
    }

    // 当鼠标离开canvas时的事件处理函数
    function onMouseLeave() {
        pointerX = null;
        pointerY = null;
    }
</script>
</html>
