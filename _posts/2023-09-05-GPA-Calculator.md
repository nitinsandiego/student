---
toc: false
comments: false
layout: post
title: GPA Calculator
description: Add your grade and crets and my GPA calculator will give you your GPA
courses: {csp: {week: 3}}
type: tangibles
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GPA Calculator</title>
</head>
<body>
    <section>
        <form id="gpaForm">
            <label for="courseName">Course Name:</label>
            <input type="text" id="courseName" required>
            <br>
            <label for="creditHours">Credit Hours:</label>
            <input type="number" id="creditHours" required>
            <br>
            <label for="grade">Grade:</label>
            <input type="text" id="grade" required>
            <br>
            <button type="button" id="calculateButton">Add Course</button>
        </form>
        <div id="results">
            <p>Total Credits: <span id="totalCreditHours">0</span></p>
            <p>GPA: <span id="gpa">0.00</span></p>
        </div>
    </section>
    <script>
        // GPA calculation function
        function calculateGPA() {
            const courseName = document.getElementById("courseName").value;
            const creditHours = parseFloat(document.getElementById("creditHours").value);
            const grade = document.getElementById("grade").value.toUpperCase();
            if (!courseName || isNaN(creditHours) || !grade) {
                alert("Please fill in all fields.");
                return;
            }
            // GPA scale (adjust as needed)
            const gradeScale = {
                A: 4.0,
                Aminus: 3.7,
                Bplus: 3.3,
                B: 3.0,
                Bminus: 2.7,
                Cplus: 2.3,
                C: 2.0,
                Cminus: 1.7,
                D: 1.0,
                F: 0.0,
            };
            if (gradeScale[grade] === undefined) {
                alert("Invalid grade entered.");
                return;
            }
            const currentTotalCreditHours = parseFloat(document.getElementById("totalCreditHours").textContent);
            const currentGPA = parseFloat(document.getElementById("gpa").textContent);
            const newTotalCreditHours = currentTotalCreditHours + creditHours;
            const weightedGPA = (creditHours * gradeScale[grade]) + (currentTotalCreditHours * currentGPA);
            const newGPA = weightedGPA / newTotalCreditHours;
            document.getElementById("totalCreditHours").textContent = newTotalCreditHours.toFixed(1);
            document.getElementById("gpa").textContent = newGPA.toFixed(2);
            // Clear input fields
            document.getElementById("courseName").value = "";
            document.getElementById("creditHours").value = "";
            document.getElementById("grade").value = "";
        }
        // Add event listener for the "Add Course" button
        document.getElementById("calculateButton").addEventListener("click", calculateGPA);
    </script>
</body>
</html>
