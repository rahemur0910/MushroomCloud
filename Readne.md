# 🍄 Mushroom Classification App (Cloud + Django + ML)

This project combines **Django (web framework)** with a **Machine Learning model (PCA + RandomForest)** to classify mushrooms as edible or poisonous. The app is structured for deployment to cloud platforms (Heroku/Render/etc.) and includes all dependencies, saved models, and a Jupyter notebook.

---

## 📂 Project Structure

```
MUSHROOMCLOUD/
│
├── code/
│   ├── .ipynb_checkpoints/     # Jupyter autosaves
│   ├── .venv/                  # Virtual environment
│   ├── jupyter-env/            # Another env folder
│   ├── mushroomsCloud/
│   │   ├── mysite/             # Django project root
│   │   │   ├── __pycache__/
│   │   │   ├── asgi.py
│   │   │   ├── settings.py     # Django settings
│   │   │   ├── urls.py         # Project URL mappings
│   │   │   ├── wsgi.py
│   │   │
│   │   ├── polls/              # Django app (custom logic)
│   │   │   ├── __pycache__/
│   │   │   ├── migrations/
│   │   │   ├── templates/      # HTML templates
│   │   │   ├── __init__.py
│   │   │   ├── admin.py
│   │   │   ├── apps.py
│   │   │   ├── models.py       # Django ORM models
│   │   │   ├── tests.py
│   │   │   ├── urls.py         # App-level routes
│   │   │   ├── views.py        # Request handling + ML calls
│   │   │
│   │   ├── Mushs.pickle        # Saved baseline model
│   │   ├── MushsPCA.pickle     # Saved PCA + RF model
│   │   ├── db.sqlite3          # SQLite DB
│   │
│   ├── Flow.txt                # Workflow notes
│   ├── manage.py               # Django entry point
│   ├── Procfile                # For deployment (gunicorn)
│   ├── requirements.txt        # Dependencies
│   ├── runtime.txt             # Python version for deployment
│   ├── mushrooms.csv           # Dataset
│   ├── Mushrooms.ipynb         # Jupyter ML notebook
```

---

## ⚙️ Requirements (corrected)

```txt
asgiref==3.2.10
Django==3.1
gunicorn==20.1.0
joblib==1.0.1
numpy==1.21.2
pandas==1.3.2
python-dateutil==2.8.2
pytz==2021.1
scikit-learn==0.24.2
scipy==1.7.1
six==1.16.0
sqlparse==0.4.1
threadpoolctl==2.2.0
```

> ❌ `sklearn==0.0` and `sql3` removed (invalid).

---

## 🧠 ML Pipeline (PCA + RF)

* Preprocess: **StandardScaler** (numeric), **OneHotEncoder** (categorical)
* PCA: `n_components=7`
* RandomForest: `n_estimators=300`
* Exported using `joblib.dump()` → `MushsPCA.pickle`

---

## 🚀 Run Locally

```bash
# Activate environment
source .venv/bin/activate   # Linux/Mac
.venv\Scripts\activate      # Windows

# Install deps
pip install -r requirements.txt

# Run Django app
python manage.py runserver
```

Now visit: [http://127.0.0.1:8000](http://127.0.0.1:8000)

---

## 🌐 Deploy to Cloud (Heroku/Render)

1. Ensure `Procfile`, `requirements.txt`, `runtime.txt` are correct.
2. Push repo to GitHub.
3. Connect Heroku/Render → Deploy.

Procfile example:

```
web: gunicorn mushroomsCloud.mysite.wsgi --log-file -
```

---

## 🧪 Jupyter Notebook (Testing)

* Load dataset → preprocess → PCA → RF.
* Train/test accuracy printed.
* Model saved to `/models/MushsPCA.pickle`.
* Reloaded model verified.

---

## 🎮 User Interaction Flow (Web App)

1. User visits the app homepage (`/polls` or custom route).
2. Form appears with mushroom attributes (cap shape, color, odor, etc.).
3. User selects values from dropdowns.
4. Form data is passed to **views.py**, which loads `MushsPCA.pickle`.
5. ML pipeline predicts edible/poisonous.
6. Result displayed on a new template page with **prediction result**.

---

## ✅ Project Checklist

### General

* [x] Virtual environment created
* [x] Requirements installed
* [x] Django project initialized
* [x] Polls app created and registered
* [x] Database migrated successfully

### Machine Learning

* [x] Mushroom dataset loaded (`mushrooms.csv`)
* [x] Features/labels split
* [x] Preprocessing pipeline created
* [x] PCA applied (7 components)
* [x] RandomForest trained (300 trees)
* [x] Train/Test accuracy evaluated
* [x] Model saved (`MushsPCA.pickle`)
* [x] Reloaded model tested successfully

### Web App

* [x] Forms connected to model
* [x] Views return predictions
* [x] Templates render prediction results
* [x] URLs configured correctly

### Deployment

* [x] Procfile added
* [x] runtime.txt set to correct Python version
* [x] requirements.txt validated
* [ ] App deployed to Heroku/Render
* [ ] Model tested in production

---

## 📌 Future Improvements

* Add REST API (Django REST Framework) for ML inference.
* Add authentication (login/logout).
* Store prediction history in database.
* Deploy Dockerized version for portability.
