# personal-health-assistant-web-app
The Health Dashboard provides users with a visually engaging platform to track health metrics like steps, calories, sleep, and water intake. It offers recommendations and progress visualizations to help users maintain a healthy lifestyle.  Technologies Used:  React: For building the user interface. Recharts Lucide React Tailwind CSS

1. Imports
javascript
Copy
Edit
import React, { useState } from 'react';
import { Activity, Heart, Scale, Utensils, Moon, Droplets, Award } from 'lucide-react';
import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer } from 'recharts';
React: Used to build the user interface and manage state.
Lucide-react: A library for lightweight, customizable SVG icons (used to represent metrics like steps and heart rate).
Recharts: A library for creating responsive and interactive data visualizations (used for line charts).
2. Mock Data
javascript
Copy
Edit
const mockData = [
  { day: 'Mon', steps: 8000, calories: 2100, sleep: 7.5 },
  { day: 'Tue', steps: 10000, calories: 2300, sleep: 8 },
  { day: 'Wed', steps: 7500, calories: 2000, sleep: 6.5 },
  { day: 'Thu', steps: 9000, calories: 2200, sleep: 7 },
  { day: 'Fri', steps: 11000, calories: 2400, sleep: 8 },
];
Contains example health metrics (steps, calories, sleep) for each day of the week.
Used to populate the line chart and simulate weekly progress data.
3. Component State
javascript
Copy
Edit
const [healthData, setHealthData] = useState({
  steps: '',
  heartRate: '',
  weight: '',
  calories: '',
  sleep: '',
  water: ''
});
const [recommendations, setRecommendations] = useState([]);
healthData: Stores the user's input for various health metrics.
recommendations: Stores health suggestions that are dynamically updated when the "Analyze Health" button is clicked.
4. Handle Submit (Generate Recommendations)
javascript
Copy
Edit
const handleSubmit = () => {
  setRecommendations([
    "Try to increase your daily steps to 10,000",
    "Consider drinking more water throughout the day",
    "Aim for 7-8 hours of sleep consistently",
    "Your heart rate is within normal range"
  ]);
};
When the "Analyze Health" button is clicked:
Mock recommendations are generated and displayed in the Recommendations Section.
5. MetricCard Component
javascript
Copy
Edit
const MetricCard = ({ icon: Icon, title, value, unit, color }) => (
  <div className="bg-white p-6 rounded-xl shadow-md hover:shadow-lg transition-all">
    <div className={`w-12 h-12 rounded-full ${color} flex items-center justify-center mb-4`}>
      <Icon className="w-6 h-6 text-white" />
    </div>
    <h3 className="text-gray-600 text-sm mb-2">{title}</h3>
    <div className="flex items-baseline">
      <span className="text-2xl font-bold text-gray-800">{value}</span>
      <span className="ml-2 text-gray-500">{unit}</span>
    </div>
  </div>
);
Reusable Component: Displays health metrics (e.g., steps, heart rate).
Props:
icon: The Lucide icon to display.
title, value, and unit: Text content for the card.
color: Background color of the icon.
6. User Interface Layout
Header
javascript
Copy
Edit
<div className="flex items-center justify-between mb-8">
  <h1 className="text-3xl font-bold text-gray-800">Health Assistant</h1>
  <button 
    onClick={handleSubmit}
    className="bg-blue-500 text-white px-6 py-2 rounded-lg hover:bg-blue-600 transition-colors"
  >
    Analyze Health
  </button>
</div>
Displays the title and the "Analyze Health" button.
The button triggers the handleSubmit function to generate recommendations.
Metric Cards
javascript
Copy
Edit
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
  <MetricCard icon={Activity} title="Daily Steps" value="8,439" unit="steps" color="bg-blue-500" />
  <MetricCard icon={Heart} title="Heart Rate" value="72" unit="bpm" color="bg-red-500" />
  <MetricCard icon={Moon} title="Sleep" value="7.5" unit="hours" color="bg-indigo-500" />
  <MetricCard icon={Droplets} title="Water Intake" value="6" unit="glasses" color="bg-cyan-500" />
</div>
A grid of 4 MetricCards shows metrics like steps, heart rate, sleep, and water intake.
Line Chart
javascript
Copy
Edit
<ResponsiveContainer width="100%" height="100%">
  <LineChart data={mockData}>
    <CartesianGrid strokeDasharray="3 3" />
    <XAxis dataKey="day" />
    <YAxis />
    <Tooltip />
    <Line type="monotone" dataKey="steps" stroke="#3B82F6" name="Steps" />
    <Line type="monotone" dataKey="calories" stroke="#EF4444" name="Calories" />
    <Line type="monotone" dataKey="sleep" stroke="#6366F1" name="Sleep" />
  </LineChart>
</ResponsiveContainer>
Displays Weekly Data:
Metrics: Steps (blue), Calories (red), and Sleep (purple).
ResponsiveContainer: Ensures the chart adapts to screen size.
Recommendations Section
javascript
Copy
Edit
<div className="bg-white p-6 rounded-xl shadow-md">
  <h2 className="text-xl font-semibold mb-4">Recommendations</h2>
  <div className="space-y-4">
    {recommendations.map((rec, index) => (
      <div key={index} className="flex items-start">
        <Award className="w-5 h-5 text-blue-500 mr-2 mt-1" />
        <p className="text-gray-700">{rec}</p>
      </div>
    ))}
    {recommendations.length === 0 && (
      <p className="text-gray-500">Click "Analyze Health" to get personalized recommendations</p>
    )}
  </div>
</div>
Dynamically shows recommendations.
Displays placeholder text if no recommendations exist.
Update Metrics Form
javascript
Copy
Edit
<div className="grid grid-cols-2 gap-4">
  <input type="number" placeholder="Steps" className="p-2 border rounded-lg" />
  <input type="number" placeholder="Heart Rate" className="p-2 border rounded-lg" />
  <input type="number" placeholder="Sleep Hours" className="p-2 border rounded-lg" />
  <input type="number" placeholder="Water (glasses)" className="p-2 border rounded-lg" />
</div>
Input fields for users to manually update health metrics like steps and sleep.
7. Goals Progress
javascript
Copy
Edit
<div className="relative pt-1">
  <div className="flex mb-2 items-center justify-between">
    <span className="text-xs font-semibold text-blue-600 bg-blue-200">Steps Goal</span>
    <span className="text-xs font-semibold text-blue-600">84%</span>
  </div>
  <div className="overflow-hidden h-2 mb-4 text-xs flex rounded bg-blue-200">
    <div style={{ width: "84%" }} className="bg-blue-500"></div>
  </div>
</div>
Displays a progress bar for achieving goals (e.g., "Steps Goal").
