---
toc: true
comments: false
layout: post
title: Formula 1 Teams Table
description: This my table of Formula 1 Teams.
courses: {csp: {week: 2}}
type: hacks
---
<input type="text" id="myInput" onkeyup="myFunction()" placeholder="Search for teams..">

<table id="myTable" class="table">
    <thead>
        <tr>
            <th>Team Name</th>
            <th>Driver 1</th>
            <th>Driver 2</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Mercedes AMG Petronas Formula 1 Team</td>
            <td>Lewis Hamilton</td>
            <td>George Russell</td>
        </tr>
        <tr>
            <td>Red Bull Racing</td>
            <td>Max Verstappen</td>
            <td>Sergio Perez</td>
        </tr>
        <tr>
            <td>Scuderia Ferrari</td>
            <td>Charles Leclerc</td>
            <td>Carlos Sainz</td>
        </tr>
        <tr>
            <td>Mclaren Racing</td>
            <td>Lando Norris</td>
            <td>Oscar Piastri</td>
        </tr>
        <tr>
            <td>Alpine</td>
            <td>Pierre Gasly</td>
            <td>Esteban Ocon</td>
        </tr>
        <tr>
            <td>Williams Racing</td>
            <td>Alexander Albon</td>
            <td>Logan Sargeant</td>
        </tr>
        <tr>
            <td>Alfa Romeo Racing</td>
            <td>Valterri Bottas</td>
            <td>Zhou Guanyu</td>
        </tr>
        <tr>
            <td>Alphatauri</td>
            <td>Daniel Ricciardo</td>
            <td>Yuki Tsunoda</td>
        </tr>
        <tr>
            <td>Haas</td>
            <td>Kevin Magnussen</td>
            <td>Nico Hülkenberg</td>
        </tr>
        <tr>
            <td>Aston Martin Racing</td>
            <td>Fernando Alonso</td>
            <td>Lance Stroll</td>
        </tr>
    </tbody>
</table>

<script>
function myFunction() {
  // Declare variables 
  var input, filter, table, tr, td, i, txtValue;
  input = document.getElementById("myInput");
  filter = input.value.toUpperCase();
  table = document.getElementById("myTable");
  tr = table.getElementsByTagName("tr");

  // Loop through all table rows, and hide those who don't match the search query
  for (i = 0; i < tr.length; i++) {
    td = tr[i].getElementsByTagName("td")[0];
    if (td) {
      txtValue = td.textContent || td.innerText;
      if (txtValue.toUpperCase().indexOf(filter) > -1) {
        tr[i].style.display = "";
      } else {
        tr[i].style.display = "none";
      }
    } 
  }
}
</script>