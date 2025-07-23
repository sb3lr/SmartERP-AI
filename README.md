
# SmartERP AI
 
## 1. Project Overview

An intelligent, comprehensive ERP system designesd for managing small and medium-sized businesses, combining:

- Complete management of inventory, invoices, customers, and users.
- Integration of AI technologies for analyzing invoice and product images (OCR + Object Detection).
- Smart financial recommendations for product pricing and profit analysis.
- A user-friendly and modern interface.
- Self-hosted deployment on the client’s server.
- One-time purchase licensing model with a unique license per client.

## 2. System Components and Detailed Description

### A. Core ERP Module  
**Main Functions:**  
- **Inventory Management**  
  - CRUD (Create, Read, Update, Delete) for products.  
  - Tracking quantities and stock availability.  
  - Categorizing products by type, brand, and category.  

- **Customer and Supplier Management**  
  - CRUD for personal and financial data.  
  - Recording transaction history for each customer or supplier.  

- **Invoices and Financial Transactions**  
  - Creating manual invoices and linking automatically processed invoices and images.  
  - Tracking invoice status (paid, pending, overdue).  
  - Recording daily financial transactions.  

- **User Roles System**  
  - Roles: Admin, Accountant, Client.  
  - Specific permissions per role (e.g., clients can only upload invoices and view their recommendations).  

- **Financial Reports**  
  - Periodic reports (weekly, monthly) on sales, profits, and stock.  
  - Exporting reports in Excel, CSV, and PDF formats.  

### B. AI Vision Module  
**Main Functions:**  
- **OCR (Text Extraction from Images)**  
  - Using Tesseract OCR combined with OpenCV for image enhancement (contrast improvement, noise removal).  
  - Analyzing colored or black-and-white invoice images.  

- **Object Detection (Product and Barcode Detection)**  
  - Using YOLOv8 to identify products, barcodes, and quantities in product and invoice images.  

- **Automatic Linking**  
  - Automatically linking invoice data (products, prices, clients) to system records.  

### C. Financial Advisor Module  
**Main Functions:**  
- Analyzing cost data (salaries, fixed and variable expenses).  
- Calculating profit margins and providing competitive pricing recommendations.  
- Suggesting ways to improve profitability and reduce costs.  
- Generating detailed financial reports with export options.  

### D. Invoice Organizer  
- Organizing invoices with easy search and filtering by date, client, or product.  
- Grouping recurring invoices and analyzing them periodically.  
- Supporting uploading invoice images or PDFs linked to invoices.  

### E. Product Recommender  
- Suggesting products to customers based on preferences like color, type, and brand.  
- Potential future integration with e-commerce APIs (Amazon, Noon) to expand product options.  

### F. Dashboard  
- Visual display of sales, profits, best-selling products, and client performance.  
- Interactive charts with time filters (daily, weekly, monthly).  
- Smart alerts system (low stock, overdue invoices, low profits).  

### G. Authentication and Role Management  
- Secure login using JWT tokens.  
- Password hashing with bcrypt.  
- Optional OAuth2 support (Google, Microsoft).  
- Permission customization per user role.  

## 3. UI/UX Design

### A. Frontend  
- **Technologies:** React.js with TypeScript (for future-proofing), Tailwind CSS or Material UI for responsive design.  
- **Main Screens:**  
  - Login/Register page.  
  - Dashboard displaying summaries and reports.  
  - Product management (lists, add, edit, delete).  
  - Customer and supplier management.  
  - Invoice creation and management.  
  - Upload and analyze invoice images.  
  - Financial recommendations page.  
  - Account settings, roles, and white-label branding.  
- **User Experience:** Simple and clear interface with concise instructions and meaningful icons. Support for Arabic and English languages.  
- **Navigation:** Fixed sidebar with clear options for each feature.  

### B. Visual Design  
- Harmonious modern colors with light and dark mode options.  
- Readable fonts (Cairo for Arabic, Roboto for English).  
- Responsive layout supporting desktop, tablet, and mobile devices.  
- Clear alerts and notifications with interactive buttons.  

## 4. Database Design

### A. Main Tables

| Table Name      | Description                        | Key Columns                                    |
|-----------------|----------------------------------|------------------------------------------------|
| Users           | User data and types              | id, name, email, password_hash, role           |
| Roles           | User roles and permissions       | id, role_name, permissions                       |
| Products        | Product information              | id, name, category, brand, stock_qty, price, barcode |
| Customers       | Customer data                   | id, name, contact_info, address                  |
| Suppliers       | Supplier data                   | id, name, contact_info                            |
| Invoices        | Invoice data                   | id, customer_id, date, status, total_amount     |
| InvoiceItems    | Invoice details (products, qty, price) | id, invoice_id, product_id, qty, price        |
| Transactions    | Financial transactions linked to invoices | id, invoice_id, payment_date, amount         |
| OCR_Results     | Text extraction results from invoices and images | id, invoice_id, extracted_text           |
| AI_Detections   | Product detection results in images | id, invoice_id, product_id, detected_qty, confidence_score |
| Recommendations | Financial and pricing recommendations | id, product_id, suggested_price, date         |
| Logs            | User activities and operation logs | id, user_id, action, timestamp                   |

### B. Core Relationships  
- One-to-Many: Customers to Invoices  
- One-to-Many: Invoices to InvoiceItems  
- Many-to-One: InvoiceItems to Products  
- One-to-Many: Users to Logs  

## 5. System Architecture

- **Backend:** Python 3.11+ with FastAPI (async supported)  
- **Frontend:** React.js with TypeScript  
- **Database:** PostgreSQL  
- **Authentication:** JWT + bcrypt  
- **Image Processing:** OpenCV + Tesseract OCR  
- **Product Detection:** YOLOv8 (pretrained model with optional retraining)  
- **Deployment:** Docker / Docker Compose for easy installation and distribution  

## 6. Delivery and Licensing

- Self-hosted standalone version installed on client’s server.  
- License key issued per client, linked to server IP or domain.  
- Automatic installation script (Shell or Docker Compose).  
- Complete documentation including:  
  - Installation and operation guide.  
  - Feature and interface explanations.  
  - API documentation (if applicable).  

## 7. Support and Maintenance

- Regular updates (performance improvements, security patches, new features).  
- Technical support via email or ticket system.  
- Option for paid custom development or advanced support.  

## 8. Future Development Roadmap

- Multi-language and multi-currency support.  
- Mobile app development (React Native or Flutter) for invoice uploading and tracking.  
- Integration with major accounting platforms (QuickBooks, SAP).  
- Advanced AI: NLP for invoice text analysis, fraud detection, inventory forecasting.  
- Built-in chatbot for user assistance.  

## Important Notes for Developers / Technical Team

- Consider modular or microservices architecture to allow future scalability.  
- Security is a priority: password encryption, protection against XSS and SQL Injection, strict role-based access control.  
- Write automated unit and integration tests to ensure quality.  
- Use OpenAPI / Swagger for API documentation.  
- Use Redux Toolkit or similar for frontend state management and maintain clear separation between frontend and backend logic.  
