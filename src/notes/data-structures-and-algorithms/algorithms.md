---
title: Data Structures and Algorithms - Algorithms
---

## Algorithms

<div class="tab">
  <a class="tablinks" onclick="openTab(event, 'algebraic-expressions')" id="defaultOpen">Algebraic Expressions</a>
  <a class="tablinks" onclick="openTab(event, 'hashing')">Hashing</a>
  <a class="tablinks" onclick="openTab(event, 'graph')">Graph</a>
</div>

<div id="algebraic-expressions" class="tabcontent">
    <h3 style="text-align:center">Algebraic Expressions</h3><br>
    <div class="card-div">
    {%- for post in collections.1107-algorithms-algebraic-expressions-code -%}
    <div class="card">
    <h3>{{ post.data.pageTitle }}</h3>
    <p class="card-p"><a href="{{ post.url }}" class="card-a">Go to page to view &raquo;</a></p>
    </div>
    {%- endfor -%}
    </div>
</div>

<div id="hashing" class="tabcontent">
    <h3 style="text-align:center">Hashing</h3><br>
    <div class="card-div">
    {%- for post in collections.1107-algorithms-hashing-code -%}
    <div class="card">
    <h3>{{ post.data.pageTitle }}</h3>
    <p class="card-p"><a href="{{ post.url }}" class="card-a">Go to page to view &raquo;</a></p>
    </div>
    {%- endfor -%}
</div>
</div>

<div id="graph" class="tabcontent">
    <h3 style="text-align:center">Graph</h3><br>
    <div class="card-div">
    {%- for post in collections.1107-algorithms-graphs-code -%}
    <div class="card">
    <h3>{{ post.data.pageTitle }}</h3>
    <p class="card-p"><a href="{{ post.url }}" class="card-a">Go to page to view &raquo;</a></p>
    </div>
    {%- endfor -%}
</div>
</div>

<p><a href="/notes/data-structures-and-algorithms/"><bold>&#8656;</bold> Back to Data Structures and Algorithms</a></p>

<script>
function openTab(evt, tabName) {
  var i, tabcontent, tablinks;
  tabcontent = document.getElementsByClassName("tabcontent");
  for (i = 0; i < tabcontent.length; i++) {
    tabcontent[i].style.display = "none";
  }
  tablinks = document.getElementsByClassName("tablinks");
  for (i = 0; i < tablinks.length; i++) {
    tablinks[i].className = tablinks[i].className.replace(" active", "");
  }
  document.getElementById(tabName).style.display = "block";
  evt.currentTarget.className += " active";
}

// Get the element with id="defaultOpen" and click on it
document.getElementById("defaultOpen").click();
</script>