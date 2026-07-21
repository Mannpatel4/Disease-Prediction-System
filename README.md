# Healthcare Disease Prediction System

---

## Quick Start (5 Steps)

```bash
# 1. Enter project folder
cd healthcare

# 2. Create virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Setup database
python manage.py migrate

# 5. Run server
python manage.py runserver
```

Open → **http://127.0.0.1:8000**

> **Note:** ML models are pre-trained and included. No retraining needed unless you change the dataset.

---

## Project Structure

```
healthcare/
├── manage.py
├── requirements.txt         
├── media/charts/                     
│
├── healthcare_project/               
│   ├── settings.py
│   └── urls.py
│
└── predictor/                 
    ├── views.py                      
    ├── models.py                     
    ├── urls.py
    ├── admin.py
    │
    ├── ml/
    │   ├── Training.csv             
    │   ├── Testing.csv        
    │   ├── train_models.py          
    │   ├── ml_engine.py              
    │   ├── naive_bayes.pkl  
    │   ├── decision_tree.pkl
    │   ├── random_forest.pkl
    │   ├── symptoms.pkl               
    │   ├── label_encoder.pkl        
    │   └── accuracy_summary.pkl       
    │
    └── templates/predictor/
        ├── base.html             
        ├── index.html                
        ├── dashboard.html        
        ├── history.html              
        └── auth.html           
```

---

## ML Models & Performance

| Model | Test Accuracy | CV Accuracy |
|---|---|---|
| **Naive Bayes** | 100.00% | 100.00% |      
| **Random Forest** | 100.00% | 100.00% |    
| **Decision Tree** | 58.54% | 58.01% |

**Note on accuracy:** This dataset represents idealized, noise-free symptom-to-disease mappings — each disease has only 5-10 fixed symptom patterns, repeated many times across the training samples (4,616 of 4,920 training rows are exact duplicates). This makes the classification problem near-perfectly separable, which is why Naive Bayes and Random Forest reach ~100% accuracy — this does not reflect real clinical diagnosis, where symptom overlap between diseases and patient-reported noise are much higher. Decision Tree's lower score (58%) likely comes from overfitting to specific duplicate patterns in a way that generalizes worse than the other two models on this data.

**Dataset:** 4,920 training samples · 41 test samples · 132 symptoms · 41 disease classes

**To retrain models** (if you modify the CSV):
```bash
python manage.py train_models
# or directly:
python predictor/ml/train_models.py
```

---

## Pages

| URL | Page |
|---|---|
| `/` | Disease predictor (symptom selection) |
| `/dashboard/` | Analytics — charts, model accuracy, stats |
| `/history/` | Your personal prediction history (login required) |
| `/login/` | Login |
| `/register/` | Register |
| `/admin/` | Django admin panel |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Django 4.2 |
| ML | scikit-learn (Naive Bayes, Decision Tree, Random Forest) |
| Data | pandas, numpy |
| Charts | matplotlib, seaborn |
| Database | SQLite |
| Frontend | HTML5, CSS3, Vanilla JS |
| Fonts | Space Mono + Outfit (Google Fonts) |

---

## Disclaimer

This system is for **educational and awareness purposes only**.
It is **not a medical diagnostic tool** and should not replace professional medical advice.
Always consult a qualified healthcare provider for diagnosis and treatment.

---