**Product Requirements Document (PRD)**

---

**Project Name:** Shothik.ai  
**Prepared By:** Jobayer Ahmed 
**Date:** 05-04-2025

---

### 1. Objective

Shothik.ai is a comprehensive AI-powered writing assistant that improves writing quality through paraphrasing, grammar fix, humanizing AI text, translation, summarization, bypassing AI detection, and content authenticity detection. It is designed for writers, students, marketers, and professionals seeking to write faster, smarter, and more naturally. The platform offers both free and premium features to cater to a wide range of users.

---

### 2. Target Users

- Content creators
    
- Students and researchers
    
- Business professionals
    
- Non-native English speakers
    
- SEO writers and bloggers
    
- Marketing and copywriting teams
    

---

### 3. Goals & Success Metrics

**Goals:**

- Reduce time spent editing and improving written content.
    
- Help users generate more natural, human-like writing.
    
- Assist non-native speakers in writing fluent English.
    

**Success Metrics:**

- > 80% returning user rate
    
- Average session duration >3 minutes
    
- <1.5 seconds tool response time
    
- 95% of users rate tools as helpful or very helpful
    

---

### 4. Core Features

### 4.1 AI Writing Editor

- Built with TipTap rich-text editor
    
- Live formatting: bold, italic, underline, lists, alignment
    
- Word count, readability stats, character tracking
    
- Supports import/export of DOCX
    
- Autosave and version history (planned)
    

### 4.2 Paraphrasing
**Objective:** Rewrite text with different tone, sentence structure, and improved readability.

**Paraphrasing Strength:** Basic, Intermediate, Advanced and Expert (position top-right)

##### Step 1: User Input

- User pastes or types text into the **Input Field**. User input can be typing, copy-paste, docx / pdf file upload.
    
- In input field text, when user block a word there's show an option **“Freeze Words”** box:
    
    - Premium users can enter specific words/phrases to **protect them from being paraphrased**.
        
    - Free users see a **locked icon** and upgrade message if they try to use it.
        

---
**Language select tab**
- At the top of the Tone/Modes tab, there is a language selection dropdown. Initially, three languages are displayed, and users can select additional languages by clicking the dropdown icon.


**Tone / Modes tab**

| Mode         | Access     |
| ------------ | ---------- |
| **Standard** | ✅ Free     |
| **Fluency**  | ✅ Free     |
| **Formal**   | 🔒 Premium |
| **Academic** | 🔒 Premium |
| **News**     | 🔒 Premium |
| **Simple**   | 🔒 Premium |
| **Creative** | 🔒 Premium |
| **Short**    | 🔒 Premium |
| **Long**     | 🔒 Premium |

> Free users can view premium modes, but clicking shows upgrade prompt.


- At the bottom of the input field, there will be a word counter of the input field, a Delete button, and a 'Paraphrase' button. If have any text in the output filed, show 'Rephrase' button except 'Paraphrase'.

---

#####  Step 3: AI Processing

- AI engine detects context, tone, grammar and language.
    
- “Freeze Words” are **skipped** during rewriting.
    
- Output is grammatically correct, contextually accurate, and meaning-preserved.
       

---

#####  Step 4: Output

- Result is displayed in an **Output Field** beside or below the input based on responsiveness.
     
-   After generating the initial output, users can:

- Select any part of the text
    
- Get **paraphrased alternatives** of that sentence or phrase
    
- See **synonym suggestions** for specific words
    
- Replace the existing sentence/word with the chosen alternative by clicking or tapping
    

######  Functional Requirements:

- Text output should be **editable**
    
- On selecting a word or sentence, show:
    
    - A **"Rephrase"** button that gives multiple sentence-level alternatives
        
    - A **"Synonyms"** option that lists related words
        
- Backend will use NLP models to generate context-aware suggestions
    
- All replacements should preserve the **meaning** and **tone**
    
- Buttons in output:
    
    -  Navigable sentence counter
	-  Word counter
	-  Delete
    -  Download
    -  Copy 

---


### 4.3 Humanize

**Objective:** Convert AI-generated or robotic-sounding content into human-like, emotional, and natural writing.

**User Flow:** Paste content → Select style → Humanize → View results & score

  **Step 1: Visit Humanize GPT Interface**

- User lands on  an editable input area.

---
 **Step 2: Choose AI Model**

- Panda is selected by default for free users.
    
- Raven model is locked unless the user upgrades.
    
- Tooltip or modal may appear encouraging users to try Raven for better quality.

---

  **Step 3: Input Text**

- The user enters text by either:
    
    - Typing directly
        
    - Pasting content (max 300 words for free version)
        
- Live indicators show:
    
    - Total word count (e.g., 100/300)
        
    - Total characters
        
    - Sentence count
        
    - Words left (300 max for free users)
        
- Clicking Humanize button and then action will start.
---

 **Step 4: Check AI Detection**

- After humanizing 'Check AI' button will active.
    
- User clicks **“Check AI”** button.
    
- Shothik AI Detector is triggered:
    
    - Shows score (e.g., “98% Human Written”)
        
    - Displays circular progress indicator and horizontal bar

- AI processes the input and:
    
    - Generates up to 2 rewritten drafts (e.g., “Draft 1 of 2”)
        
    - Displays each rewritten version below the editor
        
- Purpose: Let user decide if content needs to be rephrased.
    

---

  **Step 5: Click “Re Humanize” 

- User clicks the **“Re Humanize”** button (It will show if there any text in output).
        

---

  **Step 6: Review Rewritten Draft(s)**

- The first rewritten version (Draft 1) is shown
    
- User can:
    
    - Use **“Next”** button to view Draft 2 (if available/unlocked)
        
    - Compare rephrased versions to decide the best fit
        
- Premium gating modal appears if the user attempts to use locked features
    

---

  **Step 7: Copy or Download Final Output**

- Below each draft, there is a **“Copy”** button:
    
    - One-click copy to clipboard
        
- Download option (if enabled) to export as `.txt` or `.docx`
    

---

  **Step 8: Upgrade to Premium (If Applicable)**

- User clicks any locked button or tooltip (e.g., “Upgrade” or "Re Humanize")
    
- Shown a modal:
    
    - "Unlock advanced features and enhance your paraphrasing experience"
        
    - Call-to-action: **“Upgrade to Premium”** button
        
- Premium unlocks:
    
    - Higher word count limit
        
    - Multiple draft generations
        
    - Advanced rewriting tones (future feature)
        

---

### 4.4 AI Detector

**Objective:** Rewrite AI-generated text to achieve a 100% human score and avoid AI detectors.

**User Flow:** Paste AI text → Click “Bypass” → View rewritten content → Confirm detection score

  Step 1: Input field

- Large text box with placeholder:  
    `“Enter your text here...”`
    
- Below the box:
    
    - `Try sample` button
        
     - `Paste Text` button
        
    - `Upload Document` button (supports .pdf, .docx)
        

Step 2: Word Limit Indicator

- Progress bar below the input field:
    
    - Max: `10,000 words`
        
    - Shows how many words used/left (`e.g., 50 / 1000` or `10,000 words left`)
        

Step 3: AI Source Options (Sidebar).

- Detection support for:
    
    - ChatGPT
        
    - Claude
        
    - LLaMA
        
    - Human

	When user click on  AI Source Options, paste sample text in the input field.
        
- Language support listed:
    
    - English
        
    - French
        
    - Spanish
        
    - Option: `Request more languages`
        

 Step 4: Scan Action

- After pasting or uploading text, the user clicks the `Scan` button, which is located at the bottom-right corner of the input area.
    

Step 5: Output & Results

- Text area shows the **original content** with **highlighted sentences**:
    
    - Yellow: likely AI
        
    - Red: highly AI
        
    - Green: likely human
        
- Right Panel shows:
    
    - Circular chart: "Highly Confident – Likely AI-generated"
        
    - Probability score: `100% AI Generated`
        
    - Enhanced Sentence Detection (color scale from AI to Human)
        
    - Breakdown of:
        
        - Top sentences driving AI probability
            
        - Top sentences driving Human probability
            
- Button to `Edit` and `re-scan` if needed
    
- Option to `Share` results
    

---


### 4.5 Translator

**Objective:** Translate text between supported languages while preserving tone and structure.

**User Flow:** Input → Select source & target languages → Translate → View/copy/download

####  **Key Features & Functionality 

 **Auto Language Detection**

- Automatically detects the language of the input text.
    
- Useful when the user is unsure or doesn't select the source language.
    
- Displays the detected language before translating.
    

---

**Language Selection Dropdown**

- Users can manually select both source and target languages.
    
- Default target language is **English**.
    
- Supports all major languages (e.g., Bangla, Spanish, Hindi, French, etc.).
    
- Easy-to-use dropdown menus for language selection.
    

---

**Language Swap Option**

- One-click icon to swap source and target languages.
    
- Helpful when users want to reverse the translation direction quickly.
    

---

#### **Text Input Methods**

 **Manual Typing**

- Users can type directly into the input box.
    
- Placeholder text like “Input your text here…” guides them.
    

**Paste Text**

- A button allows users to paste copied content instantly into the input area.
    

**Try Sample Text**

- Inserts a ready-made sample text into the input field for demonstration purposes.
    

**Upload Document**

- Users can upload `.pdf` or `.docx` files.
    
- The system extracts the text and shows it in the input field.
    
- Displays word count (e.g., "39/250").
    
- Word limit per session: 250 words.
    
- Helps translate full documents without manual copying.
    

---

 **Translation Output Display**

- Translated text appears on the right side.
    
- Side-by-side layout for easy comparison with the original.
    
- Placeholder shows “Translated text” until the result appears.
    

---
#### **Post-Translation Tools**

**Translate Button**

- Triggers the translation process.
    
- Active only when there is valid input text.

 **Regenerate**

- Produces a slightly different version of the translated text.
    
- Useful for getting alternative phrasing.

**Humanize Button**

- Makes the translated text sound more natural and human-like.
    
- Especially helpful for content writing or marketing use.

**Copy to Clipboard**

- Allows users to copy the translated text with one click.
    

**Download Option**

- Enables users to download the final translation as `.txt` or `.docx`.

---

### 4.6 Grammar Fix

**Objective:** Identify and fix grammar, spelling, and punctuation errors.

#### **User Flow**
 Step 1: **Select Language**

- Toggle between `English` and `Bangla` options (top-left).
    

 Step 2: **Input Text**

Users can:

- Type manually in the left editor.
    
- Click **Try Sample Text** to auto-fill with example.
    
- Click **Paste Text** to paste from clipboard.
    
- Click **Upload Document** to upload `.pdf` or `.docx`.
    

 Step 3: **Error Detection**

- System parses the text and highlights errors.
    
- Error count shown below the text area.
    
- Misspelled words shown in red boxes (e.g., `performanc`, `peopl`).
    

 Step 4: **Grammar Correction**

- User clicks **Fix Grammar**.
    
- Right pane shows corrected output.
    
- Error count resets to `0`.
    

 Step 5: **Download / Copy Output**

- User can:
    
    - Download corrected text (icon at bottom right).
        
    - Copy corrected output to clipboard.

### 4.7 Summarize

**Objective:** Generate concise summaries from long content to improve readability and save time.

**User Flow:** Input → Select summary type → Click “Summarize” → View/download result

#### **Key Features & Functionality**

**Text Input Options**

- Manual text entry via a large text box
    
- "Paste Text" button for quick input
    
- "Try Sample Text" to auto-fill demo content
    
- Document upload support for `.pdf` and `.docx` formats
    

---

**Summary Format Options**

- **Key Sentences**: Extracts the most important sentences from the original content
    
- **Paragraph**: Generates a coherent paragraph that summarizes the main ideas
    

---

**Length Control**

- Adjustable summary length using a slider (tab position is top-right )
    - Short
    - Regular
    - Medium
    - Long

---

 **Output Display**

- Summarized text shown in a separate output panel
    
- Clean formatting based on chosen summary format
    
- Real-time display after clicking the "Summarize" button
    

---

**File Handling**

- Upload `.pdf` and `.docx` files
    
- Extract and summarize document content automatically
    

---

**Text Processing Limit**

- Input word limit shown (e.g., “39 / 500”)
    
- Prevents overflow and ensures efficient summarization
    

---

**Export & Utility Options**

- Copy summarized text to clipboard
    
- Download summary as a text or PDF file
    
- Summary sentence count (e.g., "3 Sentence") shown
       

### 4.8 Shared Utility Components (Used Across Tools)

- Retry / Try Again button
    
- Copy to clipboard
    
- Word count display
    
- Highlight changes toggle
    
- Tone selector (Friendly, Professional, etc.)
    
- Download result (DOCX, PDF)
    
- Human score / detection feedback
    

---

---



---


### 5. Payment System

#### Objective:

Enable users to subscribe to premium features through a secure, fast, and user-friendly payment experience powered by Stripe.

#### Payment Plans:

|Plan Name|Price|Features|
|---|---|---|
|Free Plan|$0/month|Limited usage of tools, word count cap, no premium tones/styles|
|Monthly Pro|$12.99/month|Unlimited access to all tools, tones, bypass mode, full-length support|
|Yearly Pro|$99/year|Same as Monthly Pro, discounted for annual billing|

#### Payment Features:

- Stripe integration for secure card processing
    
- Support for credit/debit cards, Google Pay, Apple Pay
    
- Tokenized transactions with Stripe Elements
    
- Webhooks for billing updates, success/failure, renewals, and cancellations
    
- Stripe Customer Portal integration for self-service billing management
    
- Confirmation email after payment success
    

#### User Flow:

1. User clicks “Upgrade Plan” from account or tool lock screen
    
2. Modal opens with pricing options (monthly/yearly)
    
3. User enters card info via Stripe Elements
    
4. On success, user's plan is upgraded in backend
    
5. User sees confirmation and unlocks all premium tools
    

#### Premium Access Control:

- Role-based permissioning (free, pro)
    
- Frontend checks using Redux/Context
    
- API gatekeeping for rate limits, max input size, feature availability
    

#### Additional Features (Planned):

- Coupon/discount code support
    
- Invoicing and download receipts
    
- Referral bonuses or affiliate payouts
    

---

### 6. Account Popover

#### Objective:

Provide users quick access to their profile, subscription status, account settings, and logout option via a dropdown popover menu.

#### Features:

| Element                | Description                                               |
| ---------------------- | --------------------------------------------------------- |
| User Avatar            | Shown in top-right corner (header)                        |
| Popover Trigger        | Clicking avatar shows dropdown with actions               |
| Subscription Badge     | Displays current plan (Free / Pro) beside name            |
| Account Button         | Navigates to `/account` for user info and billing         |
| Billing & Plans Button | Navigates to `/billing` or `/upgrade` for plan management |
| Logout Button          | Logs user out and clears session                          |
| Google Avatar Sync     | Shows profile photo from Google OAuth                     |

---

### 7. Technical Stack

| Tech                      | Usage                        |
| ------------------------- | ---------------------------- |
| Next.js v15               | SSR, routing, page rendering |
| React 19                  | Component-based UI           |
| MUI                       | UI components                |
| Redux Toolkit             | Global state management      |
| TipTap                    | Rich-text editing            |
| Emotion                   | CSS-in-JS styling            |
| Socket.io-client          | Real-time collaboration      |
| React Hook Form + Yup/Zod | Form handling + validation   |
| Stripe.js                 | Payment gateway              |
| jwt-decode                | Auth token management        |
| react-pdf                 | PDF generation               |
| file-saver, docx, mammoth | File handling                |
| react-oauth/google        | Google OAuth login           |


---

### 8. Pages 

|Route|Description|
|---|---|
|`/`|Marketing landing page|
|`/editor`|Main writing editor|
|`/paraphraser`|Paraphrasing tool|
|`/humanize`|AI Humanization tool|
|`/bypass`|AI Detection Bypass tool|
|`/ai-rewriter`|AI to Human Rewriter (Quick tool)|
|`/detector`|AI content detection|
|`/translate`|Language translation tool|
|`/grammar`|Grammar and spelling fixer|
|`/summarize`|Content summarizer|
|`/account`|Profile and plan details|
|`/billing`|Stripe-powered billing page|
|`/upgrade`|Plan selection and upgrade page|
|`/login`|Login via Google OAuth|

---

### 9. Non-Functional Requirements

- Performance: Tool response <1.5s, Page load <2s
    
- Security: JWT auth, Stripe tokenization
    
- Accessibility: WCAG 2.1 compliance
    
- Responsiveness: Mobile-friendly
    
- Scalability: 100,000+ MAU support
    
- Localization: Multilingual UI and translation
    

---

### 10. Integrations

- Stripe
    
- Google OAuth
    
- Socket.io (real-time collaboration)
    
- OpenAI / AI SDK (content tools)
    

---

### 11. Future Roadmap

- Chrome extension
    
- Workspace collaboration tools
    
- Voice-to-text input
    
- Grammarly-style plugin
    
- Mobile app
    
