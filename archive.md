---
layout: page
title: Archive
---

<div class="archive-selector" style="margin-bottom: 25px;">
  <button id="btn-tags" class="toggle-btn active" onclick="switchView('tags')">By Tag ({{ site.tags | size }})</button>
  <button id="btn-months" class="toggle-btn" onclick="switchView('months')">By Month</button>
</div>

<hr>

<div id="archive-tags-view">
  {% for tag in site.tags %}
    <details class="archive-details">
      <summary class="archive-summary">
        <span class="summary-title"># {{ tag[0] }}</span>
        <span class="summary-count">({{ tag[1] | size }})</span>
      </summary>
      <ul class="post-list">
        {% for post in tag[1] %}
          <li><a href="{{ post.url }}">{{ post.title }}</a></li>
        {% endfor %}
      </ul>
    </details>
  {% endfor %}
</div>

<div id="archive-months-view" style="display: none;">
  {% assign postsByYear = site.posts | group_by_exp: "post", "post.date | date: '%Y'" %}
  
  {% for year in postsByYear %}
    <details class="archive-details" {% if forloop.first %}open{% endif %}>
      <summary class="archive-summary">
        <span class="summary-title">{{ year.name }}</span>
        <span class="summary-count">({{ year.items | size }})</span>
      </summary>
      
      <div style="padding-left: 20px; border-left: 1px solid #eee; margin-top: 10px;">
        {% assign monthsInYear = year.items | group_by_exp: "item", "item.date | date: '%Y-%m'" %}
        {% for month in monthsInYear %}
          <h4 class="month-heading">{{ month.name }} <small>({{ month.items | size }})</small></h4>
          <ul class="post-list">
            {% for post in month.items %}
              <li><a href="{{ post.url }}">{{ post.title }}</a></li>
            {% endfor %}
          </ul>
        {% endfor %}
      </div>
    </details>
  {% endfor %}
</div>

<style>
  /* Toggle Buttons Style */
  .toggle-btn {
    padding: 8px 18px;
    cursor: pointer;
    border: 1px solid #ddd;
    background: #fff;
    border-radius: 6px;
    transition: all 0.2s ease;
    font-size: 14px;
    font-weight: 500;
  }
  .toggle-btn.active {
    background: #333; /* Dark theme style */
    color: #fff;
    border-color: #333;
  }

  /* Folding Style */
  .archive-details {
    margin-bottom: 15px;
  }
  .archive-summary {
    cursor: pointer;
    padding: 10px;
    background: #f9f9f9;
    border-radius: 4px;
    list-style: none; /* Hide default arrow in some browsers */
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .archive-summary::-webkit-details-marker {
    display: none; /* Hide arrow for Safari */
  }
  .archive-summary:hover {
    background: #f0f0f0;
  }
  .summary-title {
    font-size: 1.2em;
    font-weight: bold;
  }
  .summary-count {
    color: #888;
    font-size: 0.9em;
  }

  /* List Style */
  .post-list {
    list-style: square;
    padding-left: 35px;
    margin-top: 10px;
  }
  .post-list li {
    margin-bottom: 8px;
  }
  .month-heading {
    margin: 20px 0 10px 0;
    color: #555;
    font-size: 1em;
    border-bottom: 1px dashed #ddd;
    display: inline-block;
  }
</style>

<script>
function switchView(type) {
  const tagsView = document.getElementById('archive-tags-view');
  const monthsView = document.getElementById('archive-months-view');
  const btnTags = document.getElementById('btn-tags');
  const btnMonths = document.getElementById('btn-months');

  if (type === 'tags') {
    tagsView.style.display = 'block';
    monthsView.style.display = 'none';
    btnTags.classList.add('active');
    btnMonths.classList.remove('active');
  } else {
    tagsView.style.display = 'none';
    monthsView.style.display = 'block';
    btnTags.classList.remove('active');
    btnMonths.classList.add('active');
  }
}
</script>
