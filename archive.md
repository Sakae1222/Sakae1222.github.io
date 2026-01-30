---
layout: page
title: Archive
---

<div class="archive-selector" style="margin-bottom: 30px;">
  <button id="btn-tags" class="toggle-btn active" onclick="switchView('tags')">By Tag</button>
  <button id="btn-months" class="toggle-btn" onclick="switchView('months')">By Month</button>
</div>

<hr>

<div id="archive-tags-view">
  {% for tag in site.tags %}
    <h3># {{ tag[0] }} <small>({{ tag[1] | size }})</small></h3>
    <ul class="clean-list">
      {% for post in tag[1] %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
      {% endfor %}
    </ul>
  {% endfor %}
</div>

<div id="archive-months-view" style="display: none;">
  {% assign postsByMonth = site.posts | group_by_exp: "post", "post.date | date: '%Y-%m'" %}
  {% for month in postsByMonth %}
    <h3>{{ month.name }} <small>({{ month.items | size }})</small></h3>
    <ul class="clean-list">
      {% for post in month.items %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
      {% endfor %}
    </ul>
  {% endfor %}
</div>

<style>
  /* Minimalist Button Style */
  .toggle-btn {
    padding: 6px 16px;
    cursor: pointer;
    border: 1px solid transparent; /* No border by default for cleaner look */
    background: #f0f0f0;
    border-radius: 20px; /* Pill shape */
    transition: all 0.2s ease;
    font-size: 14px;
    font-weight: 500;
    color: #666;
    margin: 0 5px;
  }
  .toggle-btn.active {
    background: #333; /* Dark for English/Tech blog feel */
    color: #fff;
  }
  .toggle-btn:hover {
    background: #e0e0e0;
  }
  .toggle-btn.active:hover {
    background: #555;
  }

  /* Clean Heading Style */
  h3 {
    margin-top: 2em;
    margin-bottom: 1em;
    font-weight: bold;
    color: #333;
  }
  h3 small {
    font-weight: normal;
    color: #999;
    font-size: 0.7em;
    margin-left: 5px;
  }

  /* Remove bullets and padding from lists */
  .clean-list {
    list-style-type: none; /* 去掉点点 */
    padding-left: 0;       /* 去掉左侧缩进 */
    margin-left: 5px;
  }
  .clean-list li {
    margin-bottom: 10px;
    line-height: 1.6;
  }
  .clean-list li a {
    text-decoration: none;
    color: #444; /* Slightly softer black for links */
  }
  .clean-list li a:hover {
    color: #000;
    text-decoration: underline;
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
