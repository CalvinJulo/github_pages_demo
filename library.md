---
layout: default
title: Book Library
---

# 📚 English Textbook Library

<div style="margin-bottom: 30px;">
  <input type="text" id="bookSearch" onkeyup="searchBooks()" placeholder="Search by title, publisher or level..." 
         style="width: 100%; padding: 12px; font-size: 16px; border: 2px solid #007bff; border-radius: 8px;">
</div>

<hr>

<div id="bookList" style="display: flex; flex-wrap: wrap; gap: 20px;">
  {% for book in site.data.books %}
  <div class="book-card" style="border: 1px solid #ddd; padding: 15px; border-radius: 10px; width: 250px; background: #f9f9f9;">
    <h3 class="title">{{ book.title }}</h3>
    <p><strong>Publisher:</strong> <span class="publisher">{{ book.publisher }}</span></p>
    <p><strong>Level:</strong> <span class="level">{{ book.level }}</span></p>
    <p style="font-size: 0.9em; color: #666;">Category: {{ book.category }}</p>
  </div>
  {% endfor %}
</div>

<script>
function searchBooks() {
  // Get input value and convert to lowercase
  let input = document.getElementById('bookSearch').value.toLowerCase();
  let cards = document.getElementsByClassName('book-card');

  // Loop through all book cards
  for (let i = 0; i < cards.length; i++) {
    let title = cards[i].querySelector('.title').innerText.toLowerCase();
    let publisher = cards[i].querySelector('.publisher').innerText.toLowerCase();
    let level = cards[i].querySelector('.level').innerText.toLowerCase();

    // If matches, show; otherwise, hide
    if (title.includes(input) || publisher.includes(input) || level.includes(input)) {
      cards[i].style.display = "";
    } else {
      cards[i].style.display = "none";
    }
  }
}
</script>
