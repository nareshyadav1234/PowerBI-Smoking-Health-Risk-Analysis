# 🫁 Smoking Health Risk Analysis - Power BI Dashboard

## 📌 Project Overview
This repository contains an interactive Power BI dashboard designed to analyze the impact of smoking on vital human organs. It provides a visual and data-driven approach to understanding how smoking habits correlate with health conditions, demographics, and overall patient risk.

## 📊 Key Features
* **Dynamic Organ Visuals:** Uses custom Image URLs to dynamically switch between **Healthy** and **Damaged** states of organs (Heart, Lungs, Liver, Kidney, Human Body) based on user selection.
* **Custom Navigation:** A clean, button-style vertical slicer for seamless organ selection.
* **Health KPIs:** Tracks Total Patients, Average Age, and Average BMI dynamically based on the filtered data.
* **Demographic Insights:** Includes Stacked Column Charts for "Smoking Status by Gender" and "Cholesterol & Hypertension Risk".
* **Trend Analysis:** Line charts showing "Smoking Duration & Daily Intake" across different age groups.

## 🛠️ Tools & Technologies Used
* **Power BI Desktop:** For data modeling, DAX calculations, and visualization.
* **Data Processing:** Excel/CSV for structuring the health dataset and managing public Image URLs for seamless rendering.

## 💡 Key DAX Measures Used
Here are some of the core DAX formulas used to calculate the dynamic KPIs:

**Age Group:**
Age Group = 
SWITCH(
    TRUE(),
    health_dataset[Age] <= 28, "18â€“28",
    health_dataset[Age] <= 38, "29â€“38",
    health_dataset[Age] <= 48, "39â€“48",
    health_dataset[Age] <= 58, "49â€“58",
    health_dataset[Age] <= 68, "59â€“68",
    "69+"
)


**Average Age:**
vs Avg Age = 
VAR _CurrentAge = AVERAGE(health_dataset[Age])
VAR _OverallAge = CALCULATE(AVERAGE(health_dataset[Age]), ALL(health_dataset))
VAR _Diff = _CurrentAge - _OverallAge

RETURN
SWITCH(
    TRUE(),
    _Diff > 0, UNICHAR(9650) & " " & FORMAT(_CurrentAge, "0.0"),
    _Diff < 0, UNICHAR(9660) & " " & FORMAT(_CurrentAge, "0.0"),
    FORMAT(_CurrentAge, "0.0")
)`

**Average BMI:**
vs Avg BMI = 
VAR _CurrentBMI = AVERAGE(health_dataset[BMI])
VAR _OverallBMI = CALCULATE(AVERAGE(health_dataset[BMI]), ALL(health_dataset))
VAR _Diff = _CurrentBMI - _OverallBMI

RETURN
SWITCH(
    TRUE(),
    _Diff > 0, UNICHAR(9650) & " " & FORMAT(_CurrentBMI, "0.0"),
    _Diff < 0, UNICHAR(9660) & " " & FORMAT(_CurrentBMI, "0.0"),
    FORMAT(_CurrentBMI, "0.0")
)
`
