<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSV Viewer</title>
    <style>
        body { font-family: Arial, sans-serif; background-color: #f4f4f4; padding: 20px; }
        table { width: 100%; border-collapse: collapse; background: white; }
        th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
        th { background-color: #4CAF50; color: white; }
    </style>
</head>
<body>
    <h2>CSV Data Viewer</h2>
    <table id="csvTable">
        <thead><tr id="tableHead"></tr></thead>
        <tbody id="tableBody"></tbody>
    </table>

    <script>
        const CSV_URL = "https://raw.githubusercontent.com/NBoudreauMA/hubbardston-budget/refs/heads/main/BUDGET_1";
        
        async function fetchCSV() {
            try {
                const response = await fetch(CSV_URL);
                if (!response.ok) {
                    throw new Error("Failed to fetch CSV file.");
                }
                const text = await response.text();
                const rows = text.split("\n").map(row => row.split(","));
                
                if (rows.length > 1) {
                    document.getElementById("tableHead").innerHTML = rows[0].map(header => `<th>${header}</th>`).join("");
                    document.getElementById("tableBody").innerHTML = rows.slice(1).map(row => 
                        `<tr>${row.map(cell => `<td>${cell}</td>`).join("")}</tr>`
                    ).join("");
                }
            } catch (error) {
                console.error("Error fetching CSV:", error);
                document.body.innerHTML += `<p style='color:red;'>Failed to load CSV file. Please check the URL.</p>`;
            }
        }
        
        fetchCSV();
    </script>
</body>
</html>
