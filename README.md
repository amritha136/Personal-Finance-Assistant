# Personal Finance Assistant

This project is a full-stack web application designed to help users track, manage, and understand their financial activities. It is packaged as a single, self-contained Google Colab notebook that sets up its own backend server, database, and provides client-side code for interacting with all features.

## ✨ Features

The application implements all core requirements from the project assignment, along with several bonus features to enhance functionality and robustness.

### Core Features
- **User Authentication:** Secure user registration and login system with password hashing.
- **Transaction Management:** Ability to create, and list income and expense entries.
- **Data Extraction (OCR):** Extracts expense details from uploaded receipt images or PDFs using Tesseract OCR.
- **Data Visualization:** Generates graphs to summarize financial habits.

### Bonus Features
- **Multi-User Support:** The application is built to handle multiple distinct users.
- **API Pagination:** The transaction list endpoint (`/transactions`) supports pagination.
- **Tabular PDF Parsing:** Extracts transaction data from uploaded PDF bank statements that are in a tabular format.

### Data Visualizations
- **Expenses by Category:** A pie chart showing the distribution of expenses across different categories.
- **Daily Expense Trend:** A bar chart visualizing the total amount spent each day.
- **Income vs. Expense:** A summary bar chart comparing total income against total expenses for a clear financial overview.

## 💻 Technology Stack

- **Backend:** Flask, Gunicorn
- **Database:** SQLAlchemy (with SQLite)
- **Authentication:** Flask-JWT-Extended
- **OCR:** Tesseract (`pytesseract`, `pdf2image`)
- **PDF Parsing:** `tabula-py`
- **Data Handling & Plotting:** Pandas, Matplotlib
- **Deployment (for Colab):** `pyngrok` for exposing the local server

## 🚀 Setup and Usage Instructions

This notebook is designed to run entirely within the Google Colab environment.

### Prerequisites
1.  A Google Account (to use Google Colab).
2.  A free **ngrok** account (to create a public URL for the API).

### Step-by-Step Guide

1.  **Configure Colab Secrets (❗️Crucial Step)**
    Before running the notebook, you **must** add your ngrok authtoken to the Colab Secrets Manager.
    - Click the **key icon(🔑)** on the left sidebar in Colab.
    - Click **"Add a new secret"**.
    - For the **Name**, enter `NGROK_AUTH_TOKEN`.
    - For the **Value**, paste your personal ngrok token.
    - Ensure the "Notebook access" toggle is enabled.

2.  **Upload and Run the Notebook**
    - Upload the `personal_finance_assistant.ipynb` file to Google Colab.
    - To execute the entire project, simply run all cells in order from top to bottom. The easiest way is to go to the menu and select **`Runtime > Run all`**.

3.  **Interact with the Application**
    - The notebook will first install dependencies and set up the file structure.
    - It will then start the Flask server and create a public URL using ngrok.
    - The subsequent cells in "Step 5" allow you to interact with all API features, from registering a user to generating graphs.

## 📁 Project Structure

The notebook programmatically creates the following file structure within the Colab environment:
├── personal_finance_assistant.ipynb
├── backend/
│   ├── app.py          # Main Flask application with all API endpoints
│   ├── models.py       # SQLAlchemy database models (User, Transaction)
│   ├── database.py     # SQLAlchemy database instance setup
│   └── ocr.py          # Logic for OCR and PDF table extraction
├── templates/
│   └── index.html      # Simple homepage for the API
├── static/
│   └── styles.css
└── test_data/          # Contains sample files generated for testing uploads

## 🔌 API Endpoints

The backend provides the following RESTful API endpoints:

- `POST /register`: Register a new user.
- `POST /login`: Log in a user and receive a JWT token.
- `POST /transactions`: Add a new income or expense transaction (requires auth).
- `GET /transactions`: List all transactions for the logged-in user (supports filtering and pagination, requires auth).
- `POST /extract-receipt`: Upload a receipt image/PDF for OCR analysis (requires auth).
- `POST /extract-statement`: Upload a tabular PDF statement for data extraction (requires auth).
