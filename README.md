<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hubbardston Budget</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f0fff0;
            color: #2d572c;
        }
        nav {
            background-color: #2d572c;
            padding: 10px;
            text-align: center;
        }
        nav a {
            color: white;
            text-decoration: none;
            margin: 0 15px;
            font-size: 18px;
            cursor: pointer;
        }
        h1 {
            text-align: center;
        }
        section {
            padding: 20px;
            text-align: center;
        }
        table {
            width: 90%;
            margin: 20px auto;
            border-collapse: collapse;
            background-color: #ffffff;
        }
        th, td {
            border: 1px solid #2d572c;
            padding: 10px;
            text-align: left;
        }
        th {
            background-color: #6dbb6d;
            color: white;
        }
        .back-to-top {
            display: block;
            margin: 20px auto;
            padding: 10px 20px;
            background-color: #2d572c;
            color: white;
            text-decoration: none;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <nav>
        <a onclick="navigateToSection('General Government')">General Gov</a>
        <a onclick="navigateToSection('Public Safety')">Public Safety</a>
        <a onclick="navigateToSection('Public Works')">Public Works</a>
        <a onclick="navigateToSection('Education')">Education</a>
    </nav>
    
    <section id="budget">
        <h1>Hubbardston Budget</h1>
        <table id="budgetTable">
            <thead>
                <tr id="tableHead"></tr>
            </thead>
            <tbody id="tableBody"></tbody>
        </table>
        <a href="#" class="back-to-top">Back to Top</a>
    </section>
    
    <script>
        async function loadBudgetData() {
            const response = await fetch('https://raw.githubusercontent.com/NBoudreauMA/hubbardston-budget/main/BUDGET_1.csv');
            const data = await response.text();
            const rows = data.split('\n').map(row => row.split(','));
            
            const tableHead = document.getElementById('tableHead');
            const tableBody = document.getElementById('tableBody');
            
            tableHead.innerHTML = rows[0].map(header => `<th>${header}</th>`).join('');
            
            rows.slice(1).forEach(row => {
                const tr = document.createElement('tr');
                tr.innerHTML = row.map(cell => `<td>${cell}</td>`).join('');
                tableBody.appendChild(tr);
            });
        }
        
        function navigateToSection(sectionName) {
            const rows = document.querySelectorAll("#tableBody tr");
            for (let row of rows) {
                if (row.cells[0] && row.cells[0].innerText.includes(sectionName)) {
                    row.scrollIntoView({ behavior: "smooth", block: "start" });
                    break;
                }
            }
        }
        
        loadBudgetData();
    </script>
</body>
</html>
