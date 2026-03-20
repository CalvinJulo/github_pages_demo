---
layout: default
title: Datamuse & OneLook Dictionary
---

<div id="onelook-section" style="margin-bottom: 40px;">
    <h2>🔍 第一板块：OneLook 深度定义</h2>
    <p style="color: #666; font-size: 0.9em;">聚合 Oxford, Cambridge, Merriam-Webster 等权威词典结果</p>

    <div style="display: flex; gap: 10px; margin-bottom: 20px;">
        <input type="text" id="onelook-input" placeholder="输入单词或短语 (如: resilient)" 
               style="flex: 1; padding: 12px; font-size: 1.1rem; border: 2px solid #007bff; border-radius: 8px;">
        <button onclick="searchOneLook()" 
                style="padding: 10px 25px; background: #007bff; color: white; border: none; border-radius: 8px; cursor: pointer; font-weight: bold;">
            查询词典
        </button>
    </div>

    <div id="onelook-container" style="position: relative; width: 100%; height: 700px; border: 1px solid #ddd; border-radius: 12px; overflow: hidden; background: #f9f9f9;">
        <div id="onelook-loader" style="display: none; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);">
            <p>正在连接 OneLook 数据库...</p>
        </div>
        
        <iframe id="onelook-frame" src="about:blank" 
                style="width: 100%; height: 100%; border: none;" 
                onload="hideLoader()">
        </iframe>
    </div>
</div>

<script>
    /**
     * 核心逻辑：更新 Iframe 地址
     * 拼接 URL：https://www.onelook.com/?w={word}
     */
    function searchOneLook() {
        const word = document.getElementById('onelook-input').value.trim();
        const frame = document.getElementById('onelook-frame');
        const loader = document.getElementById('onelook-loader');

        if (word) {
            // 显示加载动画
            loader.style.display = 'block';
            // 拼接 OneLook 查询链接
            // ls=a 参数尝试让页面布局更紧凑（如果 OneLook 支持的话）
            frame.src = `https://www.onelook.com/?w=${encodeURIComponent(word)}`;
        } else {
            alert("请输入要查询的单词！");
        }
    }

    function hideLoader() {
        document.getElementById('onelook-loader').style.display = 'none';
    }

    // 支持回车搜索
    document.getElementById('onelook-input').addEventListener('keypress', function (e) {
        if (e.key === 'Enter') {
            searchOneLook();
        }
    });
</script>
