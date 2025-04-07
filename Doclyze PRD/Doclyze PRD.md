#  Product Requirements Document (PRD)

###  Product Name

**Doclyze**  
_"Chat with your documents — extract knowledge instantly."_

---

## Objective

Doclyze AI is a web application that enables users to upload documents (PDFs, DOCX, PPTX, scanned image files, etc.) and interact with them via a conversational AI. The AI reads, understands, and responds to user queries with contextual relevance, summaries, citations, and highlights from the documents.

---

## Target Users

- Students and researchers
    
- Legal professionals
    
- Business analysts
    
- Journalists and content reviewers
    
- Anyone working with large documents or needing document insight quickly
    

---

## Key Features (MVP)

### 1. Document Upload & Management

- Upload formats: `.pdf`, `.docx`, `.pptx`, `.txt`, and scanned image-based PDFs.
    
- Upload from:
    
    - Local device
        
    - Document URL (e.g. link to a public PDF)
        
- File limits:
    
    - **Free users**: Up to 10MB / 120 pages
        
    - **Pro users**: Up to 32MB / 2000 pages
        
- OCR support for scanned/image PDFs
    
- Document list and folders for organization
    

### 2. AI Chat with Documents

- Ask any question about the uploaded document
    
- Summarize whole or part of the document
    
- Extract key information, data points, or decisions
    
- Multi-turn conversational memory per document
    
- Answer with citations (page/section references)
    
- Chat continues with new uploaded documents
    

### 3. In-App Document Viewer

- Display uploaded file (side-by-side with chat)
    
- Highlight referenced content from AI responses
    
- Scroll to referenced section when clicked
    

### 4. Multilingual Support

- Document language detection
    
- Questions and answers can be in multiple languages
    
- Translate content on request
    

### 5. Authentication & User Management

- Signup/login via email/password (Supabase Auth)
    
- Session-based access to user data, chat history, and files
    
- Role-based limits (free vs pro)
    

### 6. Chat History & Export

- Each document has its own chat history
    
- Chat logs stored and retrievable per session
    
- Export chat as `.txt` or `.csv`
    

### 7. Billing & Subscription

- Free Plan:
    
    - 2 documents/day
        
    - 50 questions/day
        
- Pro Plan ($5/month):
    
    - 50 documents/day
        
    - 1000 questions/day
        
    - Priority processing & support
        

---

## Technical Stack

### Frontend

- **Framework**: Next.js (React 19 with App Router)
    
- **Styling/UI**: Tailwind CSS + ShadCN
    
- **Rich Input**: React quill editor
    
- **Real-time**: `socket.io-client`
    
- **Document Rendering**:
    
    - PDF: `pdf.js`
        
    - DOCX: `mammoth` (converted preview)
        
    - PPTX: `pptx-parser` or convert to images
        
- **Client-side OCR** (if needed): `tesseract.js` (fallback)
    

### ⚙️ Backend

- **Runtime**: Node.js with TypeScript
    
- **Framework**: Fastify or Express.js
    
- **AI Model**: OpenAI GPT-4-turbo via OpenAI Node SDK
    
- **Document Parsing**:
    
    - PDF: `pdf-parse` or `pdf2json`
        
    - DOCX: `mammoth`
        
    - PPTX: `pptx-parser`
        
    - OCR: `tesseract.js`
        
- **Database**: Supabase PostgreSQL
    
- **Storage**: Supabase Storage (or AWS S3)
    
- **Cache**: Redis (via `ioredis`)
    

---

## 📡 API Endpoints

|Endpoint|Method|Description|
|---|---|---|
|`/api/upload`|POST|Upload document and return ID|
|`/api/parse/:fileId`|POST|Parse document content|
|`/api/chat`|POST|Ask question with file ID and return response|
|`/api/history/:fileId`|GET|Get chat history|
|`/api/files`|GET|List user-uploaded documents|
|`/api/delete/:fileId`|DELETE|Delete file and history|
|`/api/folders`|POST/GET|Organize and fetch folder structure|
|`/api/upgrade-plan`|POST|Handle billing plan upgrade|

---

## 🔁 User Flow

1. **Sign Up / Login**
    
2. **Upload Document**
    
3. **AI Parses Document**
    
4. **User Asks a Question**
    
5. **AI Responds with Context & Citations**
    
6. **User Views Highlighted Answer in Viewer**
    
7. **More Chat or Upload New Files**
    
8. **History Saved, Optionally Exported**
    
9. **Free Users Prompted to Upgrade If Limits Reached**
    

---

## 🧠 Prompting Strategy (System Message for LLM)

```text
SYSTEM:
You are an expert assistant that only responds using information extracted from the user's document. Provide accurate, helpful, and concise answers. Always cite the page or section if possible. If the question is unrelated to the document, politely inform the user.

USER PROMPT:
Document Title: "{{title}}"
Document Content: "{{cleaned_text_from_doc}}"

User's Question: "{{question}}"

Instructions:
- Answer based only on the document content.
- If applicable, include page numbers.
- Do not hallucinate or guess outside the document context.
```

---

## 🔐 Security Considerations

- Only document owners can view, chat, and delete their files
    
- Supabase Auth used for login/session management
    
- Option to permanently delete all account data
    
- Encryption in transit (SSL) and at rest (Supabase/Postgres encryption)
    

---

## 📅 Milestones & Timeline

|Week|Tasks|
|---|---|
|1|Setup Next.js + Supabase + Auth|
|2|Build file upload + parsing endpoints|
|3|Integrate OpenAI API + document-based chat|
|4|Build real-time chat UI + document viewer|
|5|Implement chat history + export|
|6|Add OCR + multilingual support|
|7|Implement plans & upgrade logic|
|8|Final QA, testing, and beta release|

---

## 🧪 Stretch Goals (Post-MVP)

- Chat across multiple documents
    
- Shareable chat sessions
    
- AI-generated document summaries (executive summary)
    
- Browser extension
    
- Chatbot API for other apps (embed doc chat in your platform)
    
- Realtime collaboration (multiple users on same doc)
    

---

## 📄 Deliverables for LLM

You can now give this PRD to any LLM and say:

> "Please act as a senior full-stack engineer. Use this PRD and walk me through building this product step by step, starting with project structure and file upload. Then proceed to document parsing, AI integration, and frontend UI."

---

Would you like this in Markdown, Google Docs, or Notion format too? Or do you want the **first task breakdown** from here right now?