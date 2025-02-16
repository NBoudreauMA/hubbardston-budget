// Install dependencies before running
// npm install react lucide-react

import React, { useState } from 'react';

import { Menu } from 'lucide-react';

// Card Component
export const Card = ({ children }) => (
  <div className="bg-white shadow-md rounded-lg p-4">{children}</div>
);

export const CardContent = ({ children }) => <div>{children}</div>;

export const CardHeader = ({ children }) => (
  <div className="border-b p-4 font-bold">{children}</div>
);

export const CardTitle = ({ children }) => <h2 className="text-lg">{children}</h2>;

const BudgetProposal = () => {
  const [activeDept, setActiveDept] = useState('GENERAL GOVERNMENT');
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);

  const budgetData = {
    'GENERAL GOVERNMENT': [
      { item: "Moderator", fy24: 100, fy25: 100, fy25Actual: 100, fy26Dept: 100, fy26Admin: 100, change: 0, changePct: "0.00%" },
      { item: "Select Board", fy24: 77161, fy25: 76473, fy25Actual: 76473, fy26Dept: 86170, fy26Admin: 86648, change: 10175, changePct: "13.31%" },
      { item: "Town Admin", fy24: 121253, fy25: 120400, fy25Actual: 119400, fy26Dept: 120800, fy26Admin: 122766, change: 3366, changePct: "2.82%" },
      { item: "Finance Committee", fy24: 30200, fy25: 30200, fy25Actual: 30200, fy26Dept: 30000, fy26Admin: 30200, change: 0, changePct: "0.00%" },
      { item: "Accountant", fy24: 44800, fy25: 45470, fy25Actual: 43770, fy26Dept: 45229, fy26Admin: 44249, change: 479, changePct: "1.10%" },
      { item: "Assessor", fy24: 83775, fy25: 95275, fy25Actual: 87275, fy26Dept: 91655, fy26Admin: 88775, change: 1500, changePct: "1.72%" },
      { item: "Treasurer Collector", fy24: 126674, fy25: 141098, fy25Actual: 128398, fy26Dept: 134772, fy26Admin: 131071, change: 2673, changePct: "2.08%" },
      { item: "Information Technology", fy24: 76000, fy25: 86000, fy25Actual: 84000, fy26Dept: 91000, fy26Admin: 91000, change: 7000, changePct: "8.33%" }
    ]
  };

  const departments = Object.keys(budgetData);

  const formatCurrency = (num) => {
    return new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(num);
  };

  return (
    <div className="min-h-screen bg-gray-50">
      <header className="bg-green-700 text-white p-4 shadow-md">
        <div className="container mx-auto flex justify-between items-center">
          <h1 className="text-2xl font-bold">Hubbardston Budget Proposal FY26</h1>
          <button onClick={() => setMobileMenuOpen(!mobileMenuOpen)} className="md:hidden">
            <Menu size={24} />
          </button>
        </div>
      </header>
      <div className="container mx-auto px-4 py-8">
        <div className="flex flex-col md:flex-row gap-6">
          <nav className={`md:w-64 ${mobileMenuOpen ? 'block' : 'hidden'} md:block`}>
            <div className="bg-white rounded-lg shadow-md p-4">
              <h2 className="text-lg font-semibold mb-4 text-green-700">Departments</h2>
              <ul className="space-y-2">
                {departments.map((dept) => (
                  <li key={dept}>
                    <button onClick={() => setActiveDept(dept)} className="w-full text-left px-4 py-2 rounded-md hover:bg-gray-100">
                      {dept}
                    </button>
                  </li>
                ))}
              </ul>
            </div>
          </nav>
          <main className="flex-1">
            <Card>
              <CardHeader>
                <CardTitle>{activeDept}</CardTitle>
              </CardHeader>
              <CardContent>
                <table className="w-full border">
                  <thead>
                    <tr>
                      <th className="text-left p-4">Item</th>
                      <th className="text-right p-4">FY24 Actual</th>
                      <th className="text-right p-4">FY25 Requested</th>
                      <th className="text-right p-4">FY25 Actual</th>
                      <th className="text-right p-4">FY26 Dept</th>
                      <th className="text-right p-4">FY26 Admin</th>
                      <th className="text-right p-4">Change ($)</th>
                      <th className="text-right p-4">Change (%)</th>
                    </tr>
                  </thead>
                  <tbody>
                    {budgetData[activeDept].map((item, index) => (
                      <tr key={index} className="border-b hover:bg-gray-50">
                        <td className="p-4">{item.item}</td>
                        <td className="text-right p-4">{formatCurrency(item.fy24)}</td>
                        <td className="text-right p-4">{formatCurrency(item.fy25)}</td>
                        <td className="text-right p-4">{formatCurrency(item.fy25Actual)}</td>
                        <td className="text-right p-4">{formatCurrency(item.fy26Dept)}</td>
                        <td className="text-right p-4">{formatCurrency(item.fy26Admin)}</td>
                        <td className="text-right p-4">{formatCurrency(item.change)}</td>
                        <td className="text-right p-4">{item.changePct}</td>
                      </tr>
                    ))}
                  </tbody>
                </table>
              </CardContent>
            </Card>
          </main>
        </div>
      </div>
    </div>
  );
};

export default BudgetProposal;
