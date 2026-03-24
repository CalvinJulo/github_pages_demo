
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My Pages Portal</title>
    <style>
        :root { --sidebar-w: 250px; --header-bg: #1a1a1b; }
        body { margin: 0; display: flex; height: 100vh; font-family: sans-serif; overflow: hidden; }
        
        /* 侧边栏样式 */
        #sidebar { 
            width: var(--sidebar-w); background: #f4f7f9; 
            border-right: 1px solid #ddd; transition: 0.3s;
            display: flex; flex-direction: column;
        }
        #sidebar.hidden { margin-left: calc(var(--sidebar-w) * -1); }
        
        .nav-header { padding: 20px; font-weight: 800; border-bottom: 1px solid #eee; }
        .nav-item { 
            padding: 15px 20px; cursor: pointer; text-decoration: none; 
            color: #333; border-bottom: 1px solid #eee; display: block;
        }
        .nav-item:hover { background: #e9ecef; }

        /* 右侧内容区 */
        #main { flex-grow: 1; display: flex; flex-direction: column; position: relative; }
        iframe { width: 100%; flex-grow: 1; border: none; }

        /* 隐藏/显示按钮 */
        #toggle-btn {
            position: absolute; left: 10px; top: 10px; z-index: 100;
            background: var(--header-bg); color: white; border: none;
            padding: 8px 12px; cursor: pointer; border-radius: 4px; opacity: 0.7;
        }
        #toggle-btn:hover { opacity: 1; }
    </style>
</head>
<body>

    <nav id="sidebar">
        <div class="nav-header">NAVIGATION</div>
        <a href="./function/practice" target="content-frame" class="nav-item">📚 Library</a>
        <a href="./function/practice" target="content-frame" class="nav-item">✍️ Practice</a>
        <a href="./function/dictionary" target="content-frame" class="nav-item">🔀 Dictionary</a>
        <div style="margin-top: auto; padding: 20px; font-size: 10px; color: #999;">PORTAL V1.0</div>
    </nav>

    <main id="main">
        <button id="toggle-btn" onclick="toggleSidebar()">☰ MENU</button>
        <iframe name="content-frame" src="word_shuffler.html"></iframe>
    </main>

    <script>
        function toggleSidebar() {
            document.getElementById('sidebar').classList.toggle('hidden');
        }
    </script>
</body>
</html>
