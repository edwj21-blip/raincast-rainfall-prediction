# RainCast – ML-Powered Rainfall Prediction Web App

RainCast is a full-stack Flask application that predicts next-day rainfall for any location on Earth using historical weather data and machine learning classifiers (K-Nearest Neighbors, Random Forest, and Decision Tree).

---

## Features

- **Interactive Global Map**: Select any geographic coordinate using an interactive Leaflet map or search by city name.
- **Automated Weather Pipeline**: Fetches historical meteorological parameters (temperature, humidity, precipitation, wind speed, pressure, sunshine duration, and cloud cover) directly via Open-Meteo's API.
- **Multi-Model Machine Learning Comparison**:
  - **K-Nearest Neighbors (KNN)** ($k=5$)
  - **Random Forest Classifier** ($100$ estimators)
  - **Decision Tree Classifier** ($\max\text{ depth} = 6$)
  - Automatic evaluation across Accuracy, Precision, Recall, and F1 Score with automatic selection of the best-performing model.
- **Explainability**: Visualizes feature importances for tree-based models.
- **Robust Fallback**: Includes synthetic data simulation if the weather API is unreachable or offline.
- **User Authentication & History**: Secure session-based authentication with password hashing and persistent prediction history.

---

## Project Structure

```
Rainfall_Prediction/
├── .env.example            # Environment configuration template
├── .gitignore              # Git ignore rules for Python, DBs, and environments
├── README.md               # Project documentation
├── requirements.txt        # Python package dependencies
├── app.py                  # Main Flask application and database models
├── test_api.py             # Diagnostic script to test weather API reachability
├── ml/
│   ├── __init__.py
│   └── predictor.py        # ML data fetching, feature engineering, and model training
├── static/
│   └── css/
│       └── style.css       # Responsive UI styling
└── templates/
    ├── base.html           # Base layout with navbar
    ├── login.html          # Login view
    ├── register.html       # User registration view
    ├── dashboard.html      # Interactive map and prediction dashboard
    └── history.html        # Historical prediction logs
```

---

## Quickstart & Installation

### 1. Clone the repository
```bash
git clone https://github.com/edwj21-blip/Rainfall_Prediction.git
cd Rainfall_Prediction
```

### 2. Set up virtual environment
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS / Linux
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Configure environment variables (optional)
```bash
# Copy template to .env
cp .env.example .env
```
You can update `SECRET_KEY` in `.env` for production use.

### 5. Run the application
```bash
python app.py
```
Open [http://127.0.0.1:5000](http://127.0.0.1:5000) in your web browser.

---

## Machine Learning Pipeline

1. **Data Acquisition**: Queries up to 90 days of daily historical weather records from Open-Meteo for the selected coordinates.
2. **Feature Engineering**: Calculates daily averages, humidity aggregations, and labels next-day precipitation ($> 1\text{ mm}$ as rain).
3. **Model Training & Validation**: Scales numerical features via `StandardScaler`, splits training/testing sets, fits KNN, Random Forest, and Decision Tree models, and ranks them by F1-score.
4. **Prediction**: The highest-scoring model infers whether it will rain tomorrow along with prediction confidence.

---

## License

This project is open source and available under the [MIT License](LICENSE).
