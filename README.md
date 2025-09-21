# Plant-Anomaly
plant anomaly detection through images using ML AI 

# 🌱 Plant Anomaly Detection Web App — Technical Specification

This document contains all the key features and details needed to start developing the **Plant Anomaly Detection Web Application** with an AI assistant (e.g., Cursor AI).

---

## 1️⃣ Goal
A web platform where users upload a plant photo and get a report on detected anomalies (e.g., diseases) using AI/ML.  
First release targets **olive trees**, later expands to other Tunisian crops.

---

## 2️⃣ Core Features
| Area | Features |
|------|-----------|
| **Image Analysis** | Upload image → ML model detects anomaly → returns class & confidence |
| **Reporting** | Show result in clear text (e.g., “Olive Leaf Spot detected, 92% confidence”) |
| **Multi-language UI** | Arabic, French, English |
| **User Roles** | Farmer / Agronomist (simple login optional later) |
| **Dataset Mgmt (Admin)** | Upload new images with labels to improve model |
| **Logs** | Store predictions & confidence for retraining |
| **Scalability** | PoC doesn’t need heavy infra, but design for cloud deployment |
| **Future (Post-PoC)** | Mobile app, suggestions for treatment, push notifications |

---

## 3️⃣ Architecture
- **Frontend:** React (hooks, context API for language switch)
- **Backend API:**  
  - Option A: Spring Boot  
  - Option B: ASP.NET Core  
  - Endpoints:  
    - `POST /detect` → image → JSON result  
    - `GET /health` → service status  
    - `POST /feedback` → user feedback for active learning
- **ML Service:**  
  - Python (FastAPI or Flask) hosting trained model, or integrated inside backend if feasible.
  - Start with public models (PlantVillage) → fine-tune with Tunisian crops.

---

## 4️⃣ ML Workflow
1. **Baseline Training**
   - Use pre-trained CNN (EfficientNet/MobileNet) or YOLOv8.
   - Train on global datasets (PlantVillage, PlantDoc).
2. **Integration**
   - Export model as `.h5` or `.pt`.
   - Load in backend (ONNX/TensorFlow SavedModel).
3. **Local Adaptation**
   - Collect Tunisian images, fine-tune last layers.
   - Version models (`model_v1_global`, `model_v2_tunisia`).

---

## 5️⃣ Data Strategy
- **Initial data:** Public/global plant disease datasets.
- **Local data:** Agronomist captures olive leaf photos (healthy/diseased).
- **Storage:** Organized in folders:
  ```
  data/
    train/
      healthy/
      olive_spot/
      ...
    val/
    test/
  ```
- **Augmentation:** brightness, rotation, blur, shadows.

---

## 6️⃣ UI / UX Requirements
- Clean dashboard for uploading images.
- Preview of uploaded photo + result (disease name + confidence).
- Support Arabic/French/English toggle.
- Simple “help” section with instructions for farmers.

---

## 7️⃣ Deployment
- **Dev stage:** Run locally (React + backend + ML server).
- **Cloud (PoC):** Any (Azure, AWS, GCP).
- **Later:** Containerize (Docker) → Kubernetes or App Service.

---

## 8️⃣ Security & Privacy
- Store only minimal image data (if needed for retraining).
- GDPR-compliant if images contain identifiable info (unlikely).

---

## 9️⃣ Roadmap
| Phase | Deliverables |
|-------|--------------|
| P0 | Environment & datasets ready |
| P1 | Baseline ML model trained |
| P2 | Backend API + ML integration |
| P3 | React frontend (upload + result) |
| P4 | Tunisian dataset & fine-tuning |
| P5 | Mobile app (after web MVP) |

---

## 🔗 Suggested Tools
- **ML:** TensorFlow/Keras or PyTorch, Albumentations for augmentation.
- **Backend-ML Bridge:** FastAPI or gRPC between backend & Python service.
- **Version control:** GitHub/GitLab.
- **Issue tracking:** GitHub Projects / Trello.

---

### 👉 Next Steps for Cursor AI
1. Scaffold a **React app** (image upload, multilingual layout).
2. Scaffold a **Spring Boot** or **ASP.NET Core** API with `/detect` endpoint.
3. Create a **Python ML microservice** (FastAPI) for inference.
4. Set up local dev environment: React → API → ML service integration.
5. Prepare unit tests for API and frontend components.
