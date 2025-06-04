<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>小北的时光邮局</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #e0f7fa, #f8bbd0, #e1bee7);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            overflow-x: hidden;
        }
        
        /* 登录界面 */
        .login-container {
            width: 100%;
            max-width: 400px;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
            padding: 40px 30px;
            text-align: center;
            transform: translateY(0);
            transition: transform 0.8s ease-out, opacity 0.8s ease-out;
            position: relative;
            overflow: hidden;
        }
        
        .login-container::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 8px;
            background: linear-gradient(to right, #64b5f6, #e91e63, #ff9800);
        }
        
        .login-title {
            color: #5c6bc0;
            font-size: 28px;
            margin-bottom: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
        }
        
        .login-title i {
            font-size: 32px;
        }
        
        .login-form {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        
        .input-group {
            position: relative;
        }
        
        .input-group i {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: #64b5f6;
            font-size: 18px;
        }
        
        .login-input {
            width: 100%;
            padding: 14px 20px 14px 50px;
            border: 2px solid #e3f2fd;
            border-radius: 12px;
            font-size: 16px;
            transition: all 0.3s;
            outline: none;
        }
        
        .login-input:focus {
            border-color: #64b5f6;
            box-shadow: 0 0 0 3px rgba(100, 181, 246, 0.2);
        }
        
        .login-btn {
            background: linear-gradient(to right, #64b5f6, #e91e63);
            color: white;
            border: none;
            padding: 14px;
            border-radius: 12px;
            font-size: 18px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            margin-top: 10px;
            box-shadow: 0 5px 15px rgba(100, 181, 246, 0.4);
        }
        
        .login-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(100, 181, 246, 0.6);
        }
        
        .brands {
            display: flex;
            justify-content: center;
            gap: 25px;
            margin: 30px 0;
        }
        
        .brand {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 20px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s;
        }
        
        .brand:hover {
            transform: translateY(-5px);
        }
        
        .brand:nth-child(1) { background: #4caf50; color: white; }
        .brand:nth-child(2) { background: #2196f3; color: white; }
        .brand:nth-child(3) { background: #ff5722; color: white; }
        .brand:nth-child(4) { background: #9c27b0; color: white; }
        
        .login-footer {
            color: #777;
            font-size: 14px;
            margin-top: 20px;
            line-height: 1.6;
        }
        
        /* 游戏主容器 */
        .game-container {
            width: 100%;
            max-width: 900px;
            height: 90vh;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            display: flex;
            flex-direction: column;
            overflow: hidden;
            position: relative;
            display: none;
        }
        
        /* 顶部状态栏 */
        .status-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 20px;
            background: linear-gradient(to right, #e3f2fd, #bbdefb);
            border-bottom: 2px solid #90caf9;
            position: relative;
        }
        
        .player-info {
            display: flex;
            gap: 15px;
        }
        
        .info-box {
            background: white;
            padding: 6px 15px;
            border-radius: 20px;
            display: flex;
            align-items: center;
            gap: 8px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            font-weight: 500;
        }
        
        .info-box i {
            color: #ff9800;
        }
        
        .announcement {
            position: absolute;
            bottom: -25px;
            left: 0;
            right: 0;
            background: linear-gradient(to right, #ffecb3, #ffccbc);
            padding: 6px 20px;
            font-size: 13px;
            text-align: center;
            color: #e91e63;
            font-weight: 500;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            white-space: nowrap;
            overflow: hidden;
        }
        
        .announcement-content {
            display: inline-block;
            padding-left: 100%;
            animation: marquee 20s linear infinite;
        }
        
        @keyframes marquee {
            0% { transform: translateX(0); }
            100% { transform: translateX(-100%); }
        }
        
        /* 游戏主区域 */
        .game-area {
            display: flex;
            flex: 1;
            position: relative;
            overflow: hidden;
        }
        
        /* 左侧邮局区域 */
        .post-office {
            width: 70%;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100"><rect fill="%23e1f5fe" width="100" height="100"/><path fill="%23b3e5fc" d="M20,20 L80,20 L80,80 L20,80 Z M30,30 L50,30 L50,50 L30,50 Z M60,40 L70,40 L70,60 L60,60 Z"/></svg>');
            background-size: 200px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            position: relative;
        }
        
        /* NPC小北 */
        .npc-container {
            position: absolute;
            bottom: 20px;
            left: 30px;
            z-index: 10;
        }
        
        .npc {
            width: 120px;
            height: 160px;
            position: relative;
            cursor: pointer;
        }
        
        .npc-body {
            position: absolute;
            bottom: 0;
            width: 100%;
            height: 120px;
            background: #64b5f6;
            border-radius: 60px 60px 0 0;
        }
        
        .npc-head {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 70px;
            height: 70px;
            background: #ffecb3;
            border-radius: 50%;
        }
        
        .npc-glasses {
            position: absolute;
            top: 30px;
            left: 50%;
            transform: translateX(-50%);
            width: 60px;
            height: 25px;
            background: #212121;
            border-radius: 15px;
            display: flex;
            justify-content: space-around;
            align-items: center;
        }
        
        .npc-glasses::before,
        .npc-glasses::after {
            content: '';
            width: 20px;
            height: 20px;
            background: #b3e5fc;
            border-radius: 50%;
        }
        
        .npc-smile {
            position: absolute;
            top: 55px;
            left: 50%;
            transform: translateX(-50%);
            width: 30px;
            height: 10px;
            background: #ff5722;
            border-radius: 0 0 15px 15px;
        }
        
        .speech-bubble {
            position: absolute;
            left: 140px;
            bottom: 100px;
            background: white;
            padding: 15px;
            border-radius: 15px;
            width: 200px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
            display: none;
            z-index: 20;
        }
        
        .speech-text {
            font-size: 14px;
            color: #333;
        }
        
        .speech-bubble::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 20px;
            border-width: 10px 10px 0;
            border-style: solid;
            border-color: white transparent transparent;
        }
        
        /* 工作台区域 */
        .workbench {
            background: rgba(255, 255, 255, 0.8);
            border-radius: 15px;
            padding: 15px;
            margin-top: 20px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            flex: 1;
            display: flex;
            flex-direction: column;
        }
        
        .section-title {
            font-size: 18px;
            color: #5c6bc0;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .letters-container {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-bottom: 20px;
            min-height: 120px;
        }
        
        .letter {
            width: 100px;
            height: 80px;
            background: #fff8e1;
            border-radius: 8px;
            display: flex;
            flex-direction: column;
            padding: 8px;
            cursor: grab;
            box-shadow: 0 3px 6px rgba(0,0,0,0.1);
            position: relative;
            overflow: hidden;
            transition: transform 0.2s;
        }
        
        .letter:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 10px rgba(0,0,0,0.15);
        }
        
        .letter-header {
            display: flex;
            justify-content: space-between;
            font-size: 10px;
            margin-bottom: 5px;
        }
        
        .letter-type {
            padding: 2px 5px;
            border-radius: 3px;
            font-size: 9px;
            color: white;
        }
        
        .letter-content {
            font-size: 11px;
            line-height: 1.3;
            overflow: hidden;
            text-overflow: ellipsis;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
        }
        
        .letter-address {
            font-size: 9px;
            margin-top: auto;
            color: #666;
        }
        
        .categories {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            padding: 10px 0;
        }
        
        .category {
            width: 150px;
            height: 100px;
            background: #f5f5f5;
            border: 2px dashed #bdbdbd;
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 10px;
        }
        
        .category-icon {
            font-size: 24px;
            margin-bottom: 8px;
        }
        
        .category-name {
            font-size: 14px;
            color: #616161;
        }
        
        /* 右侧功能区域 */
        .sidebar {
            width: 30%;
            background: #f5f5f5;
            padding: 20px;
            display: flex;
            flex-direction: column;
            gap: 25px;
            border-left: 2px solid #e0e0e0;
        }
        
        .stories-section, .decoration-section {
            background: white;
            border-radius: 15px;
            padding: 15px;
            box-shadow: 0 3px 8px rgba(0,0,0,0.05);
        }
        
        .stories-list {
            max-height: 200px;
            overflow-y: auto;
            margin-top: 10px;
        }
        
        .story-item {
            padding: 10px;
            border-bottom: 1px solid #eee;
            font-size: 13px;
            cursor: pointer;
            transition: background 0.2s;
        }
        
        .story-item:hover {
            background: #f0f7ff;
        }
        
        .story-title {
            font-weight: 600;
            color: #5c6bc0;
            margin-bottom: 3px;
        }
        
        .decoration-options {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 10px;
        }
        
        .decoration-item {
            width: 70px;
            height: 70px;
            background: #e1f5fe;
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .decoration-item:hover {
            transform: scale(1.05);
            background: #b3e5fc;
        }
        
        .decoration-icon {
            font-size: 24px;
            margin-bottom: 5px;
            color: #0288d1;
        }
        
        .decoration-name {
            font-size: 11px;
            color: #555;
        }
        
        /* 底部导航 */
        .nav-bar {
            display: flex;
            justify-content: space-around;
            background: #e3f2fd;
            padding: 10px 0;
            border-top: 2px solid #bbdefb;
        }
        
        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            cursor: pointer;
            padding: 5px 15px;
            border-radius: 10px;
            transition: background 0.2s;
        }
        
        .nav-item.active {
            background: #bbdefb;
        }
        
        .nav-item i {
            font-size: 20px;
            margin-bottom: 3px;
            color: #2196f3;
        }
        
        .nav-text {
            font-size: 12px;
            color: #1976d2;
        }
        
        /* 页面内容 */
        .page-content {
            flex: 1;
            padding: 20px;
            overflow-y: auto;
            display: none;
        }
        
        .page-title {
            color: #5c6bc0;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #e3f2fd;
        }
        
        .page-content.active {
            display: block;
        }
        
        /* 派送页面 */
        .delivery-map {
            background: #e1f5fe;
            border-radius: 15px;
            height: 300px;
            margin-bottom: 20px;
            position: relative;
            overflow: hidden;
        }
        
        .map-background {
            position: absolute;
            width: 100%;
            height: 100%;
            background: linear-gradient(to bottom, #81d4fa, #4fc3f7, #29b6f6);
            opacity: 0.6;
        }
        
        .mail-truck {
            position: absolute;
            left: 50px;
            top: 50%;
            width: 80px;
            height: 40px;
            background: #ff5722;
            border-radius: 10px;
            transition: left 0.5s, top 0.5s;
        }
        
        .mail-truck::before {
            content: '';
            position: absolute;
            width: 30px;
            height: 30px;
            background: #ffccbc;
            border-radius: 50%;
            top: 30px;
            left: 10px;
        }
        
        .mail-truck::after {
            content: '';
            position: absolute;
            width: 30px;
            height: 30px;
            background: #ffccbc;
            border-radius: 50%;
            top: 30px;
            left: 40px;
        }
        
        .delivery-point {
            position: absolute;
            width: 20px;
            height: 20px;
            background: #4caf50;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            box-shadow: 0 0 0 5px rgba(76, 175, 80, 0.3);
        }
        
        /* 赞助页面 */
        .sponsor-section {
            background: white;
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            margin-bottom: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
        }
        
        .sponsor-title {
            color: #e91e63;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        .wechat-qr {
            width: 180px;
            height: 180px;
            background: #f5f5f5;
            margin: 15px auto;
            border: 2px dashed #e0e0e0;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            color: #9e9e9e;
        }
        
        .contact-info {
            background: #fff8e1;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            color: #ff9800;
            margin-top: 20px;
        }
        
        .custom-website {
            background: #e8f5e9;
            padding: 20px;
            border-radius: 15px;
            margin-top: 30px;
        }
        
        .website-examples {
            display: flex;
            gap: 15px;
            margin-top: 15px;
            flex-wrap: wrap;
            justify-content: center;
        }
        
        .example {
            background: white;
            padding: 10px 15px;
            border-radius: 10px;
            box-shadow: 0 3px 8px rgba(0,0,0,0.1);
            font-size: 14px;
        }
        
        .example i {
            color: #e91e63;
            margin-right: 5px;
        }
        
        /* 信件类型颜色 */
        .domestic { background: #c8e6c9; border-left: 4px solid #4caf50; }
        .international { background: #ffecb3; border-left: 4px solid #ffc107; }
        .postcard { background: #ffccbc; border-left: 4px solid #ff5722; }
        .urgent { background: #f8bbd0; border-left: 4px solid #e91e63; }
        
        .type-domestic { color: #4caf50; }
        .type-international { color: #ff9800; }
        .type-postcard { color: #ff5722; }
        .type-urgent { color: #e91e63; }
        
        /* 动画效果 */
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
            100% { transform: translateY(0px); }
        }
        
        .npc {
            animation: float 3s ease-in-out infinite;
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .game-area {
                flex-direction: column;
            }
            
            .post-office, .sidebar {
                width: 100%;
            }
            
            .sidebar {
                height: 300px;
            }
        }
    </style>
</head>
<body>
    <!-- 登录界面 -->
    <div class="login-container" id="login-container">
        <h1 class="login-title"><i class="fas fa-envelope-open-text"></i>小北的时光邮局</h1>
        
        <div class="login-form">
            <div class="input-group">
                <i class="fas fa-user"></i>
                <input type="text" class="login-input" placeholder="用户名">
            </div>
            
            <div class="input-group">
                <i class="fas fa-lock"></i>
                <input type="password" class="login-input" placeholder="密码">
            </div>
            
            <button class="login-btn" id="login-btn">进入邮局</button>
        </div>
        
        <div class="brands">
            <div class="brand">B</div>
            <div class="brand">D</div>
            <div class="brand">D</div>
            <div class="brand">M</div>
        </div>
        
        <div class="login-footer">
            <p>欢迎来到时光邮局，这里收藏着来自世界各地人们的信件与心愿</p>
            <p>登录后即可开始整理信件，传递思念</p>
        </div>
    </div>
    
    <!-- 游戏主容器 -->
    <div class="game-container" id="game-container">
        <!-- 顶部状态栏 -->
        <div class="status-bar">
            <div class="player-info">
                <div class="info-box">
                    <i class="fas fa-user"></i>
                    <span>助手小安</span>
                </div>
                <div class="info-box">
                    <i class="fas fa-coins"></i>
                    <span id="coins">850</span>
                </div>
                <div class="info-box">
                    <i class="fas fa-star"></i>
                    <span>等级 5</span>
                </div>
            </div>
            <div class="info-box">
                <i class="fas fa-tasks"></i>
                <span>任务: 整理信件 (3/8)</span>
            </div>
            
            <div class="announcement">
                <div class="announcement-content">
                    <i class="fas fa-bullhorn"></i> 公告：有大佬有好的想法或者想参与进来可以联系我，让我们一起完善本网页游戏！想不想要一个自己的专属网站？加我微信：15236570751（鲜花）例如：与女朋友的恋爱日常；个人简历；简单的日常软件及你们的私人网站（可以选择在百度上公开或者自己使用，不会暴露任何自己消息）
                </div>
            </div>
        </div>
        
        <!-- 游戏主区域 -->
        <div class="game-area">
            <!-- 邮局页面 -->
            <div class="post-office" id="post-office">
                <!-- NPC小北 -->
                <div class="npc-container">
                    <div class="npc" id="npc">
                        <div class="npc-body"></div>
                        <div class="npc-head"></div>
                        <div class="npc-glasses"></div>
                        <div class="npc-smile"></div>
                    </div>
                    <div class="speech-bubble" id="speech-bubble">
                        <div class="speech-text">你好！我是小北，欢迎来到时光邮局！你能帮我整理这些信件吗？</div>
                    </div>
                </div>
                
                <!-- 工作台 -->
                <div class="workbench">
                    <h2 class="section-title">
                        <i class="fas fa-envelope"></i>信件整理工作台
                    </h2>
                    
                    <div class="letters-container" id="letters-container">
                        <!-- 信件会通过JS动态生成 -->
                    </div>
                    
                    <h2 class="section-title">
                        <i class="fas fa-folder-open"></i>分类区域
                    </h2>
                    
                    <div class="categories">
                        <div class="category" id="category-domestic">
                            <div class="category-icon type-domestic">
                                <i class="fas fa-home"></i>
                            </div>
                            <div class="category-name type-domestic">国内信件</div>
                        </div>
                        <div class="category" id="category-international">
                            <div class="category-icon type-international">
                                <i class="fas fa-globe-asia"></i>
                            </div>
                            <div class="category-name type-international">海外信件</div>
                        </div>
                        <div class="category" id="category-postcard">
                            <div class="category-icon type-postcard">
                                <i class="fas fa-image"></i>
                            </div>
                            <div class="category-name type-postcard">明信片</div>
                        </div>
                        <div class="category" id="category-urgent">
                            <div class="category-icon type-urgent">
                                <i class="fas fa-bolt"></i>
                            </div>
                            <div class="category-name type-urgent">加急信件</div>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- 右侧功能区域 -->
            <div class="sidebar">
                <div class="stories-section">
                    <h2 class="section-title">
                        <i class="fas fa-book-open"></i>故事收集
                    </h2>
                    <div class="stories-list" id="stories-list">
                        <div class="story-item">
                            <div class="story-title">奶奶的思念</div>
                            <div class="story-preview">亲爱的孙子，奶奶想你...</div>
                        </div>
                        <div class="story-item">
                            <div class="story-title">十年之约</div>
                            <div class="story-preview">给十年后的自己，希望你...</div>
                        </div>
                        <div class="story-item">
                            <div class="story-title">远方的祝福</div>
                            <div class="story-preview">虽然我们相隔千里，但...</div>
                        </div>
                    </div>
                </div>
                
                <div class="decoration-section">
                    <h2 class="section-title">
                        <i class="fas fa-paint-brush"></i>邮局装饰
                    </h2>
                    <div class="decoration-options">
                        <div class="decoration-item">
                            <div class="decoration-icon">
                                <i class="fas fa-couch"></i>
                            </div>
                            <div class="decoration-name">沙发</div>
                        </div>
                        <div class="decoration-item">
                            <div class="decoration-icon">
                                <i class="fas fa-plant"></i>
                            </div>
                            <div class="decoration-name">绿植</div>
                        </div>
                        <div class="decoration-item">
                            <div class="decoration-icon">
                                <i class="fas fa-palette"></i>
                            </div>
                            <div class="decoration-name">墙色</div>
                        </div>
                        <div class="decoration-item">
                            <div class="decoration-icon">
                                <i class="fas fa-rug"></i>
                            </div>
                            <div class="decoration-name">地毯</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 其他页面内容 -->
        <div class="page-content" id="delivery-page">
            <h2 class="page-title"><i class="fas fa-truck"></i> 信件派送</h2>
            
            <div class="delivery-map">
                <div class="map-background"></div>
                <div class="mail-truck" id="mail-truck"></div>
                <div class="delivery-point" style="top: 30px; left: 150px;">1</div>
                <div class="delivery-point" style="top: 100px; left: 300px;">2</div>
                <div class="delivery-point" style="top: 200px; left: 200px;">3</div>
            </div>
            
            <div class="sponsor-section">
                <h3 class="sponsor-title"><i class="fas fa-heart"></i> 支持我们</h3>
                <p>喜欢这个游戏吗？您的支持将帮助我们继续开发！</p>
                
                <div class="wechat-qr">
                    微信二维码<br>
                    15236570751
                </div>
                
                <div class="contact-info">
                    <i class="fas fa-comment"></i> 加微信：15236570751 支持我们
                </div>
            </div>
        </div>
        
        <div class="page-content" id="stories-page">
            <h2 class="page-title"><i class="fas fa-book"></i> 故事集</h2>
            
            <div class="stories-list">
                <div class="story-item">
                    <div class="story-title">奶奶的思念</div>
                    <div class="story-content">亲爱的孙子，奶奶想你了。自从你去了大城市工作，奶奶每天都会坐在门前的摇椅上，望着村口的方向。记得你小时候最喜欢吃奶奶做的桂花糕，今年桂花开了，奶奶又做了很多，等你回来吃...</div>
                </div>
                <div class="story-item">
                    <div class="story-title">十年之约</div>
                    <div class="story-content">亲爱的未来的我，当你打开这封信时，已经过去十年了。现在的我23岁，刚刚大学毕业，对未来充满期待又有些迷茫。不知道十年后的你是否实现了梦想？是否还保持着对生活的热情？...</div>
                </div>
                <div class="story-item">
                    <div class="story-title">远方的祝福</div>
                    <div class="story-content">亲爱的陌生人，虽然我们素未谋面，但我希望这封信能给你带来温暖。生活总有不如意的时候，但请相信，在世界的某个角落，有人正在为你祝福。愿你每天都能发现生活中的小确幸...</div>
                </div>
            </div>
        </div>
        
        <div class="page-content" id="decoration-page">
            <h2 class="page-title"><i class="fas fa-paint-roller"></i> 装饰店</h2>
            
            <div class="decoration-options" style="justify-content: center;">
                <div class="decoration-item" style="width: 100px; height: 100px;">
                    <div class="decoration-icon">
                        <i class="fas fa-couch"></i>
                    </div>
                    <div class="decoration-name">邮局沙发</div>
                    <div class="decoration-price">200金币</div>
                </div>
                <div class="decoration-item" style="width: 100px; height: 100px;">
                    <div class="decoration-icon">
                        <i class="fas fa-plant"></i>
                    </div>
                    <div class="decoration-name">绿植装饰</div>
                    <div class="decoration-price">150金币</div>
                </div>
                <div class="decoration-item" style="width: 100px; height: 100px;">
                    <div class="decoration-icon">
                        <i class="fas fa-palette"></i>
                    </div>
                    <div class="decoration-name">墙面粉刷</div>
                    <div class="decoration-price">300金币</div>
                </div>
                <div class="decoration-item" style="width: 100px; height: 100px;">
                    <div class="decoration-icon">
                        <i class="fas fa-rug"></i>
                    </div>
                    <div class="decoration-name">温馨地毯</div>
                    <div class="decoration-price">250金币</div>
                </div>
            </div>
            
            <div class="sponsor-section">
                <h3 class="sponsor-title"><i class="fas fa-gift"></i> 特别赞助</h3>
                <p>通过赞助获取专属装饰和金币奖励！</p>
                
                <div class="contact-info">
                    <i class="fas fa-comments"></i> 加微信：15236570751 获取专属装饰
                </div>
                
                <div class="custom-website">
                    <h4><i class="fas fa-star"></i> 专属网站定制服务</h4>
                    <p>想要一个自己的专属网站吗？我们可以为您定制：</p>
                    <div class="website-examples">
                        <div class="example"><i class="fas fa-heart"></i> 恋爱纪念网站</div>
                        <div class="example"><i class="fas fa-user-graduate"></i> 个人简历网站</div>
                        <div class="example"><i class="fas fa-blog"></i> 私人博客</div>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="page-content" id="settings-page">
            <h2 class="page-title"><i class="fas fa-cog"></i> 设置</h2>
            
            <div class="sponsor-section">
                <h3 class="sponsor-title"><i class="fas fa-hands-helping"></i> 赞助与支持</h3>
                <p>您的支持是我们持续开发的动力！</p>
                
                <div class="wechat-qr">
                    微信赞助二维码<br>
                    15236570751
                </div>
                
                <div class="contact-info">
                    <i class="fas fa-comment-dots"></i> 加微信：15236570751 支持我们
                </div>
            </div>
            
            <div class="custom-website">
                <h4><i class="fas fa-laptop-code"></i> 专属网站定制</h4>
                <p>想要一个展示你们爱情故事的网站？或者一个专业的个人简历网站？我们都可以为您定制！</p>
                <p>特点：</p>
                <ul style="text-align: left; padding-left: 30px; margin-top: 10px;">
                    <li>完全个性化设计</li>
                    <li>响应式布局，手机电脑都能完美展示</li>
                    <li>可选择公开在百度搜索或设为私人访问</li>
                    <li>不会泄露任何个人信息</li>
                </ul>
                
                <div class="contact-info" style="margin-top: 20px;">
                    <i class="fas fa-comments"></i> 立即咨询：微信 15236570751
                </div>
            </div>
        </div>
        
        <!-- 底部导航 -->
        <div class="nav-bar">
            <div class="nav-item active" data-page="post-office">
                <i class="fas fa-home"></i>
                <div class="nav-text">邮局</div>
            </div>
            <div class="nav-item" data-page="delivery-page">
                <i class="fas fa-truck"></i>
                <div class="nav-text">派送</div>
            </div>
            <div class="nav-item" data-page="stories-page">
                <i class="fas fa-book"></i>
                <div class="nav-text">故事集</div>
            </div>
            <div class="nav-item" data-page="decoration-page">
                <i class="fas fa-store"></i>
                <div class="nav-text">装饰店</div>
            </div>
            <div class="nav-item" data-page="settings-page">
                <i class="fas fa-cog"></i>
                <div class="nav-text">设置</div>
            </div>
        </div>
    </div>

    <script>
        // 游戏数据
        const letters = [
            {
                id: 1,
                type: 'domestic',
                title: '给奶奶的信',
                content: '奶奶，今年春节我一定回家看您，给您带最爱吃的点心...',
                address: '北京市海淀区',
                urgent: false
            },
            {
                id: 2,
                type: 'international',
                title: '留学日记',
                content: '亲爱的爸妈，我在英国一切都好，不用担心...',
                address: 'London, UK',
                urgent: false
            },
            {
                id: 3,
                type: 'postcard',
                title: '海边风景',
                content: '这里的海真美，希望下次能和你一起来！',
                address: '三亚市天涯区',
                urgent: false
            },
            {
                id: 4,
                type: 'urgent',
                title: '重要文件',
                content: '请尽快处理合同文件，截止日期临近...',
                address: '上海市浦东新区',
                urgent: true
            },
            {
                id: 5,
                type: 'domestic',
                title: '同学聚会',
                content: '老同学，下个月我们计划举办毕业十周年聚会...',
                address: '成都市锦江区',
                urgent: false
            },
            {
                id: 6,
                type: 'international',
                title: '生日祝福',
                content: '亲爱的，虽然不能陪你过生日，但礼物已经在路上...',
                address: 'New York, USA',
                urgent: false
            }
        ];

        // 初始化游戏
        document.addEventListener('DOMContentLoaded', function() {
            const loginContainer = document.getElementById('login-container');
            const gameContainer = document.getElementById('game-container');
            const loginBtn = document.getElementById('login-btn');
            const npc = document.getElementById('npc');
            const speechBubble = document.getElementById('speech-bubble');
            const mailTruck = document.getElementById('mail-truck');
            const navItems = document.querySelectorAll('.nav-item');
            const pageContents = document.querySelectorAll('.page-content');
            
            // 登录按钮事件
            loginBtn.addEventListener('click', function() {
                // 登录动画效果
                loginContainer.style.transform = 'translateY(-100vh)';
                loginContainer.style.opacity = '0';
                
                // 显示游戏主界面
                setTimeout(() => {
                    loginContainer.style.display = 'none';
                    gameContainer.style.display = 'flex';
                    
                    // 初始化游戏内容
                    initGame();
                }, 800);
            });
            
            // 初始化游戏内容
            function initGame() {
                const lettersContainer = document.getElementById('letters-container');
                
                // 生成信件
                letters.forEach(letter => {
                    const letterEl = document.createElement('div');
                    letterEl.className = `letter ${letter.type}`;
                    letterEl.dataset.id = letter.id;
                    letterEl.dataset.type = letter.type;
                    
                    let typeText = '';
                    let typeClass = '';
                    
                    switch(letter.type) {
                        case 'domestic':
                            typeText = '国内';
                            typeClass = 'type-domestic';
                            break;
                        case 'international':
                            typeText = '海外';
                            typeClass = 'type-international';
                            break;
                        case 'postcard':
                            typeText = '明信片';
                            typeClass = 'type-postcard';
                            break;
                        case 'urgent':
                            typeText = '加急';
                            typeClass = 'type-urgent';
                            break;
                    }
                    
                    letterEl.innerHTML = `
                        <div class="letter-header">
                            <span class="letter-type ${typeClass}">${typeText}</span>
                            ${letter.urgent ? '<span class="type-urgent"><i class="fas fa-bolt"></i></span>' : ''}
                        </div>
                        <div class="letter-content">${letter.title}</div>
                        <div class="letter-address">${letter.address}</div>
                    `;
                    
                    lettersContainer.appendChild(letterEl);
                });
                
                // NPC互动
                npc.addEventListener('click', function() {
                    if(speechBubble.style.display === 'block') {
                        speechBubble.style.display = 'none';
                    } else {
                        const messages = [
                            "你好！我是小北，欢迎来到时光邮局！",
                            "这些信件需要分类整理，你能帮帮我吗？",
                            "每封信都藏着一个感人的故事哦！",
                            "派送信件时小心路上的障碍物！",
                            "装饰邮局可以吸引更多客人来访！"
                        ];
                        const randomMsg = messages[Math.floor(Math.random() * messages.length)];
                        
                        speechBubble.innerHTML = `<div class="speech-text">${randomMsg}</div>`;
                        speechBubble.style.display = 'block';
                        setTimeout(() => {
                            speechBubble.style.display = 'none';
                        }, 5000);
                    }
                });
                
                // 显示初始对话
                setTimeout(() => {
                    speechBubble.style.display = 'block';
                    setTimeout(() => {
                        speechBubble.style.display = 'none';
                    }, 5000);
                }, 1000);
                
                // 简单拖拽功能实现
                const lettersEl = document.querySelectorAll('.letter');
                const categories = document.querySelectorAll('.category');
                
                // 为信件添加拖拽功能
                lettersEl.forEach(letter => {
                    letter.setAttribute('draggable', 'true');
                    
                    letter.addEventListener('dragstart', function(e) {
                        e.dataTransfer.setData('text/plain', this.dataset.id);
                        this.style.opacity = '0.5';
                    });
                    
                    letter.addEventListener('dragend', function() {
                        this.style.opacity = '1';
                    });
                });
                
                // 分类区域事件
                categories.forEach(category => {
                    category.addEventListener('dragover', function(e) {
                        e.preventDefault();
                    });
                    
                    category.addEventListener('drop', function(e) {
                        e.preventDefault();
                        const letterId = e.dataTransfer.getData('text/plain');
                        const letter = document.querySelector(`.letter[data-id="${letterId}"]`);
                        const letterType = letter.dataset.type;
                        const categoryType = this.id.split('-')[1];
                        
                        if(letterType === categoryType) {
                            // 正确分类
                            this.appendChild(letter);
                            letter.style.opacity = '1';
                            letter.style.cursor = 'default';
                            letter.draggable = false;
                            
                            // 增加金币
                            const coinsEl = document.getElementById('coins');
                            let coins = parseInt(coinsEl.textContent);
                            coins += 50;
                            coinsEl.textContent = coins;
                            
                            // 显示成功消息
                            speechBubble.innerHTML = '<div class="speech-text">太棒了！分类正确！继续加油！</div>';
                            speechBubble.style.display = 'block';
                            setTimeout(() => {
                                speechBubble.style.display = 'none';
                            }, 3000);
                        } else {
                            // 错误分类
                            speechBubble.innerHTML = '<div class="speech-text">这个分类不太对哦，再试试看？</div>';
                            speechBubble.style.display = 'block';
                            setTimeout(() => {
                                speechBubble.style.display = 'none';
                            }, 3000);
                        }
                    });
                });
                
                // 派送卡车动画
                let position = 0;
                setInterval(() => {
                    position = (position + 1) % 3;
                    switch(position) {
                        case 0:
                            mailTruck.style.left = "50px";
                            mailTruck.style.top = "50%";
                            break;
                        case 1:
                            mailTruck.style.left = "300px";
                            mailTruck.style.top = "100px";
                            break;
                        case 2:
                            mailTruck.style.left = "200px";
                            mailTruck.style.top = "200px";
                            break;
                    }
                }, 2000);
            }
            
            // 导航切换
            navItems.forEach(item => {
                item.addEventListener('click', function() {
                    // 更新活动导航项
                    navItems.forEach(nav => nav.classList.remove('active'));
                    this.classList.add('active');
                    
                    // 隐藏所有页面内容
                    pageContents.forEach(page => page.classList.remove('active'));
                    
                    // 显示选中的页面内容
                    const pageId = this.dataset.page;
                    document.getElementById(pageId).classList.add('active');
                    
                    // 特殊处理邮局页面
                    if(pageId === 'post-office') {
                        document.getElementById('post-office').style.display = 'flex';
                    } else {
                        document.getElementById('post-office').style.display = 'none';
                    }
                });
            });
        });
    </script>
</body>
</html>
