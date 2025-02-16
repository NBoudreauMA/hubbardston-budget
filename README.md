import React, { useState, useEffect } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Table, TableHead, TableRow, TableCell, TableBody } from "@/components/ui/table";
import { Button } from "@/components/ui/button";
import Papa from "papaparse";

const CSV_URL = "https://raw.githubusercontent.com/NBoudreauMA/hubbardston-budget/main/CURRENT%20-%20FY26%20Working%20Budget%20(1)(Expenditures%20By%20Category).csv";

const App = () => {
  const [data, setData] = useState([]);
  const [headers, setHeaders] = useState([]);

  useEffect(() => {
    fetch(CSV_URL)
      .then((response) => response.text())
      .then((text) => {
        Papa.parse(text, {
          header: true,
          skipEmptyLines: true,
          dynamicTyping: true,
          transformHeader: (header) => header.trim(),
          complete: (result) => {
            let cleanData = result.data.map(row => {
              let cleanedRow = {};
              Object.keys(row).forEach(key => {
                const trimmedKey = key.trim();
                if (trimmedKey) {
                  cleanedRow[trimmedKey] = row[key]?.toString().trim() || "-";
                }
              });
              return cleanedRow;
            }).filter(row => Object.values(row).some(value => value !== ""));
            
            if (cleanData.length > 0) {
              const validHeaders = Object.keys(cleanData[0]).filter(header => header);
              setHeaders(validHeaders);
              setData(
                cleanData.map(row =>
                  validHeaders.reduce((acc, header) => {
                    acc[header] = row[header] || "-";
                    return acc;
                  }, {})
                )
              );
            }
          },
        });
      })
      .catch((error) => console.error("Error fetching CSV:", error));
  }, []);

  return (
    <div className="min-h-screen bg-green-100 p-4">
      <nav className="bg-green-600 p-4 text-white text-xl font-bold shadow-md">Hubbardston Budget Viewer</nav>
      <div className="container mx-auto mt-6">
        <Card>
          <CardContent>
            <Table>
              <TableHead>
                <TableRow>
                  {headers.map((header, index) => (
                    <TableCell key={index} className="font-bold">{header}</TableCell>
                  ))}
                </TableRow>
              </TableHead>
              <TableBody>
                {data.map((row, rowIndex) => (
                  <TableRow key={rowIndex}>
                    {headers.map((header, cellIndex) => (
                      <TableCell key={cellIndex}>{row[header]}</TableCell>
                    ))}
                  </TableRow>
                ))}
              </TableBody>
            </Table>
          </CardContent>
        </Card>
      </div>
    </div>
  );
};

export default App;
