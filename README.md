# Predicting Mental Health Risk from Social Media Usage Patterns

This was my 4th semester dissertation project for M.Sc Data Science at 
Dr. Bhimrao Ambedkar University, Agra. I wanted to explore something that 
felt relevant to my generation — how the way we use social media actually 
affects our mental health, and whether we can predict that risk using ML.

Supervised by Dr. Ranjana Gupta and Dr. Minakshi Pachauri, Department of 
Statistics, May 2026.

---

## What this project does

Takes survey responses about a person's social media habits and predicts 
whether they are at Low, Medium, or High mental health risk — using machine 
learning models trained on 447 real survey responses.

---

## Dataset

Source: Social Media and Mental Health Survey (Kaggle)  
Link: https://www.kaggle.com/datasets/souvikahmed071/social-media-and-mental-health

447 responses, 21 features covering demographics, behavioral patterns 
(purposeless usage, distraction, validation-seeking) and psychological 
indicators (anxiety, depression, sleep issues). Measured on a Likert scale 
of 1–5.

---

## My approach

**Data Preprocessing** — cleaned column names, handled missing values, 
converted Likert text responses (Never/Sometimes/Often etc.) to numeric, 
extracted usage hours from categorical ranges.

**Feature Engineering** — instead of using raw variables directly, I created 
4 composite scores that better capture underlying behavior:
- Addiction Score — avg of purposeless use, distraction, restlessness, validation-seeking
- Behavioral Score — avg of comparison and comparison feelings  
- Mental Score — avg of concentration difficulty, sleep issues, interest fluctuation
- Overall Score — combined average of all three above

**Target Variable** — built a Mental Health Index from depression, anxiety 
and sleep issues, then split into Low (≤2), Medium (2–3) and High (>3) risk.

**EDA** — 8 visualizations covering age distribution, gender vs risk, usage 
hours vs risk, addiction patterns, sleep issues, correlation heatmap, 
comparison behavior, and platform usage.

**Clustering** — applied both K-Means and Hierarchical clustering on usage 
and behavioral features. Both methods independently produced the same 3 
user groups, which matched the Low/Medium/High risk categories — that was 
a satisfying result to see.

**Model Building** — trained and compared 6 classification models with 
80/20 stratified split and 5-fold cross-validation.

---

## Results

| Model | Test Accuracy | CV Mean |
|-------|--------------|---------|
| Random Forest | 78.31% | 73.25% |
| Logistic Regression | 77.11% | 75.66% |
| XGBoost | 77.11% | 70.84% |
| Gradient Boosting | 75.90% | 72.77% |
| Decision Tree | 73.49% | 66.99% |
| SVM | 62.65% | 61.69% |

Random Forest was selected as the best model. The two engineered features — 
mental_score and overall_score — together contributed nearly 30% of total 
predictive power, which confirmed that feature engineering was worth doing.

---

## Live Prediction System

The final part of the project is a live prediction function that takes a 
person's behavioral inputs, runs the same feature engineering pipeline, 
and outputs a full Mental Health Risk Report — including risk level, 
probability breakdown across classes, addiction level, and personalized 
recommendations.

The HTML file in this repo is an interactive version of this predictor.

---

## Files in this repo

| File | Description |
|------|-------------|
| `4th_sem_project_.ipynb` | Full analysis notebook — preprocessing, EDA, clustering, models |
| `live prediction of mental health.html` | Interactive live prediction app |
| `4th sem final project .docx` | Complete project report |
| `mental_health_simple_ppt.pptx` | Presentation slides |
| `requirements.txt` | Python libraries needed |

---

## How to run

```bash
pip install -r requirements.txt
```
Then open `4th_sem_project_.ipynb` in Jupyter or Google Colab.  
Download the dataset from Kaggle and save it as `smmh.csv` in the same folder.

---

## Tools used

Python, Pandas, NumPy, Scikit-learn, XGBoost, Seaborn, Matplotlib, PCA, 
Google Colab

---

## What I learned

The most interesting finding was that behavioral patterns — how you use 
social media — matter more than demographic factors like gender in 
predicting mental health risk. Age and platform type had more influence 
than gender, which surprised me.

Also, SVM performed the worst here (62.65%) which makes sense because the 
risk categories don't have a clean separating boundary in feature space.
