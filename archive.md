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

<div style="margin-bottom: 2rem; text-align: center;">
  <button onclick="showArchive('byTag')" id="btnTag" style="padding: 8px 16px; margin: 0 8px; border: 1px solid #e0ddd0; background: #91AD70; color: white; border-radius: 6px; cursor: pointer; font-weight: bold;">By Tag</button>
  <button onclick="showArchive('byMonth')" id="btnMonth" style="padding: 8px 16px; margin: 0 8px; border: 1px solid #e0ddd0; background: white; color: #666; border-radius: 6px; cursor: pointer;">By Month</button>
</div>

<!-- By Tag Archive -->
<div id="archiveByTag">
  {% for tag in site.tags %}
    <h3>{{ tag[0] }}</h3>
    <ul>
      {% for post in tag[1] %}
        <li><a href="{{ post.url }}">{{ post.date | date: "%B %Y" }} - {{ post.title }}</a></li>
      {% endfor %}
    </ul>
  {% endfor %}
</div>

<!-- By Month Archive -->
<div id="archiveByMonth" style="display: none;">
  {% assign postsByYearMonth = site.posts | group_by_exp: "post", "post.date | date: '%Y-%m'" %}
  
  {% for yearMonth in postsByYearMonth %}
    {% assign year = yearMonth.name | slice: 0, 4 %}
    {% assign month = yearMonth.name | slice: 5, 2 %}
    
    {% comment %}Convert month number to name{% endcomment %}
    {% case month %}
      {% when '01' %}{% assign monthName = 'January' %}
      {% when '02' %}{% assign monthName = 'February' %}
      {% when '03' %}{% assign monthName = 'March' %}
      {% when '04' %}{% assign monthName = 'April' %}
      {% when '05' %}{% assign monthName = 'May' %}
      {% when '06' %}{% assign monthName = 'June' %}
      {% when '07' %}{% assign monthName = 'July' %}
      {% when '08' %}{% assign monthName = 'August' %}
      {% when '09' %}{% assign monthName = 'September' %}
      {% when '10' %}{% assign monthName = 'October' %}
      {% when '11' %}{% assign monthName = 'November' %}
      {% when '12' %}{% assign monthName = 'December' %}
    {% endcase %}
    
    <h3>{{ monthName }} {{ year }} ({{ yearMonth.items | size }} posts)</h3>
    <ul>
      {% for post in yearMonth.items %}
        <li>
          <span>{{ post.date | date: "%d" }}</span> - 
          <a href="{{ post.url }}">{{ post.title }}</a>
        </li>
      {% endfor %}
    </ul>
  {% endfor %}
</div>

<script>
function showArchive(type) {
  const byTag = document.getElementById('archiveByTag');
  const byMonth = document.getElementById('archiveByMonth');
  const btnTag = document.getElementById('btnTag');
  const btnMonth = document.getElementById('btnMonth');
  
  if (type === 'byTag') {
    byTag.style.display = 'block';
    byMonth.style.display = 'none';
    btnTag.style.background = '#91AD70';
    btnTag.style.color = 'white';
    btnTag.style.fontWeight = 'bold';
    btnMonth.style.background = 'white';
    btnMonth.style.color = '#666';
    btnMonth.style.fontWeight = 'normal';
  } else {
    byTag.style.display = 'none';
    byMonth.style.display = 'block';
    btnTag.style.background = 'white';
    btnTag.style.color = '#666';
    btnTag.style.fontWeight = 'normal';
    btnMonth.style.background = '#91AD70';
    btnMonth.style.color = 'white';
    btnMonth.style.fontWeight = 'bold';
  }
}
</script>
