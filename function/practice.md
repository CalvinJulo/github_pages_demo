---
layout: default
title: Vocabulary Practice Lab
---

# ✍️ Vocabulary Practice Lab

<div id="quiz-box" style="padding: 20px; border: 2px solid #333; border-radius: 12px; background: #fff;">
  <p style="color: #666;">Can you spell the word for this definition?</p>
  
  <div id="definition-area" style="min-height: 80px; margin-bottom: 20px;">
    <h3 id="live-definition">Loading definition...</h3>
    <em id="live-phonetic" style="color: #007bff;"></em>
  </div>

  <input type="text" id="user-input" placeholder="Type the word here..." 
         style="width: 100%; padding: 10px; font-size: 1.2rem; border: 1px solid #ccc;">
  
  <div style="margin-top: 15px;">
    <button onclick="checkAnswer()" style="padding: 10px 20px; background: #28a745; color: white; border: none; cursor: pointer;">Check Answer</button>
    <button onclick="nextQuestion()" style="padding: 10px 20px; background: #6c757d; color: white; border: none; cursor: pointer;">Skip</button>
  </div>

  <p id="feedback" style="margin-top: 15px; font-weight: bold;"></p>
  
  <hr>
  <p>Deep Dive: 
    <a id="oxford-link" href="#" target="_blank" style="margin-right: 10px;">Oxford Dictionary ↗</a>
    <a id="cambridge-link" href="#" target="_blank">Cambridge Dictionary ↗</a>
  </p>
</div>

<script>
  const vocab = {{ site.data.vocab | jsonify }};
  let currentIndex = 0;

  // Function to fetch data from Free Dictionary API
  async function fetchDefinition(word) {
    try {
      const response = await fetch(`https://api.dictionaryapi.dev/api/v2/entries/en/${word}`);
      const data = await response.json();
      return {
        definition: data[0].meanings[0].definitions[0].definition,
        phonetic: data[0].phonetic || ""
      };
    } catch (error) {
      return { definition: "Could not load definition.", phonetic: "" };
    }
  }

  async function loadQuestion() {
    const currentWord = vocab[currentIndex].word;
    document.getElementById('live-definition').innerText = "Fetching definition...";
    document.getElementById('feedback').innerText = "";
    document.getElementById('user-input').value = "";

    // 1. Fetch from API
    const info = await fetchDefinition(currentWord);
    document.getElementById('live-definition').innerText = info.definition;
    document.getElementById('live-phonetic').innerText = info.phonetic;

    // 2. Update External Links (Scheme A)
    document.getElementById('oxford-link').href = `https://www.oxfordlearnersdictionaries.com/definition/english/${currentWord}`;
    document.getElementById('cambridge-link').href = `https://dictionary.cambridge.org/dictionary/english/${currentWord}`;
  }

  function checkAnswer() {
    const input = document.getElementById('user-input').value.trim().toLowerCase();
    const correct = vocab[currentIndex].word.toLowerCase();
    const feedback = document.getElementById('feedback');

    if (input === correct) {
      feedback.innerHTML = "✅ Correct! Well done.";
      feedback.style.color = "green";
      setTimeout(nextQuestion, 2000);
    } else {
      feedback.innerHTML = `❌ Incorrect. The word starts with "${correct[0]}..."`;
      feedback.style.color = "red";
    }
  }

  function nextQuestion() {
    currentIndex = (currentIndex + 1) % vocab.length;
    loadQuestion();
  }

  // Initial Load
  loadQuestion();
</script>
