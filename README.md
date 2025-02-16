import React, { useState } from 'react';
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card';
import { Menu } from 'lucide-react';

const BudgetProposal = () => {
  const [activeDept, setActiveDept] = useState('GENERAL GOVERNMENT');
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);

  // Full budget data
  const budgetData = {
    'GENERAL GOVERNMENT': [
      { item: "Moderator", fy25: 100, fy26: 100, change: 0 },
      { item: "Select Board", fy25: 76473, fy26: 86648, change: 13.31 },
      { item: "Town Admin", fy25: 120400, fy26: 122766, change: 2.82 },
      { item: "Finance Committee", fy25: 30200, fy26: 30200, change: 0 },
      { item: "Accountant", fy25: 45470, fy26: 44249, change: 1.10 },
      { item: "Assessor", fy25: 95275, fy26: 88775, change: 1.72 },
      { item: "Treasurer Collector", fy25: 141098, fy26: 131071, change: 2.08 },
      { item: "Information Technology", fy25: 86000, fy26: 91000, change: 8.33 },
      { item: "Town Clerk", fy25: 75450, fy26: 74170, change: 4.54 },
      { item: "Building & Maintenance", fy25: 47640, fy26: 62361, change: 30.35 }
    ],
    'PUBLIC SAFETY': [
      { item: "Police", fy25: 737565, fy26: 709576, change: 1.73 },
      { item: "Fire", fy25: 613243, fy26: 571748, change: -2.79 },
      { item: "Land Use", fy25: 94214, fy26: 117398, change: -39.24 },
      { item: "Emergency Management", fy25: 2489, fy26: 2483, change: 0 },
      { item: "Animal Control", fy25: 18944, fy26: 20500, change: 0 },
      { item: "Tree Warden", fy25: 1900, fy26: 1900, change: 0 },
      { item: "Dispatch", fy25: 142410, fy26: 158238, change: 6.20 }
    ],
    'PUBLIC WORKS': [
      { item: "DPW Director", fy25: 89269, fy26: 94402, change: 5.75 },
      { item: "DPW Wages", fy25: 285975, fy26: 285975, change: 2.00 },
      { item: "Snow and Ice", fy25: 237130, fy26: 233300, change: -0.90 },
      { item: "Street Lights", fy25: 6000, fy26: 6000, change: 0 },
      { item: "Cemetery", fy25: 1300, fy26: 1300, change: 0 }
    ],
    'SCHOOL': [
      { item: "Quabbin Regional", fy25: 6343869, fy26: 6880292, change: 8.00 },
      { item: "QRSD Debt", fy25: 56318, fy26: 57444, change: 2.00 },
      { item: "Montachusett Technical", fy25: 357138, fy26: 357138, change: 0 }
    ],
    'HUMAN SERVICES': [
      { item: "Senior Center", fy25: 22204, fy26: 25550, change: 18.27 },
      { item: "Veterans", fy25: 16350, fy26: 9850, change: 0 }
    ],
    'CULTURE & RECREATION': [
      { item: "Library", fy25: 89639, fy26: 91290, change: 1.95 },
      { item: "Recreation", fy25: 2500, fy26: 2500, change: 0 },
      { item: "Agricultural Commission", fy25: 300, fy26: 300, change: 0 },
      { item: "Historical Commission", fy25: 200, fy26: 200, change: 0 }
    ],
    'DEBT': [
      { item: "Short-Term Interest", fy25: 14485, fy26: 20000, change: 38.07 },
      { item: "Principal on Short-Term Debt", fy25: 50000, fy26: 25000, change: -50.00 },
      { item: "School Roof", fy25: 82377, fy26: 101862, change: 23.65 }
    ],
    'LIABILITIES & ASSESSMENTS': [
      { item: "Cherry Sheet Assessment", fy25: 10151, fy26: 12280, change: 0 },
      { item: "Worcester Regional Retirement", fy25: 431576, fy26: 480823, change: 7.33 },
      { item: "Health Insurance", fy25: 219761, fy26: 241737, change: 10.00 },
      { item: "Medicare", fy25: 33360, fy26: 33360, change: 0 },
      { item: "Liability Insurance", fy25: 156175, fy26: 163984, change: 5.00 },
      { item: "Offsets and Overlay", fy25: 68627, fy26: 72765, change: 0 }
    ]
  };

  const departments = Object.keys(budgetData);

  const formatCurrency = (num) => {
    if (!num) return '$0';
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD'
    }).format(num);
  };

  const getDepartmentTotal = (dept) => {
    return budgetData[dept].reduce((acc, item) => acc + item.fy26, 0);
  };

  return (
    <div className="min-h-screen bg-gray-50">
      {/* Header */}
      <header className="bg-green-700 text-white p-4 shadow-md">
        <div className="container mx-auto flex justify-between items-center">
          <h1 className="text-2xl font-bold">Hubbardston Budget Proposal FY26</h1>
          <button 
            onClick={() => setMobileMenuOpen(!mobileMenuOpen)}
            className="md:hidden"
          >
            <Menu size={24} />
          </button>
        </div>
      </header>

      <div className="container mx-auto px-4 py-8">
        <div className="flex flex-col md:flex-row gap-6">
          {/* Navigation Sidebar */}
          <nav className={`md:w-64 ${mobileMenuOpen ? 'block' : 'hidden'} md:block`}>
            <div className="bg-white rounded-lg shadow-md p-4">
              <h2 className="text-lg font-semibold mb-4 text-green-700">Departments</h2>
              <ul className="space-y-2">
                {departments.map((dept) => (
                  <li key={dept}>
                    <button
                      onClick={() => setActiveDept(dept)}
                      className={`w-full text-left px-4 py-2 rounded-md transition-colors ${
                        activeDept === dept
                          ? 'bg-green-100 text-green-700 font-medium'
                          : 'hover:bg-gray-100'
                      }`}
                    >
                      <div className="flex justify-between items-center">
                        <span>{dept}</span>
                        <span className="text-sm text-gray-600">
                          {formatCurrency(getDepartmentTotal(dept))}
                        </span>
                      </div>
                    </button>
                  </li>
                ))}
              </ul>
            </div>
          </nav>

          {/* Main Content */}
          <main className="flex-1">
            <Card>
              <CardHeader className="flex flex-row justify-between items-center">
                <CardTitle className="text-xl text-green-700">{activeDept}</CardTitle>
                <div className="text-right">
                  <div className="text-sm text-gray-600">FY26 Total</div>
                  <div className="text-lg font-semibold">
                    {formatCurrency(getDepartmentTotal(activeDept))}
                  </div>
                </div>
              </CardHeader>
              <CardContent>
                <div className="overflow-x-auto">
                  <table className="w-full">
                    <thead>
                      <tr className="border-b">
                        <th className="text-left p-4">Item</th>
                        <th className="text-right p-4">FY25 Requested</th>
                        <th className="text-right p-4">FY26 Admin</th>
                        <th className="text-right p-4">Change (%)</th>
                      </tr>
                    </thead>
                    <tbody>
                      {budgetData[activeDept].map((item, index) => (
                        <tr key={index} className="border-b hover:bg-gray-50">
                          <td className="p-4">{item.item}</td>
                          <td className="text-right p-4">{formatCurrency(item.fy25)}</td>
                          <td className="text-right p-4">{formatCurrency(item.fy26)}</td>
                          <td className="text-right p-4">
                            <span className={item.change > 0 ? 'text-red-600' : 'text-green-600'}>
                              {item.change > 0 ? '+' : ''}{item.change}%
                            </span>
                          </td>
                        </tr>
                      ))}
                    </tbody>
                  </table>
                </div>
              </CardContent>
            </Card>
          </main>
        </div>
      </div>
    </div>
  );
};

export default BudgetProposal;
