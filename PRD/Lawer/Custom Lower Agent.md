# 📄 Product Requirements Document (PRD)

---

## 1. **Project Name:**

**Automated Data Scraper & Reporting System for Custom Lower Agent**

---

## 2. **Overview:**

This system will automatically scrape specific legal or documentation-related websites daily, extract and store structured data, generate formatted reports, and optionally display the collected data in a frontend dashboard.

The system will consist of:

- **Backend**: Scraping, data storage, API development, report generation, and notification.
    
- **Frontend**: Dashboard to view, download, and manage scraped data.
    

---

## 3. **Goals:**

- Automate data collection from multiple external websites.
    
- Store collected data securely.
    
- Allow users to view and search scraped data via a dashboard.
    
- Enable downloadable reports (Excel/PDF).
    
- Schedule daily scraping automatically.

---

## 4. **Scope:**

### 4.1 Backend (Node.js + Express + MongoDB):

- Scrape websites (static and dynamic) daily.
    
- Store raw and processed data in MongoDB.
    
- Provide REST APIs for frontend data access.
    
- Generate reports in Excel and PDF format.
    
- Error handling and logging system.
    

### 4.2 Frontend (React.js):

- Admin login and authentication.
    
- Dashboard to view scraped data (list, table, filters).
    
- Download reports manually (Excel/PDF).
    
- View daily/weekly/monthly scraping summaries.
    
- Manual trigger for re-scraping (optional).
    
- Notification for scraping status (success/failure).
    

---

## 5. **Tech Stack:**

| Part               | Technology                    |
| ------------------ | ----------------------------- |
| Frontend           | React.js, TailwindCSS, Axios  |
| Backend            | Node.js, Express.js           |
| Database           | MongoDB (mongoose ORM)        |
| Scraping Libraries | Puppeteer, Cheerio, Axios     |
| Scheduler          | Node-cron                     |
| Report Generation  | exceljs (Excel), pdfkit (PDF) |


---

## 6. **Functional Requirements:**

### 6.1 Backend

| ID    | Feature            | Description                                           |
| ----- | ------------------ | ----------------------------------------------------- |
| BE-01 | Scraping Engine    | Scrape specific websites based on schedule (cron job) |
| BE-02 | Data Storage       | Save raw and processed data in MongoDB                |
| BE-03 | REST APIs          | Provide GET APIs to fetch scraped data                |
| BE-04 | Report Generator   | Create daily Excel and PDF reports                    |
| BE-06 | Error Logging      | Maintain error logs during scraping                   |

---

### 6.2 Frontend

|ID|Feature|Description|
|---|---|---|
|FE-01|Authentication|Secure admin login system|
|FE-02|Dashboard Home|Overview of latest scraped data|
|FE-03|Data List View|Table of scraped data with filters and search|
|FE-04|Download Reports|Download Excel or PDF reports manually|
|FE-05|Scraping Status|Display daily scraping success/failure logs|
|FE-06|Manual Re-Scrape|(Optional) Admin can trigger re-scraping manually|

---

## 7. **Non-Functional Requirements:**

- Backend APIs must have proper authentication (JWT/Session).
    
- Daily scraping must run automatically without manual intervention.
    
- Frontend must be mobile-responsive.
    
- System should be able to handle 1000+ new records per day easily.
    
- Code must be modular, scalable, and properly documented.
    

---

## 8. **Data Flow Diagram (Simple)**
`(1) node-cron Scheduler → (2) Scraper → (3) MongoDB Storage → (4) Report Generator ↘  (5) Express API → (6) React Dashboard (View/Download)`

---

## 9. **APIs List (Sample):**

|Method|Route|Description|
|---|---|---|
|GET|/api/data|Fetch all scraped data|
|GET|/api/data/:id|Fetch single record details|
|POST|/api/auth/login|Admin login|
|GET|/api/reports/daily|Download today's report|
|POST|/api/scrape/manual|(Optional) Trigger manual scraping|

---

## 10. **UI/UX Plan (Simple Wireframe Idea):**

- **Login Page**
    
- **Dashboard Home** (Total records today, Last scrape time, Summary)
    
- **Data Table** (Filters: Date, Keyword search)
    
- **Download Buttons** (Excel/PDF)
    
- **Notification Toasts** (Success/Error)
    

---

## 12. **Risks & Mitigation:**

- **Website structure change** → Use dynamic scraping tool (`puppeteer`) for resilience.
    
- **IP blocking** → Use rate limiting and proxy rotation if needed.
    
- **Data inconsistency** → Validation and schema checks before saving.