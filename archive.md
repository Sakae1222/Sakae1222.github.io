<!--
---
layout: page
title: Archive
---

{% for tag in site.tags %}
  <h3>{{ tag[0] }}</h3>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.date | date: "%B %Y" }} - {{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}
-->

---
layout: page
title: Archive
---

<div class="archive-selector" style="margin-bottom: 20px;">
  <button id="btn-tags" class="toggle-btn active" onclick="switchView('tags')">按标签 ({{ site.tags | size }})</button>
  <button id="btn-months" class="toggle-btn" onclick="switchView('months')">按月份</button>
</div>

<hr>

<div id="archive-tags-view">
  {% for tag in site.tags %}
    <h3># {{ tag[0] }} <small style="font-weight: normal; color: #888;">({{ tag[1] | size }})</small></h3>
    <ul>
      {% for post in tag[1] %}
        <li><a href="{{ post.url }}">{{ post.date | date: "%Y-%m-%d" }} - {{ post.title }}</a></li>
      {% endfor %}
    </ul>
  {% endfor %}
</div>

<div id="archive-months-view" style="display: none;">
  {% assign postsByMonth = site.posts | group_by_exp: "post", "post.date | date: '%Y-%m'" %}
  {% for month in postsByMonth %}
    <h3>{{ month.name }} <small style="font-weight: normal; color: #888;">({{ month.items | size }} 篇)</small></h3>
    <ul>
      {% for post in month.items %}
        <li>
          <span style="color: #999; font-family: monospace; margin-right: 10px;">{{ post.date | date: "%d日" }}</span>
          <a href="{{ post.url }}">{{ post.title }}</a>
        </li>
      {% endfor %}
    </ul>
  {% endfor %}
</div>

<style>
  .toggle-btn {
    padding: 6px 15px;
    cursor: pointer;
    border: 1px solid #e0e0e0;
    background: #fafafa;
    border-radius: 20px; /* 圆角看起来更现代一点 */
    transition: all 0.2s ease;
    font-size: 14px;
    outline: none;
  }
  .toggle-btn.active {
    background: #3498db; /* 经典蓝色，你可以换成你喜欢的颜色 */
    color: white;
    border-color: #3498db;
    box-shadow: 0 2px 5px rgba(52,152,219,0.3);
  }
  .toggle-btn:hover {
    background: #eee;
  }
  .toggle-btn.active:hover {
    background: #2980b9;
  }
  h3 {
    margin-top: 1.5em;
    border-bottom: 1px solid #eee;
    padding-bottom: 5px;
  }
  ul {
    list-style-type: none;
    padding-left: 10px;
  }
  li {
    margin-bottom: 8px;
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
