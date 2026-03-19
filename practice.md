---
layout: default
title: Recite vocabulary
---

# Core vocabulary

<div id="quiz-container" style="padding: 20px; border: 2px solid #007bff; border-radius: 10px;">
  <p>请默写以下单词的英文：</p>
  <h2 id="chinese-hint">正在加载...</h2>
  <input type="text" id="user-input" placeholder="输入英文单词" style="font-size: 1.5rem; width: 100%;">
  <button onclick="checkAnswer()" style="margin-top: 10px; padding: 10px 20px;">检查答案</button>
  <p id="feedback" style="font-weight: bold; margin-top: 10px;"></p>
</div>

<script>
  // 这里的 site.data.vocab 会被 Jekyll 在部署时转成 JS 数组
  const words = {{ site.data.vocab | jsonify }};
  let currentIndex = 0;

  function showQuestion() {
    document.getElementById('chinese-hint').innerText = words[currentIndex].meaning;
    document.getElementById('user-input').value = "";
    document.getElementById('feedback').innerText = "";
  }

  function checkAnswer() {
    const input = document.getElementById('user-input').value.trim().toLowerCase();
    const correct = words[currentIndex].word.toLowerCase();
    const feedback = document.getElementById('feedback');

    if (input === correct) {
      feedback.innerText = "✅ 太棒了！正确！";
      feedback.style.color = "green";
      // 2秒后自动切换下一题
      setTimeout(() => {
        currentIndex = (currentIndex + 1) % words.length;
        showQuestion();
      }, 2000);
    } else {
      feedback.innerText = "❌ 不对哦，再检查一下拼写。";
      feedback.style.color = "red";
    }
  }

  // 初始化第一题
  showQuestion();
</script>
