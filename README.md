<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hubbardston FY26 Budget - General Government</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        header {
            background: #003366;
            color: white;
            padding: 20px;
            text-align: center;
        }
        .container {
            width: 90%;
            margin: 20px auto;
            background: white;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h2 {
            border-bottom: 2px solid #0055A4;
            padding-bottom: 5px;
        }
        .table-container {
            overflow-x: auto;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }
        th, td {
            padding: 10px;
            border: 1px solid #ddd;
            text-align: left;
        }
        th {
            background: #0055A4;
            color: white;
        }
    </style>
</head>
<body>
    <header>
        <h1>Hubbardston FY26 Budget - General Government</h1>
    </header>
    
    <div class="container">
        <h2>General Government</h2>
        <div class="table-container">
            <table id="budget-table">
                <thead>
                    <tr>
                        <th>Department</th>
                        <th>Category</th>
                        <th>FY24 Actual</th>
                        <th>FY25 Requested</th>
                        <th>FY25 Actual</th>
                        <th>FY26 Dept</th>
                        <th>FY26 Admin</th>
                        <th>Change ($)</th>
                        <th>Change (%)</th>
                    </tr>
                </thead>
                <tbody>
                </tbody>
            </table>
        </div>
    </div>

    <script>
        async function loadCSV() {
            const response = await fetch('https://raw.githubusercontent.com/NBoudreauMA/hubbardston-budget/refs/heads/main/CURRENT%20-%20FY26%20Working%20Budget%20(1)(Expenditures%20By%20Category).csv'); // Replace with the actual CSV URL
            const data = await response.text();
            const rows = data.split('\n').slice(1);
            const tableBody = document.querySelector('#budget-table tbody');
            
            rows.forEach(row => {
                const cols = row.split(',');
                if (cols.length > 1) {
                    const tr = document.createElement('tr');
                    cols.forEach(col => {
                        const td = document.createElement('td');
                        td.textContent = col.trim();
                        tr.appendChild(td);
                    });
                    tableBody.appendChild(tr);
                }
            });
        }
        
        loadCSV();
    </script>
</body>
</html>
