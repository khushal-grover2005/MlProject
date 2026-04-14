# Student Performance Prediction - End-to-End ML Project

A comprehensive machine learning project that predicts student mathematics performance based on demographic and academic features. This project demonstrates the complete ML lifecycle: data ingestion, exploratory analysis, feature engineering, model training, evaluation, and production deployment via a Flask web application.

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Dataset](#dataset)
- [Project Architecture](#project-architecture)
- [Installation & Setup](#installation--setup)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Models](#models)
- [Results](#results)
- [Technologies Used](#technologies-used)
- [Configuration](#configuration)
- [Contributing](#contributing)
- [Author](#author)

---

## 🎯 Project Overview

This project builds a regression model to predict a student's mathematics score based on several input features including:
- **Demographic Information**: Gender, Race/Ethnicity, Parental Education Level
- **Academic Background**: Lunch Type, Test Preparation Course Status
- **Prior Academic Performance**: Reading Score, Writing Score

The project implements industry best practices including:
- Modular code structure with separation of concerns
- Custom exception handling and logging
- Multiple ML model comparison and selection
- Cross-validation and hyperparameter tuning
- Automated data preprocessing pipeline
- RESTful API deployment via Flask

---

## ✨ Features

✅ **End-to-End Pipeline**: Data ingestion → Transformation → Model Training → Prediction  
✅ **Multiple Models**: Random Forest, XGBoost, CatBoost, Gradient Boosting, Linear Regression, Decision Trees, AdaBoost  
✅ **Automated Preprocessing**: Categorical encoding, feature scaling, and train-test splitting  
✅ **Model Evaluation**: R² score metrics and performance comparison  
✅ **Production Ready**: Flask web application for real-time predictions  
✅ **Logging & Exception Handling**: Custom error handling and detailed logging  
✅ **Modular Design**: Clean separation of concerns for maintainability  

---

## 📊 Dataset

### Input Features (7 total)
| Feature | Type | Description |
|---------|------|-------------|
| **gender** | Categorical | Male / Female |
| **race_ethnicity** | Categorical | Group A-E |
| **parental_level_of_education** | Categorical | High school, Some college, Bachelor's, Master's, etc. |
| **lunch** | Categorical | Standard / Free or reduced |
| **test_preparation_course** | Categorical | Completed / None |
| **reading_score** | Numerical | Score from 0-100 |
| **writing_score** | Numerical | Score from 0-100 |

### Target Variable
| Variable | Range |
|----------|-------|
| **math_score** | 0-100 |

---

## 🏗️ Project Architecture

```
Data Ingestion
    ↓
Data Transformation (Encoding, Scaling)
    ↓
Model Training (Multiple Models)
    ↓
Model Evaluation & Selection
    ↓
Prediction Pipeline
    ↓
Flask Web Application
```

### Data Flow
1. **Training Phase**: Raw data → Preprocessing → Model training
2. **Prediction Phase**: User input → Preprocessing → Model prediction → Results

---

## 🚀 Installation & Setup

### Prerequisites
- Python 3.8 or higher
- Anaconda/Miniconda (recommended)
- Git

### Step 1: Clone the Repository
```bash
git clone <repository-url>
cd "ML projects"
```

### Step 2: Create a Conda Environment
```bash
conda create -n ML python=3.8
conda activate ML
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

Or install the package in development mode:
```bash
pip install -e .
```

---

## 💻 Usage

### Training a Model
Run the training pipeline to train and evaluate models:

```python
from src.pipeline.trainpipeline import TrainPipeline

pipeline = TrainPipeline()
pipeline.run()
```

### Running the Flask Application
Start the web server:

```bash
python app.py
```

The application will be available at `http://localhost:5000`

**Home Page**: `http://localhost:5000/`  
**Prediction Endpoint**: `http://localhost:5000/predictdata` (POST)

### Making Predictions via Web Interface
1. Open the application in your browser
2. Fill in the form with student information:
   - Select gender, race/ethnicity, parental education
   - Choose lunch type and test prep status
   - Enter reading and writing scores
3. Click "Predict" to get the predicted math score

### Making Predictions Programmatically
```python
from src.pipeline.predictpipeline import CustomData, PredictPipeline

# Prepare data
data = CustomData(
    gender='male',
    race_ethnicity='group B',
    parental_level_of_education="bachelor's degree",
    lunch='standard',
    test_preparation_course='completed',
    reading_score=75,
    writing_score=78
)

# Make prediction
pred_pipeline = PredictPipeline()
prediction = pred_pipeline.predict(data.get_data_as_data_frame())
print(f"Predicted Math Score: {prediction[0]}")
```

---

## 📁 Project Structure

```
ML projects/
├── app.py                          # Flask web application
├── setup.py                        # Package setup configuration
├── requirements.txt                # Project dependencies
├── README.md                       # Project documentation
│
├── artifacts/                      # Trained models and preprocessors
│   ├── model.pkl                   # Trained ML model
│   ├── preprocessor.pkl            # Data preprocessor pipeline
│   ├── train.csv                   # Training dataset
│   ├── test.csv                    # Test dataset
│   └── data.csv                    # Raw dataset
│
├── src/                            # Source code
│   ├── __init__.py
│   ├── exception.py                # Custom exception handling
│   ├── logger.py                   # Logging configuration
│   ├── utils.py                    # Utility functions
│   │
│   ├── components/                 # ML pipeline components
│   │   ├── __init__.py
│   │   ├── dataingestion.py        # Data loading and validation
│   │   ├── datatransformation.py   # Feature engineering & preprocessing
│   │   └── modeltrainer.py         # Model training and evaluation
│   │
│   ├── pipeline/                   # High-level pipelines
│   │   ├── trainpipeline.py        # Training pipeline orchestration
│   │   └── predictpipeline.py      # Prediction pipeline
│   │
│   └── logs/                       # Log files
│
├── notebook/                       # Jupyter notebooks for exploration
│   ├── EDA.ipynb                   # Exploratory Data Analysis
│   ├── MT.ipynb                    # Model Training experiments
│   └── data/                       # Notebook data
│
├── templates/                      # HTML templates for Flask app
│   └── index.html                  # Web interface
│
└── logs/                           # Application logs
```

---

## 🤖 Models

The project trains and compares multiple regression models:

| Model | Type | Library |
|-------|------|---------|
| **Random Forest** | Ensemble | scikit-learn |
| **Decision Tree** | Tree-based | scikit-learn |
| **Gradient Boosting** | Boosting | scikit-learn |
| **Linear Regression** | Linear | scikit-learn |
| **XGBoost** | Gradient Boosting | xgboost |
| **CatBoost** | Gradient Boosting | catboost |
| **AdaBoost** | Adaptive Boosting | scikit-learn |

**Model Selection**: The best model is selected based on R² score on the test set.

---

## 📈 Results

After training, the model performance is evaluated using:

- **R² Score**: Coefficient of determination (0-1, higher is better)
- **Mean Squared Error**: Average squared prediction error
- **Model Comparison**: Identifies the best performing model

Results are logged in:
- `catboost_info/learn_error.tsv` - Training error metrics
- `logs/` - Application logs

---

## 🛠️ Technologies Used

### Core Libraries
- **pandas** (1.x): Data manipulation and analysis
- **numpy**: Numerical computing
- **scikit-learn**: Machine learning algorithms and preprocessing
- **xgboost**: Gradient boosting framework
- **catboost**: Categorical boosting
- **matplotlib & seaborn**: Data visualization

### Web Framework
- **Flask**: Lightweight web framework
- **gunicorn**: WSGI HTTP server (production)

### Utilities
- **dill**: Enhanced serialization for model persistence

---

## ⚙️ Configuration

### Model Trainer Configuration
Located in `src/components/modeltrainer.py`:
```python
@dataclass
class ModelTrainerConfig:
    trained_model_file_path = 'artifacts/model.pkl'
```

### Data Ingestion Configuration
Located in `src/components/dataingestion.py`:
- Input data path
- Train/test split ratio
- Test size percentage

### Flask Configuration
Located in `app.py`:
- Host: `0.0.0.0` (accessible from any interface)
- Default port: `5000`
- Debug mode can be enabled for development

---

## 📝 Logging & Error Handling

### Logger
Custom logging module in `src/logger.py` logs:
- Training progress
- Model evaluation metrics
- Data transformation steps
- Prediction requests

### Exception Handling
Custom exception handling in `src/exception.py` provides:
- Detailed error messages with file and line numbers
- Error context and traceback information
- Graceful error recovery

---

## 🔄 Development Workflow

### For Data Scientists
1. Use `notebook/EDA.ipynb` for exploratory data analysis
2. Use `notebook/MT.ipynb` for model experimentation
3. Once satisfied, integrate changes into `src/components/`

### For ML Engineers
1. Update components in `src/components/`
2. Test via the training pipeline
3. Deploy via the Flask app

### For Deployment
1. Run training to generate artifacts
2. Deploy Flask app using gunicorn:
```bash
gunicorn --workers 4 --bind 0.0.0.0:5000 app:app
```

---

## 📦 Package Installation

This project can be installed as a package:

```bash
pip install -e .
```

Then import components in other projects:
```python
from src.pipeline.predictpipeline import PredictPipeline, CustomData
from src.exception import CustomException
```

---

## 🤝 Contributing

Contributions are welcome! Please:
1. Create a new branch for your feature
2. Add logs for important operations
3. Test your changes thoroughly
4. Submit a pull request with a clear description

---

## 📄 License

This project is open source and available under the MIT License.

---

## 👤 Author

**Khushal Grover**  
📧 khushalgrover64@gmail.com

---

## 🎓 Learning Resources

This project demonstrates:
- ML pipeline architecture
- Data preprocessing best practices
- Model comparison and selection
- Production deployment with Flask
- Logging and error handling
- Modular code design

Ideal for learning or portfolio building!

---

## ❓ FAQ

**Q: How do I train a new model?**  
A: Run the training pipeline script. It will train all models and save the best one.

**Q: Can I use this in production?**  
A: Yes! Use gunicorn to serve the Flask app: `gunicorn --workers 4 --bind 0.0.0.0:5000 app:app`

**Q: How do I improve model performance?**  
A: Explore notebooks, try feature engineering, adjust hyperparameters, or add new data.

**Q: What if the model is not accurate?**  
A: Check `catboost_info/` logs, review data quality, try different models, or add more training data.