# 🏥 Hospital Readmission Risk Analysis

---

## 1. Project Overview
This project investigates hospital readmission risk among diabetic patients.  
The workflow includes **data cleaning**, **feature engineering**, **exploratory data analysis (EDA)**, and **visualization** to uncover patterns that drive readmissions.

---

## 2. Business Problem
Hospital readmissions within 30 days are costly and impact patient outcomes.  
The goal is to identify **key drivers of readmission** and provide actionable insights to reduce unnecessary readmissions, improve patient care, and optimize hospital resources.

---

## 3. Dataset Information
- **Source**: Diabetic patient hospital records  
- **Size**: ~101,766 rows × 50 columns  
- **Features**:
  - Patient demographics (age, gender, race)
  - Admission details (type, source, length of stay)
  - Diagnosis codes
  - Medications and lab results
  - Target variable: `readmitted` (within 30 days)

---

## 4. Data Cleaning Process
- Removed or imputed missing values.
- Standardized categorical labels (`unknow` → `unknown`, `others` → `Other`).
- Collapsed rare categories in `race` and `medical_specialty`.
- Corrected inconsistencies in diagnosis codes.
- Encoded target variable `readmitted`.

---

## 5. Feature Engineering
- Grouped diagnosis codes into broader categories.
- Created age groups for demographic analysis.
- Aggregated medication counts.
- Derived hospital stay length categories.

---

## 6. Exploratory Data Analysis
- Distribution analysis of demographics and admission types.
- Correlation matrix to identify feature relationships.
- Comparative analysis of readmitted vs non-readmitted patients.

---

## 7. Visualizations
- 📊 **scatter_plot** →## Medications vs Stay Length##
- sns.scatterplot(x='meds_given_count', y='time_in_hospital', hue='readmitted', data=df)
- <img width="782" height="527" alt="image" src="https://github.com/user-attachments/assets/40900b21-db27-4871-b0f1-754d72aacd28" />
  ###Summary: Medication count and hospital stay length show moderate correlation with readmission.
  #Age group also aligns with higher risk, confirming demographic influence.
---------------------------------------------------------------------------------------------------------------------
- 📊 **Horizontal Bar Chart** → ## Top 10 diagnoses in readmitted patients##
top_diag = (df[df['readmitted']==1]['diag_1_category']
            .value_counts()
            .head(10))

sns.barplot(y=top_diag.index, x=top_diag.values, orient='h')
plt.title("Top 10 Diagnoses in Readmitted Patients")
plt.xlabel("Count")
plt.ylabel("Diagnosis Category")
plt.savefig("chart8_dashboard.png", dpi=150, bbox_inches="tight")
plt.show()
<img width="876" height="557" alt="image" src="https://github.com/user-attachments/assets/d90d8c72-6191-47ed-9076-844214303648" />

    -------------------------------------------------------------------------------------------------------------------------------------------------------
- 📊 **Heatmap** → ##Correlation matrix of all features##
diag_readmit = df.groupby('diag_1_category')['readmitted'].mean() * 100
sns.barplot(y=diag_readmit.index, x=diag_readmit.values, orient='h')
plt.title("Readmission Rate by Diagnosis Category")
plt.xlabel("Readmission %")
plt.ylabel("Diagnosis Category")
plt.savefig("chart5_dashboard.png", dpi=150, bbox_inches="tight")
plt.show()
<img width="862" height="550" alt="image" src="https://github.com/user-attachments/assets/e4436ead-4b34-48df-8d7b-2648f79fb5e6" />
 Patients with circulatory and endocrine conditions (including diabetes) show the highest readmission rates, reflecting the chronic nature of these illnesses. 
    Respiratory and digestive diagnoses also contribute significantly, while injury and musculoskeletal cases have comparatively lower readmission percentages.

-  
- 📊 **violinPlot** → ##Hospital stay days vs readmission status##
  sns.violinplot(x='readmitted', y='time_in_hospital', data=df)
plt.title("Hospital Stay Length vs Readmission")
plt.xlabel("Readmitted within 30 days (0=No, 1=Yes)")
plt.ylabel("Time in Hospital (days)")
plt.savefig("chart6_dashboard.png", dpi=150, bbox_inches="tight")
plt.show()
<img width="767" height="552" alt="image" src="https://github.com/user-attachments/assets/6cfeba2f-92a8-4378-937e-affac6cc76d8" />

  Summary: Patients with shorter stays are more likely to be readmitted, 
   #suggesting that early discharge may contribute to higher risk.
 -------------------------------------------------------------------------------------------------------

-  
- 📊 **Hist Chart** → ##Readmission rate by gender##
- "sns.histplot(data=df, x='gender', hue='readmitted', multiple='stack', stat='count')
plt.title("Gender vs Readmission")
plt.savefig("chart4_dashboard.png", dpi=150, bbox_inches="tight")
plt.show()
<img width="883" height="678" alt="chart3_dashboard" src="https://github.com/user-attachments/assets/e23ca178-cd9f-473b-bdd1-84c0765046db" />

 Readmission Rate by Gender
   ##Summary: Readmission rates are similar across genders, with only minor differences.
        Gender appears less predictive compared to age or diagnosis.
        
- ------------------------------------------------------------------------------------------------------------------------------------------------------
- 📊 **pie Chart** → ## Readmission rate by age group ##
- - - "age_readmit = df.groupby('age_group')['readmitted'].mean() * 100
plt.pie(age_readmit.values, labels=age_readmit.index, autopct='%1.1f%%')
plt.title("Readmission Rate by Age Group")
plt.savefig("chart3_dashboard.png", dpi=150, bbox_inches="tight")
plt.show()"

 #this pie chat showing how readmission rate (%) hapen by age group
 ###Summary: The majority of patients are not readmitted, but a significant minority return within 30 days.
            # This highlights the importance of targeted interventions.
plt.savefig("chart2_dashboard.png", dpi=150, bbox_inches="tight")
- <img width="562" height="502" alt="Screenshot 2026-06-05 005845" src="https://github.com/user-attachments/assets/fd0c3f69-e15d-4302-82b1-90f25063293b" />


---

## 9. Key Findings
- Shorter hospital stays are linked to higher readmission risk.
- Certain diagnoses (e.g., circulatory and respiratory diseases) show elevated readmission rates.
- Polypharmacy (multiple medications) correlates with increased readmission.
- Demographic differences exist (age and gender influence risk).

---

## 10. Recommendations
- Strengthen discharge protocols for short-stay patients.
- Implement targeted follow-up care for high-risk diagnoses.
- Review medication management for patients with multiple prescriptions.
- Develop demographic-specific intervention strategies.

---

## 11. Project Structure
<img width="677" height="227" alt="image" src="https://github.com/user-attachments/assets/cc2c2982-69f7-4bd7-ba79-866de3d8a4ce" />


---

## 12. Future Improvements
- Build predictive models (Logistic Regression, Random Forest, XGBoost).
- Use advanced interpretability tools (SHAP, LIME).
- Incorporate external datasets (socioeconomic factors, comorbidities).
- Deploy a dashboard for real-time monitoring of readmission risk.

---

## 🛠️ Libraries Used
- **Data Handling**: `pandas`, `numpy`
- **Visualization**: `matplotlib`, `seaborn`
- **Model Preparation**: `scikit-learn`

---

## 📌 Usage
1. Open `readmission_analysis.ipynb` in Jupyter Notebook.
2. Run cells sequentially to reproduce cleaning and visualization.
3. Use `diabetic_cleaned.csv` for modeling experiments.
4. Review charts (`chart1_dashboard.png`, etc.) for visual insights.
5. Refer to `Hospital_Readmission_Report.xlsx` for consolidated results.

