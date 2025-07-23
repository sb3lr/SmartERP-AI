# SmartERP AI – Intelligent ERP System with AI-Powered Image and Invoice Analysis

## Project Goal
To develop a full-stack web-based ERP platform that integrates artificial intelligence for automating image recognition, invoice analysis, financial recommendations, and customer behavior prediction. The system will support multiple user roles and provide a dashboard interface with data visualization and smart decision support.

## System Overview

The system will have the following main modules:

* Core ERP: inventory, invoices, transactions, user roles.
* AI Vision Module: image and invoice analysis using OCR and object detection.
* AI Financial Advisor: pricing suggestions and cost analysis.
* Invoice Organizer: structured storage and sorting of invoices.
* Product Recommender: user preference–based product suggestions.
* Dashboard: dynamic reporting and charts.
* Authentication and Role Management.

## Tech Stack

### Backend

* Language: Python 3.11+
* Framework: FastAPI (with Pydantic models, async support)
* Dependency Manager: Poetry or Pip with venv
* Environment Variables: managed via .env and python-dotenv

### Frontend

* Language: JavaScript or TypeScript
* Framework: React.js (with functional components and Hooks)
* State Management: Redux Toolkit
* UI Framework: Tailwind CSS or Material UI
* Chart Library: Chart.js or Recharts

### Database

* Primary DBMS: PostgreSQL
* ORM: SQLAlchemy or Tortoise ORM with FastAPI
* Migrations: Alembic

### Authentication and Authorization

* JWT-based authentication with role-based access control
* OAuth2 login support (optional)
* Secure password hashing using bcrypt

### File Storage

* Local server file system (/uploads) for MVP
* Image size limits and MIME-type validation

## AI and OCR Components

### OCR for Text Extraction from Images

* Engine: Tesseract OCR (wrapped via pytesseract)
* Preprocessing: OpenCV (grayscale, thresholding, denoising)
* Layout Parsing (optional advanced): LayoutLM (HuggingFace)

### Image Object Detection (Product Recognition)

* Model: YOLOv8 (Ultralytics)
* Runtime: Python inference pipeline
* Task: detect product type, label, barcode from image

### Financial Advisor (AI Recommendation Engine)

* Engine: Custom Python logic using Pandas and Scikit-learn
* Inputs: staff count, salaries, fixed costs, selling prices
* Outputs: profit margin estimation, price suggestions, daily or monthly reports

### Customer Recommender

* Model: NLP-based recommendation engine
* Tech: OpenAI GPT-4 API or sentence transformers (BERT) for matching preferences
* Fallback: Rule-based filtering from database based on tags or metadata

## Key Features

### Core ERP Functionality

* Product and inventory management (CRUD)
* Customer and supplier database
* Invoice creation (manual and AI-based)
* Daily transaction logging
* User permission levels: Admin, Accountant, Client

### Image and Invoice Processing

* Upload images via frontend
* OCR and vision analysis to extract:

  * Product name, quantity, price, barcode
* Auto-link invoice to a customer if matched
* Store structured data in database

### AI Financial Module

* Interactive form for financial data entry
* Analysis of:

  * Operating costs
  * Profit margins
  * Suggested pricing
  * Cost-cutting tips
* Exportable report (CSV, Excel, or printable HTML)

### Invoice Organizer

* Classify by client and date
* Identify and group recurring items
* Export summary tables per day or week

### Personalized Product Recommender

* Ask users for preferences (color, category, brand)
* Suggest matching products from internal database
* Optionally integrate Amazon, Noon, or AliExpress APIs
* Show availability status and buy link

### Smart Dashboard

* Total sales, revenue, top products, clients
* Filters: daily, weekly, monthly
* Visualized with interactive charts
* Automated insights and recommendations

## User Roles

* Admin: Full system control, manage users, products, invoices
* Accountant: View and add invoices, run financial reports
* Client: Upload images, view matched products, receive suggestions
* AI Agent (internal): Non-human, executes AI logic and analysis

## APIs and Integrations

* RESTful API structure
* Protected endpoints with JWT
* Upload API (image/jpeg, image/png, max 5MB)
* External APIs (optional): Amazon or Noon product search via public APIs
* All AI modules must be locally hostable; no paid services unless specified (OpenAI optional)

## Deployment Plan

* Local development: Docker and docker-compose
* Production: VPS with Ubuntu 22.04+, Nginx, Gunicorn or Uvicorn
* Static file handling: Nginx
* Frontend build: Vite with React
* Backend served via API route

## Getting Started

This guide will walk you through setting up and running the SmartERP AI project on your local machine for development and testing purposes.

### Prerequisites

Before you begin, ensure you have the following installed on your system:

*   **Docker:** [Get Docker](https://docs.docker.com/get-docker/)
*   **Docker Compose:** [Install Docker Compose](https://docs.docker.com/compose/install/)
*   **Git:** [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

### Installation

1.  **Clone the repository:**

    ```bash
    git clone <repository-url>
    cd V2
    ```

2.  **Configure Backend Environment:**

    Navigate to the `backend` directory and create a `.env` file by copying the example file:

    ```bash
    cp backend/.env.example backend/.env
    ```

    Open the `backend/.env` file and modify the variables if necessary. The default values are configured to work with the provided `docker-compose.yml`.

    ```
    DATABASE_URL=postgresql://user:password@db/smarterp
    SECRET_KEY=your_secret_key_please_change
    ALGORITHM=HS256
    ACCESS_TOKEN_EXPIRE_MINUTES=30
    ```

    **Important:** For a production environment, you must change `SECRET_KEY` to a strong, unique secret.

### Running the Application (Recommended: Docker)

Once you have completed the installation steps, you can start the application using Docker Compose. This is the recommended way to run the project for a consistent development environment.

1.  **Build and Start Containers:**

    From the **root of the `V2` directory**, run the following command:

    ```bash
    docker-compose up --build
    ```

    This command will build the Docker images for the frontend and backend services and then start the containers. The `--build` flag ensures that the images are rebuilt if there are any changes to the `Dockerfile` or the source code.

2.  **Accessing the Application:**

    *   **Frontend:** Open your web browser and navigate to [http://localhost:3000](http://localhost:3000)
    *   **Backend API:** The backend API will be available at [http://localhost:8000](http://localhost:8000)
    *   **API Documentation:** Interactive API documentation (Swagger UI) is available at [http://localhost:8000/docs](http://localhost:8000/docs)

### Stopping the Application (Docker)

To stop the application and shut down the containers, press `Ctrl+C` in the terminal where `docker-compose` is running, and then run:

```bash
docker-compose down
```

This will stop and remove the containers and the network created by `docker-compose up`.

### Running the Application (Alternative: Manually)

If you prefer not to use Docker, you can run the frontend and backend services separately. You will need to have **Node.js** and **Python** installed on your system.

#### Running the Backend

1.  **Navigate to the backend directory:**

    ```bash
    cd backend
    ```

2.  **Create a virtual environment and install dependencies:**

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    pip install -r requirements.txt
    ```

3.  **Start the backend server:**

    ```bash
    uvicorn app.main:app --reload
    ```

    The backend will be running at [http://localhost:8000](http://localhost:8000).

#### Running the Frontend

1.  **Navigate to the frontend directory:**

    ```bash
    cd frontend
    ```

2.  **Install dependencies:**

    ```bash
    npm install
    ```

3.  **Start the frontend development server:**

    ```bash
    npm start
    ```

    The frontend will be running at [http://localhost:3000](http://localhost:3000).

## Project Structure

*   `backend/`: Contains the FastAPI application, including all API logic, database models, and AI services.
*   `frontend/`: Contains the React.js application, including all UI components, pages, and state management logic.
*   `uploads/`: A directory used for temporary storage of uploaded files (e.g., images for OCR).
*   `docker-compose.yml`: Defines the services, networks, and volumes for the Docker application.

## User Roles & Default Credentials

For testing purposes, you can use the following default user roles and credentials. These will need to be created in the database first.

*   **Admin:**
    *   **Email:** `admin@example.com`
    *   **Password:** `admin123`
*   **Accountant:**
    *   **Email:** `accountant@example.com`
    *   **Password:** `accountant123`
*   **Client:**
    *   **Email:** `client@example.com`
    *   **Password:** `client123`

## Loading Sample Data

To populate the database with sample data for testing, you will need to run a database seeding script. (A script for this will be provided at `backend/app/initial_data.py` and can be executed after the application is running).

## Deliverables

* Complete source code (Git-based)
* Fully functional frontend and backend
* Setup and run instructions (README.md and .env.example)
* API documentation (OpenAPI or Swagger UI)
* Sample database dump for testing
* Deployment guide with server configuration
* Admin dashboard with working CRUD and AI integration
* At least one example dataset (invoices, products, user types)
