# NAMASTE AYUSH EHR Platform

[![HL7 FHIR R4](https://img.shields.io/badge/HL7-FHIR%20R4-orange.svg)](https://hl7.org/fhir/R4/)
[![ICD-11 TM2](https://img.shields.io/badge/WHO-ICD--11%20TM2-blue.svg)](https://icd.who.int/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.95+-green.svg)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-19-61dafb.svg)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-7-purple.svg)](https://vitejs.dev/)

An advanced, FHIR R4-compliant Electronic Health Record (EHR) and terminology integration platform for India's AYUSH sector (Ayurveda, Siddha, Unani). It seamlessly maps traditional medicine terminologies (NAMASTE) with WHO ICD-11 Traditional Medicine Module 2 (TM2) and biomedicine standards.

---

## Key Features

- **Standardized Terminology Mapping**: Search and map 4,500+ NAMASTE codes across Ayurveda, Siddha, and Unani to WHO ICD-11 TM2 and biomedicine standards.
- **FHIR R4 Resources**: Generate standard FHIR `CodeSystem`, `ConceptMap`, `ValueSet`, `Condition`, and `Bundle` resources for clinical interoperability.
- **ABHA ID Authentication**: Integrated mock ABHA ID authentication and OTP verification workflow.
- **Dual Coding Interface**: Bidirectional translation between traditional medicine concepts and ICD-11 classifications with real-time suggestions.
- **Interactive Documentation**: Built-in Swagger UI, ReDoc, and static API explorer pages.
- **Production Ready Deployment**: Fully configured for Vercel (frontend) and Docker/Coolify (backend).

---

## Project Structure

```text
NAMASTE/
├── backend/            # FastAPI REST API, FHIR resources, and authentication
│   ├── app/            # Application routes, models, services, database
│   ├── ayush_emr.db    # SQLite database
│   ├── Dockerfile      # Container definition
│   └── requirements.txt# Python dependencies
├── frontend/           # React 19 + Vite web application
│   ├── public/         # Static assets and API documentation (public/api/)
│   ├── src/            # Components, pages, routing, and context
│   └── package.json    # Frontend dependencies and build scripts
├── api/                # Terminology databases (Ayurveda, Siddha, Unani, ICD-11)
├── who-api/            # WHO terminology dataset and helper scripts
├── vercel.json         # Vercel deployment configuration
└── package.json        # Root workspace scripts for unified builds
```

---

## Prerequisites

- **Node.js**: v18.0.0 or newer
- **npm**: v9.0.0 or newer
- **Python**: v3.8 or newer (for backend)

---

## Quick Start (Local Development)

### 1. Start the Backend API

```powershell
cd backend
python -m venv venv

# Windows (PowerShell)
.\venv\Scripts\Activate.ps1
# Linux / macOS
# source venv/bin/activate

pip install -r requirements.txt
python start_server.py
```
*API will run at `http://localhost:8000`.*

### 2. Start the Frontend

From the repository root:
```powershell
npm install
npm run dev
```
*Or directly in the `frontend/` directory:*
```powershell
cd frontend
npm install
npm run dev
```
*Web app will be available at `http://localhost:5173`.*

---

## Deploying to Vercel

The repository includes pre-configured root and frontend `vercel.json` files for zero-configuration deployments.

### Option A: Deploy from Repository Root (Recommended)
1. Import your GitHub repository into [Vercel](https://vercel.com).
2. Leave the **Root Directory** setting as default (`.`).
3. Set **Framework Preset** to `Vite`.
4. (Optional) In **Environment Variables**, add:
   - `VITE_API_URL`: URL of your deployed backend (e.g., `https://your-backend-api.com/api`).
5. Click **Deploy**.

### Option B: Deploy `frontend/` Subfolder
1. When importing to Vercel, set the **Root Directory** to `frontend`.
2. Build command and output directory are automatically detected (`npm run build` / `dist`).
3. Set `VITE_API_URL` environment variable if connecting to a remote backend.
4. Click **Deploy**.

---

## API Documentation & Exploration

When running the backend:
- **Interactive Swagger UI**: `http://localhost:8000/docs`
- **ReDoc**: `http://localhost:8000/redoc`
- **Health Check**: `http://localhost:8000/api/health`

### Main API Routes

| Endpoint | Method | Description |
| :--- | :--- | :--- |
| `/api/auth/generate-otp` | `POST` | Generate OTP for ABHA ID / Mobile |
| `/api/auth/verify-otp` | `POST` | Verify OTP and obtain JWT access token |
| `/api/patients` | `GET`, `POST` | Manage patient profiles and records |
| `/api/diseases/search` | `GET` | Search NAMASTE and ICD-11 TM2 terms |
| `/api/fhir/CodeSystem/{id}` | `GET` | Retrieve FHIR CodeSystem resource |
| `/api/fhir/ConceptMap/{id}` | `GET` | Retrieve FHIR ConceptMap resource |
| `/api/fhir/ConceptMap/$translate` | `POST` | Translate between NAMASTE and ICD-11 |
| `/api/fhir/Bundle` | `POST` | Ingest and validate FHIR clinical bundles |

---

## Demo Access Credentials

To test the demo and FHIR functionality (e.g. at `/fhir-demo`):
- **Mock ABHA ID**: `91-1234-5678-9012` (or `91-9876-5432-1098`)
- **Mock OTP**: Any 6-digit number (e.g., `123456`)

---

## License

This project is licensed under the MIT License.