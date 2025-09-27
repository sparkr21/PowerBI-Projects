# Students Academic Stress Dashboard – Requirement Document

## 1. Overview  
The **Students Academic Stress Dashboard** supports EduRise Foundation's mission to monitor and alleviate academic stress among students. It provides insights into key stress drivers—peer pressure, home pressure, study environment, intoxication, and academic stage—enabling program managers to prioritize interventions.

---

## 2. Report Objectives  
- **Quantify overall student stress** by aggregating stress index scores and sub-dimensions.  
- **Identify primary stress drivers** (peer pressure, pressure from home, study environment, intoxication).  
- **Segment stress by academic stage** (high school, undergraduate, post-graduate).  
- **Track population coverage**, displaying total student count.

---

## 3. Data Sources  
- Student survey responses (Excel/CSV) containing:  
  - `StudentID` (unique identifier)  
  - `PeerPressureScore` (1–5)  
  - `HomePressureScore` (1–5)  
  - `StudyEnvironment` (categorical: Peaceful, Noisy, Disrupted)  
  - `AcademicStressIndex` (1–5 overall score)  
  - `AcademicStage` (categorical: high school, undergraduate, post-graduate)  
  - `Intoxication` (Yes/No/Prefer not to say)  
- Data refresh schedule: **Daily at 2 AM**.

---

## 4. Metrics & Calculations  
### 4.1 Key Measures  
- **Count of Students**: `COUNTROWS(StudentSurvey)`  
- **Average Academic Stress Index**: `AVERAGE(StudentSurvey[AcademicStressIndex])`  
- **Distribution of Peer Pressure**: percentage per score value  
- **Distribution of Home Pressure**: percentage per score value  
- **Study Environment Breakdown**: percentage per category  
- **Intoxication Breakdown**: percentage per response  

### 4.2 DAX Examples  
```dax
CountOfStudents = COUNTROWS(StudentSurvey)
AvgStressIndex = AVERAGE(StudentSurvey[AcademicStressIndex])
PeerPressureDistribution = 
    DIVIDE(
        COUNTROWS(StudentSurvey),
        CALCULATE(COUNTROWS(StudentSurvey), ALL(StudentSurvey[PeerPressureScore]))
    )
```

---

## 5. Visualizations  
| Visual                    | Type             | Data Fields                                   | Interactions                  |
|---------------------------|------------------|-----------------------------------------------|-------------------------------|
| Peer Pressure             | Donut Chart      | Value: Count of Students <br> Legend: PeerPressureScore | Hover to display percentage  |
| Stress Level              | Clustered Column| Axis: AcademicStressIndex <br> Value: Count of Students | Select bar to cross-filter   |
| Pressure From Home        | Clustered Column| Axis: HomePressureScore <br> Value: Count of Students | Select bar to filter visuals |
| Study Environment         | Pie Chart        | Legend: StudyEnvironment <br> Value: Count of Students | Hover for category detail    |
| Academic Stage            | Clustered Column| Axis: AcademicStage <br> Value: Count of Students | Click to filter other charts |
| Intoxication              | Pie Chart        | Legend: Intoxication <br> Value: Count of Students | Hover shows counts & %       |

---

## 6. Layout & Formatting  
- **Theme**: EduRise Foundation branded colors (blue for primary).  
- **Font**: Segoe UI, size 12 for labels, 14 for titles.  
- **Header**: Logo at top-left, report title centered, total student count at top-right.  
- **Grid**: Two columns, three rows of visuals.  

---

## 7. User Requirements  
- **Performance**: Must load under 5 seconds for up to 10,000 records.  
- **Accessibility**: Tooltips for each visual; descriptive alt-text for screen readers.  
- **Export**: PDF and PowerPoint export enabled.  
- **Mobile**: Responsive layout with single-column stacking.  

---

## 8. Security & Sharing  
- **Permissions**:  
  - Data analysts: Edit access  
  - Program managers: View access  
- **Workspace**: Published to EduRise Foundation "Student Insights" workspace.  
- **Row-Level Security**: Filter by region for local coordinators.

---

## 9. Maintenance  
- **Data Source Updates**: Validate incoming survey files weekly.  
- **Dashboard Review**: Quarterly stakeholder feedback and update visuals or metrics as needed.  

---

*End of Requirement Document*