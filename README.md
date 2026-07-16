<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Designer Portfolio - Acid & Minimalist</title>
    <!-- 引入高质感无衬线字体 -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=Inter:wght@300;400;600&display=swap" rel="stylesheet">
    
    <style>
        /* ==========================================
           1. 基础重置与变量定义
           ========================================== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body, html {
            width: 100%;
            height: 100%;
            font-family: 'Inter', sans-serif;
            background-color: #0d0d0d;
            color: #ffffff;
            overflow-x: hidden;
        }

        /* ==========================================
           2. 酸性背景与噪点滤镜 (核心视觉)
           ========================================== */
        .acid-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -2;
            /* 酸性高饱和渐变：电蓝色 (#0055ff) 与 鲜橙色 (#ff5500) 的剧烈碰撞 */
            background: radial-gradient(circle at 20% 30%, #ff5500 0%, transparent 50%),
                        radial-gradient(circle at 80% 70%, #0055ff 0%, transparent 60%),
                        linear-gradient(135deg, #0d0d0d 0%, #1a0033 100%);
            background-size: 120% 120%;
            filter: contrast(1.1) saturate(1.2);
        }

        /* 使用 SVG 噪点滤镜生成颗粒质感 */
        .noise-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -1;
            opacity: 0.05; /* 控制颗粒的分寸感，5% 既有质感又不会喧宾夺主 */
            pointer-events: none;
        }

        /* ==========================================
           3. 极简主义排版与负空间
           ========================================== */
        header {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            padding: 40px 60px;
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            z-index: 10;
        }

        .logo {
            font-family: 'Syne', sans-serif;
            font-weight: 800;
            font-size: 1.2rem;
            letter-spacing: -0.05em;
            text-transform: uppercase;
        }

        .meta-info {
            font-size: 0.75rem;
            font-family: 'Inter', sans-serif;
            line-height: 1.6;
            color: rgba(255, 255, 255, 0.7);
            text-align: right;
        }

        /* 首屏主容器 */
        .hero-section {
            width: 100%;
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            padding: 0 10%;
        }

        /* 非对称大标题 */
        .hero-title-wrap {
            position: absolute;
            left: 10%;
            bottom: 15%;
            max-width: 800px;
            z-index: 1;
        }

        .hero-title {
            font-family: 'Syne', sans-serif;
            font-size: clamp(3rem, 8vw, 7.5rem); /* 响应式巨幅文字 */
            font-weight: 800;
            line-height: 0.9;
            letter-spacing: -0.04em;
            text-transform: uppercase;
        }

        /* ==========================================
           4. 玻璃拟态物理气泡 (Glassmorphism Sphere)
           ========================================== */
        .glass-sphere-container {
            position: absolute;
            top: 35%;
            right: 15%;
            width: 350px;
            height: 350px;
            z-index: 2;
        }

        .glass-sphere {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            /* 模拟玻璃表面的微弱高光和暗部 */
            background: radial-gradient(circle at 30% 30%, rgba(255, 255, 255, 0.2) 0%, rgba(255, 255, 255, 0) 70%);
            /* 关键效果：让穿过球体的背景产生模糊和扭曲感 */
            backdrop-filter: blur(12px) contrast(1.2);
            -webkit-backdrop-filter: blur(12px) contrast(1.2);
            border: 1px solid rgba(255, 255, 255, 0.15);
            box-shadow: 
                inset 0 20px 30px rgba(255, 255, 255, 0.15),
                inset 10px 0 10px rgba(0, 0, 0, 0.2),
                inset -10px 0 10px rgba(255, 255, 255, 0.1),
                0 30px 60px rgba(0, 0, 0, 0.3);
            /* 漂浮动画 */
            animation: float 8s ease-in-out infinite alternate;
        }

        /* 精致的微型标签元素 */
        .sphere-tag {
            position: absolute;
            top: -20px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 0.7rem;
            letter-spacing: 0.2em;
            color: rgba(255, 255, 255, 0.6);
            border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 4px 12px;
            border-radius: 20px;
            background: rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(5px);
        }

        /* ==========================================
           5. 动画效果
           ========================================== */
        @keyframes float {
            0% {
                transform: translateY(0px) rotate(0deg);
            }
            100% {
                transform: translateY(-25px) rotate(5deg);
            }
        }

        /* 极简向下滚动指示器 */
        .scroll-indicator {
            position: absolute;
            bottom: 40px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 0.75rem;
            letter-spacing: 0.1em;
            opacity: 0.6;
            text-transform: uppercase;
        }
    </style>
</head>
<body>

    <!-- 1. 酸性渐变背景 -->
    <div class="acid-bg"></div>

    <!-- 2. SVG 噪点叠加层（利用浏览器原生的 SVG 噪点生成器，无需外部图片） -->
    <svg class="noise-overlay" xmlns="http://www.w3.org/2000/svg">
        <filter id="noiseFilter">
            <feTurbulence type="fractalNoise" baseFrequency="0.8" numOctaves="3" stitchTiles="stitch"/>
        </filter>
        <rect width="100%" height="100%" filter="url(#noiseFilter)"/>
    </svg>

    <!-- 3. 极简页眉 (Header) -->
    <header>
        <div class="logo">ACID.STUDIO</div>
        <div class="meta-info">
            PORTFOLIO 2026 // EDITION 01<br>
            SHINAGAWA, TOKYO [35.62° N, 139.73° E]
        </div>
    </header>

    <!-- 4. 首屏主展区 (Hero Section) -->
    <main class="hero-section">
        
        <!-- 非对称大标题 -->
        <div class="hero-title-wrap">
            <h1 class="hero-title">
                CURATED<br>
                DISTORTION.
            </h1>
        </div>

        <!-- 3D 悬浮透镜气泡 -->
        <div class="glass-sphere-container">
            <div class="sphere-tag">INTERACTIVE SPHERE</div>
            <div class="glass-sphere"></div>
        </div>

        <!-- 滚动提示 -->
        <div class="scroll-indicator">Scroll to Explore ↓</div>

    </main>

</body>
</html>

