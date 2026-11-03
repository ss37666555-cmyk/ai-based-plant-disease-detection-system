# PhytoAI: AI-Based Plant Disease Detection System

[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110+-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.15+-EE4C2C?logo=pytorch&logoColor=white)](https://pytorch.org/)
[![React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=black)](https://react.dev/)
[![TailwindCSS](https://img.shields.io/badge/Tailwind-3.4+-38B2AC?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![SQLite](https://img.shields.io/badge/Database-SQLite%203-003B57?logo=sqlite&logoColor=white)](https://www.sqlite.org/)

An enterprise-grade, modern, and responsive full-stack artificial intelligence web application designed for automated plant leaf disease diagnosis, pathogen classification, and precision agronomy guidance.

---

## 🌟 Key Features

- **Automated Plant Pathology Detection**: Classifies **38 distinct plant conditions** (healthy foliage and diseases) across **14 major agricultural crops** (Tomato, Potato, Corn, Apple, Grape, Pepper, Peach, Strawberry, Cherry, Soybean, Orange, Squash, Raspberry, Blueberry).
- **Dual Input Modes**: 
  - Drag-and-drop or file upload (JPG, JPEG, PNG, WEBP).
  - Live webcam and mobile camera capture with circular leaf alignment guides.
- **Deep Learning Model (PyTorch & MobileNetV2)**:
  - Preprocesses and rescales images to 224×224 RGB tensors with ImageNet normalization.
  - Multi-class Softmax probability distribution with top-5 candidate hypotheses.
  - Intelligent Computer Vision chromatic diagnostic fallback engine for instant demonstrations without requiring gigabytes of training weights.
- **Complete Agronomic Protocol**:
  - Detailed disease description, pathogen taxonomy, and severity rating.
  - Clinical symptom checklist and probable environmental triggers.
  - Recommended biological, organic, and chemical treatment options.
  - Long-term preventative agronomy practices (crop rotation, aeration, drip irrigation).
- **Persistent Historical Archive (SQLite & SQLAlchemy)**:
  - Saves all uploaded leaf images to `/uploads`.
  - Records detection metadata, timestamps, confidence scores, and symptoms.
  - Search and filter by crop species and health status with pagination.
  - Printable / PDF diagnostic pathology reports with one click (`window.print()`).
- **Real-Time Analytics Dashboard**:
  - Live statistics: total scans, healthy vs. diseased distribution, model accuracy, and recently logged scans.

---

## 📂 Project Directory Structure

```text
plant-disease-detection/
├── frontend/                     # Modern React + Vite Single Page App
│   ├── public/                   # Static assets and icons
│   ├── src/
│   │   ├── components/           # Reusable UI components
│   │   │   ├── Navbar.jsx        # Sticky navigation with live backend status ping
│   │   │   ├── Footer.jsx        # Agricultural themed footer & disclaimers
│   │   │   ├── CameraModal.jsx   # Live webcam / mobile camera viewfinder
│   │   │   ├── LoadingOverlay.jsx# Animated 4-step neural analysis overlay
│   │   │   └── ReportModal.jsx   # Modal for full printable pathology reports
│   │   ├── pages/                # Top-level application views
│   │   │   ├── Home.jsx          # Dashboard, live stats, crop catalog, how-it-works
│   │   │   ├── Detect.jsx        # Image uploader, drag-and-drop, sample presets
│   │   │   ├── Results.jsx       # Detailed diagnosis, treatments, prevention
│   │   │   ├── History.jsx       # Database records, search, filter, delete
│   │   │   └── About.jsx         # Technical overview, PlantVillage specs, contact
│   │   ├── services/
│   │   │   └── api.js            # Axios client configured for FastAPI endpoints
│   │   ├── App.jsx               # Application root & view state router
│   │   ├── index.css             # Tailwind base and print styling
│   │   └── main.jsx              # React DOM entry point
│   ├── index.html                # HTML document entry
│   ├── package.json              # NPM dependencies & build scripts
│   ├── tailwind.config.js        # Agricultural color themes & extensions
│   ├── postcss.config.js         # PostCSS configuration
│   └── vite.config.js            # Vite build configuration
├── backend/                      # High-throughput FastAPI REST API
│   ├── database/
│   │   ├── db.py                 # SQLite engine & SQLAlchemy SessionLocal dependency
│   │   └── plant_disease.db      # Transactional SQLite database file
│   ├── models/
│   │   ├── detection.py          # SQLAlchemy ORM DetectionRecord table model
│   │   └── schemas.py            # Pydantic request and response schemas
│   ├── routes/
│   │   ├── predict.py            # POST /api/predict endpoint
│   │   └── history.py            # GET /api/history, GET /api/stats, DELETE endpoints
│   ├── services/
│   │   └── detection_service.py  # File validation, upload handling, DB persistence
│   ├── requirements.txt          # Python backend package dependencies
│   └── main.py                   # FastAPI server entry point, CORS, static mounts
├── ai_model/                     # Machine Learning and Agronomic Knowledge Base
│   ├── model.py                  # PyTorch MobileNetV2 & Lightweight CNN architectures
│   ├── train.py                  # Training pipeline with data augmentations & validation
│   ├── predict.py                # Inference pipeline, tensor transforms, fallback engine
│   ├── disease_info.py           # Comprehensive 38-class PlantVillage knowledge base
│   └── requirements.txt          # AI training dependencies
├── uploads/                      # Permanent filesystem storage for scanned leaf images
├── .env.example                  # Environment variable template
└── README.md                     # Comprehensive project documentation
```

---

## 🚀 Getting Started

### Prerequisites

Ensure you have installed:
1. **Python 3.10+** (Python 3.11 recommended)
2. **Node.js 18+** & **npm**

---

### 1. Backend Installation & Setup

Navigate into the backend and install the required Python packages:

```bash
# From workspace root
python -m pip install -r backend/requirements.txt
```

#### Run the FastAPI Backend Server:

```bash
python -m uvicorn backend.main:app --host 0.0.0.0 --port 8000 --reload
```

- **API Documentation (Swagger UI)**: [http://localhost:8000/docs](http://localhost:8000/docs)
- **Alternative ReDoc UI**: [http://localhost:8000/redoc](http://localhost:8000/redoc)
- **Health Check Endpoint**: [http://localhost:8000/api/health](http://localhost:8000/api/health)

---

### 2. Frontend Installation & Setup

In a separate terminal, navigate into `frontend`:

```bash
cd frontend
npm install
npm run dev
```

The web application will launch at:
👉 **[http://localhost:5173](http://localhost:5173)**

To produce an optimized production build:
```bash
npm run build
npm run preview
```

---

## 🌿 AI Model & PlantVillage Training Instructions

The application supports training custom weights or loading an existing checkpoint:

### Recommended Dataset
- **PlantVillage Dataset**: Contains 54,303 healthy and diseased agricultural leaf images.
- Can be downloaded from [Kaggle: PlantVillage Dataset](https://www.kaggle.com/datasets/emmarex/plantdisease) or GitHub.

### Training Your Own Weights

1. Extract the PlantVillage dataset into a folder structured as:
   ```text
   dataset/
   ├── Apple___Apple_scab/
   ├── Apple___Black_rot/
   ├── Apple___healthy/
   ├── Tomato___Early_blight/
   └── ...
   ```
2. Run the training script:
   ```bash
   python ai_model/train.py --data_dir ./dataset --epochs 15 --batch_size 32 --lr 0.0003
   ```
3. The script automatically uses Cosine Annealing, CrossEntropyLoss, and saves the best model checkpoint to `ai_model/plant_disease_model.pth`.
4. When `backend/main.py` starts, it automatically detects `ai_model/plant_disease_model.pth` and switches inference mode to **Trained MobileNetV2 Weights**.

---

## 📡 REST API Reference

### 1. `POST /api/predict`
Accepts a plant leaf image, runs inference, saves the file to `/uploads`, stores the record in SQLite, and returns diagnosis details.
- **Content-Type**: `multipart/form-data`
- **Body**: `image` (binary file: JPG, PNG, WEBP)

#### Sample cURL Request:
```bash
curl -X POST "http://localhost:8000/api/predict" \
  -H "accept: application/json" \
  -H "Content-Type: multipart/form-data" \
  -F "image=@sample_leaf.jpg"
```

#### Sample JSON Response:
```json
{
  "id": 1,
  "image_url": "/uploads/3b9e4a8f_sample_leaf.jpg",
  "class_name": "Tomato___Early_blight",
  "plant_name": "Tomato",
  "disease_name": "Early Blight",
  "is_healthy": false,
  "confidence": 92.4,
  "pathogen": "Alternaria linariae / solani (Fungus)",
  "severity": "High",
  "description": "Early blight is one of the most common and pervasive fungal diseases of tomatoes. It begins on bottom foliage...",
  "symptoms": [
    "Dark brown to black spots with concentric rings creating a distinct 'target board' pattern",
    "Broad yellow halo surrounding each expanding necrotic lesion",
    "Lower foliage turns yellow, withers, and collapses"
  ],
  "causes": [
    "Warm temperatures (24°C - 29°C) accompanied by frequent rains or heavy dew",
    "Fungal spores overwintering in infected tomato stakes and plant refuse"
  ],
  "treatment": [
    "Apply Chlorothalonil, Copper hydroxide, or Mancozeb at the first sign of lower spotting",
    "Prune off and safely bag all infected bottom leaves"
  ],
  "prevention": [
    "Prune lower suckers to maintain at least 12-18 inches of air space above mulch",
    "Apply 3-4 inches of clean straw or plastic mulch beneath each tomato vine",
    "Sanitize tomato stakes with 10% bleach between seasons"
  ],
  "top_predictions": [
    {
      "class_name": "Tomato___Early_blight",
      "plant_name": "Tomato",
      "disease_name": "Early Blight",
      "is_healthy": false,
      "confidence_score": 92.4
    },
    {
      "class_name": "Potato___Early_blight",
      "plant_name": "Potato",
      "disease_name": "Early Blight",
      "is_healthy": false,
      "confidence_score": 5.1
    }
  ],
  "inference_time_ms": 32.5,
  "model_source": "MobileNetV2 Feature & Chromatic Diagnostic Engine",
  "is_demo_mode": true
}
```

### 2. `GET /api/history`
Query parameters:
- `search`: Keyword string for crop or disease.
- `plant`: Filter by crop name (e.g. `Tomato`, `Potato`, `Apple`).
- `status_filter`: `healthy`, `diseased`, or `all`.
- `page`: Page index (default: `1`).
- `limit`: Number of items per page (default: `12`).

### 3. `GET /api/history/{id}`
Retrieves complete record details including leaf image URL, symptoms, causes, and treatments.

### 4. `DELETE /api/history/{id}`
Deletes the detection record from SQLite and removes the image from `/uploads`.

### 5. `GET /api/stats`
Returns aggregated dashboard metrics (total detections, healthy count, diseased count, accuracy rate, top crops, top diseases).

### 6. `GET /api/health`
Returns system health, PyTorch compute device (`cpu` / `cuda`), and total supported classes.

---

## 🛡️ Agronomic Disclaimer

PhytoAI is intended as a field decision-support and educational tool. Agricultural producers and growers should consult local university agricultural extension agents or certified agronomists before administering high-volume synthetic fungicides or commercial bactericides.

---

## 📄 License
This project is licensed under the MIT License.
