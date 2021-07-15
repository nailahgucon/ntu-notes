---
title: Data Structures and Algorithms - Data Structures
---

## Data Structures 

<div class="tab">
  <a class="tablinks" onclick="openTab(event, 'linked-list')" id="defaultOpen">Linked List</a>
  <a class="tablinks" onclick="openTab(event, 'stack-and-queue')">Stack and Queue</a>
  <a class="tablinks" onclick="openTab(event, 'binary-tree')">Binary Tree</a>
  <a class="tablinks" onclick="openTab(event, 'binary-search-tree')">Binary Search Tree</a>
</div>

<div id="linked-list" class="tabcontent">
    <h3 style="text-align:center">Linked List</h3><br>
    <div class="card-div">
    {%- for post in collections.1107-data-structures-linked-list-code -%}
    <div class="card">
    <h3>{{ post.data.pageTitle }}</h3>
    <p class="card-p"><a href="{{ post.url }}" class="card-a">Go to page to view &raquo;</a></p>
    </div>
    {%- endfor -%}
    </div>
</div>

<div id="stack-and-queue" class="tabcontent">
    <h3 style="text-align:center">Stack and Queue</h3><br>
    <div class="card-div">
    {%- for post in collections.1107-data-structures-stack-and-queue-code -%}
    <div class="card">
    <h3>{{ post.data.pageTitle }}</h3>
    <p class="card-p"><a href="{{ post.url }}" class="card-a">Go to page to view &raquo;</a></p>
    </div>
    {%- endfor -%}
</div>
</div>

<div id="binary-tree" class="tabcontent">
  <h3 style="text-align:center">Binary Tree</h3><br>
    <div class="card-div">
    {%- for post in collections.1107-data-structures-binary-tree-code -%}
    <div class="card">
    <h3>{{ post.data.pageTitle }}</h3>
    <p class="card-p"><a href="{{ post.url }}" class="card-a">Go to page to view &raquo;</a></p>
    </div>
    {%- endfor -%}
</div>
</div>

<div id="binary-search-tree" class="tabcontent">
    <h3 style="text-align:center">Binary Search Tree</h3><br>
    <div class="card-div">
    {%- for post in collections.1107-data-structures-binary-search-tree-code -%}
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