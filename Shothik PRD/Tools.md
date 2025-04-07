## 1. Paraphrase
**Objective:** Rewrite text with different tone, sentence structure, and improved readability.

### **Layout Breakdown**

The interface is split into **three main sections**:

####  **Top Bar (Global Options)**

- **Language Switcher** (Top-left):
    
    - Allows switching between English, Bangla, or more languages using the dropdown. English will be selected by default. 
        
- **Tone/Modes Tab** (Below Language Switcher):
    
    - Includes various rephrasing tones:
        - ✅ Free: **Standard**, **Fluency**
        - 🔒 Premium: **Formal**, **Academic**, **News**, **Simple**, **Creative**, **Short**, **Long**
            
    - **Locked icons:** indicate that an upgrade is needed. Free users cannot use the locked modes but can still view them and when user click on locked modes then show a tiny upgrade modal.
        
- **Paraphrasing Strength Slider (Top-right)**
    - There are 4 steps: Basic, Intermediate, Advanced, and Expert. When the user selects a specific strength using the slider, the output will display the corresponding response.
        

---

####  **Main Panels**

##### Left Panel – **Input Field**

- Users can:
    
    - Type or paste text or try with sample text.
        
    - Upload `.pdf`  and `.docx` files
        
- Features:
    
    - Word counter (bottom-left, e.g., **39 / 180**)
        
    - Trash icon to clear the input
        
    - **“Paraphrase”** button to process the text
	    
	- If there is text in the output, it will show **"Rephrase"** button instead of **"Paraphrase"** conditionally. 
	
	-  When a user pastes any text into the input field, the system will use Natural Language Understanding (NLU) to detect the type of content (e.g., Medical, Technical, Legal, etc.). Based on the detected content type, the system will paraphrase the text while maintaining proper indentation and formatting to preserve the original content structure and theme.

	- The system should detect and handle content duplication to ensure the generated paraphrased output is original and unique.

	- When users paste content with multiple paragraphs into the input section, the system must maintain the original paragraph gaps and line breaks.
    
	- Currently, multiple paragraphs merge into a single paragraph—this should be fixed to retain proper formatting.
        
- 🔒 **Freeze Word Functionality**:
    
    - When a word (like **“passed”**) is selected, a **“Please upgrade to Freeze”** tooltip appears
        
    - Only **premium users** can freeze selected words to **prevent them from being changed** during rephrasing
        

---
**Left and right side will be divided by a line.**
-  A movable divider will be placed between the input and output sections. Users will be able to drag this divider left or right to resize the input and output areas as needed. At the top of the divider, there will be a swiper icon that allows users to transfer selected paragraphs from the output section to the input section with a single click.
  
#####  Right Panel – **Output Field**

- Shows the paraphrased version after clicking **“Paraphrase”**
    
- Features include:
    
    - Highlighted words to show changed parts
        
    - Edited output is fully **interactive and editable**
        
    -   After generating the initial output, **user** can:

	- Select any part of the text
	    
	- Get **paraphrased alternatives** of that sentence or phrase
	    
	- See **synonym suggestions** for specific words

	- Replace the existing sentence/word with the chosen alternative by clicking or tapping
	
	-  In the paraphrased output, clicking on a 2–3 word phrase will show synonym suggestions. Below the suggestions, a “Break” action button will be displayed. If the user clicks “Break,” the phrase will be broken down into individual words, and the phrase behavior will be removed.
       

---

 **Bottom Controls (Output Panel)**

- 1/3 – Shows the **current sentence suggestion number**
    
- Arrows – To **navigate** between sentence options
    
- Word counter – Show the word number of output
    
- Download – Exports result (e.g., `.docx`)
    
- Copy – Copies output to clipboard
    
- Delete – Clears the output panel
    
---


## 2. Humanize

**Objective:** Convert AI-generated or robotic-sounding content into human-like, emotional, and natural writing.

### **Layout Overview** 

#### **Top Section**
- **Language Selector:** English, Bangla, All (dropdown)
    
- **AI Model Tabs:**
    
    - `Panda` (selected by default for free users)
        
    - `Raven` (locked with upgrade tooltip)
        
- **Paraphrasing Strength Slider** (Top-right corner):
    - There are 4 steps: Basic, Intermediate, Advanced, and Expert. When the user selects a specific strength using the slider, the output will display the corresponding response.
        

---

#### **Main Input Area**

- Placeholder: “Enter your text here…”
    
- Three buttons for input methods:
    
    -  **Try Sample Text**
        
    -  **Paste Text**
        
    -  **Upload Document** (supports `.pdf`, `.docx`)
        

##### **Word Limit Indicator (Bottom-right):**
- Displays:
    
    - `Word Count` (e.g., 100 / 300 words)
        
    - `Character Count`
        
    - `Sentence Count`
        
    - **Remaining Word Limit Progress Bar**
        

---

##### **Humanizing & AI Detection Area**

##### **Behavior of the buttons after providing input**

- **Check AI** (disabled at first, activated post-Humanize)
    
- **Humanize** (green button – primary CTA)
    
- **Re-Humanize** (visible after first generation)
    

##### **Humanized Content Output Area:**

- Appears below after processing
    
- Multiple draft versions visible (e.g., Draft 1 of 2)
    
- **Score Display**:
    
    - Via **Shothik AI Detector**
        
    - Shown as:
        
        - Horizontal progress bar
            
        - Circular percentage badge (e.g., 99%)
            

---
##### **Output Tools**
-  Download 
-  Copy
-  Previous/Next (for switching drafts)
    
---
#### **User Flow**
1. **User Lands on Page**  
    → Empty input field with model selector & paste/upload buttons
    
2. **User Inputs Content**  
    → Text typed/pasted or document uploaded (max 300 words)
    
3. **User Clicks "Humanize"**  
    → Processing begins
    
4. **Tool Generates Output**  
    → Draft appears below with:
    
    - Humanized content
        
    - Score from AI detector
        
    - Re-Humanize, Copy, Download, Draft navigation
        
5. **User Clicks “Check AI”**  
    → Shothik AI Detector shows human-likeness score
    
6. **User Reviews & Compares Drafts**  
    → Switch between versions and finalize preferred output
    
7. **User Downloads or Copies Output**  
    → Result exported
    
8. **User Hits Locked Feature**  
    → Prompt appears to **Upgrade**
    
---

## 3. AI Detector

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


## 4. Translator

**Objective:** Translate text between supported languages while preserving tone and structure.

Layout Structure

The Translator tool UI is split into **two main panels**:

| Panel           | Purpose                                                |
| --------------- | ------------------------------------------------------ |
| **Left Panel**  | Input: Enter text or upload documents                  |
| **Right Panel** | Output: View, regenerate, and humanize the translation |
|                 |                                                        |
|                 |                                                        |

#### Left panel – Input section
**Function:**
This panel allows users to provide content to be translated.

**UI Elements:**

| Element                      | Description                                                          |
| ---------------------------- | -------------------------------------------------------------------- |
| **Input Text Area**          | Large text box with placeholder: _“Input your text here…”_           |
| **Word Counter**             | Displays live word usage (e.g., `39 / 250`)                          |
| **Clear Button**             | Trash icon to remove all text                                        |
| **Upload Document**          | Upload `.pdf` or `.docx`; extracts text into the input box           |
| **Paste Text Button**        | Quickly paste copied content                                         |
| **Try Sample Text**          | Inserts sample content for testing                                   |
| **Source Language Dropdown** | Default is “Auto Detect”, but users can manually select any language |
|  **Swap Language Button**    | Switches source and target languages with one click                  |

 **Notes:**

- Supports **up to 250 words**
    
- Shows word count live
    
- Handles both manual typing and file-based input
    
- Ensures flexible user control before translation
    

---

#### Right panel - Output section

**Function:**

This panel displays the translated result and provides enhancement tools.

**UI Elements:**

| Element                  | Description                                                        |
| ------------------------ | ------------------------------------------------------------------ |
| **Translated Text Area** | Displays translation side-by-side with input                       |
| **Placeholder**          | _“Translated text”_ before translation begins                      |
| **Status Text**          | Shows _“Analyzing…”_ during processing                             |
| **Translate Button**     | Starts the translation process (activated when text is entered)    |
| **Regenerate Button**    | Rewrites the translation in a different tone/structure             |
| **Humanize Button**      | Makes translation sound more natural, emotional, and user-friendly |
| **Copy Button**          | Copies final translation to clipboard                              |
|  **Download Button**     | Downloads translated result as `.txt` or `.docx`                   |

#####  Notes:
- Humanize and Regenerate only appear **after** translation is completed
    
- Output is **editable**, so users can make manual changes before copying or downloading
    

---

## 5. Grammar Fix

**Objective:** Identify and fix grammar, spelling, and punctuation errors.

###  Layout Overview

The UI is divided into two main sections:

| Panel            | Role                           |
| ---------------- | ------------------------------ |
| **Left Panel**   | Input and error detection area |
|  **Right Panel** | Output with corrected version  |

---

###  Left panel – Input Section

**Function:**

Allows users to input or upload text. The system detects and highlights grammar/spelling errors.

**UI Components:**

| Element                 | Description                                                       |
| ----------------------- | ----------------------------------------------------------------- |
| **Text Editor**         | Editable field where users can type or paste content              |
| **Placeholder**         | “Input your text here…” shown when field is empty                 |
| **Try Sample Text**     | Fills the editor with example content                             |
| **Paste Text**          | Allows one-click pasting from clipboard                           |
| **Upload Document**     | Accepts `.pdf` or `.docx` uploads                                 |
| **Word Counter**        | e.g., `43 / 250` shows live word usage                            |
| **Clear Icon**          | Deletes all input                                                 |
| **Error Count Display** | Shows total detected errors (e.g., `Errors: 2`)                   |
| **Error Highlights**    | Red-underlined or boxed error words (e.g., `performanc`, `peopl`) |
|  **Language Switcher**  | Toggles between `English`, `Bangla`, or `All` (top-left)          |

---

###  Right panel – Output Section

**Function:**

Displays corrected version of the user’s input with all grammatical and spelling issues resolved.

**UI Components:**

| Element                  | Description                                         |
| ------------------------ | --------------------------------------------------- |
| **Corrected Output Box** | Displays grammar-fixed version side-by-side         |
| **Fix Grammar Button**   | Triggers grammar correction                         |
| **Analyzing State**      | Temporarily displays “Analyzing…” during processing |
| **Updated Error Status** | “Errors: 0” after successful fix                    |
| **Copy Icon**            | One-click copy to clipboard                         |
|  **Download Icon**       | Exports final output as `.txt` or `.docx`           |

---

### User Flow (Step-by-Step)

**Step 1:  Select Language**

- User selects a language from top-left:
    
    - English (default)
        
    - Bangla
        
    - All (for auto-detection/mixed input)
        

---

**Step 2: Input Text**

- User can:
    
    - Type directly into the left panel
        
    - Click **Try Sample Text**
        
    - Click **Paste Text**
        
    - Click **Upload Document** (supports `.pdf`, `.docx`)
        

---

**Step 3: Real-Time Error Detection**

- System detects errors as user types or uploads:
    
    - Highlights issues with red underlines or boxes
        
    - Displays **live error count**
        
    - Words like `performanc` or `peopl` appear in red
        

---

**Step 4:  Fix Grammar**

- User clicks **Fix Grammar**
    
- System shows “Analyzing…” while processing
    
- Corrected version appears in the **Right Panel**
    
- Error count resets to **0**
    

---

**Step 5:  Post-Correction Actions**

- User can:
    
    -  Copy the corrected output
        
    -  Download the result
        
    -  Manually edit the corrected text if needed
        


## 6. Summarize

**Objective:** Generate concise summaries from long content to improve readability and save time.

### Layout Overview

The interface is divided into **two main panels**:

| Panel        | Role                         |
| ------------ | ---------------------------- |
| Left Panel   | User Input and File Upload   |
|  Right Panel | Summarized Output and Export |

---

####  Left panel – **Input Section**

**Function:**

Allows users to provide content for summarization.

**Components & Features:**

| Element                              | Description                                                       |
| ------------------------------------ |:----------------------------------------------------------------- |
| **Input Text Box**                   | Editable text area with placeholder: _“Input your text here…”_    |
| **Paste Text Button**                | One-click option to paste clipboard content                       |
| **Try Sample Text**                  | Autofills demo text for testing                                   |
| **Upload Document**                  | Accepts `.pdf`, `.docx` formats and extracts content to input box |
| **Word Counter**                     | Shows live input size (e.g., `39 / 500`)                          |
| **Trash Icon**                       | Clears all entered content                                        |
| **Summary Format Toggle (Top-left)** | Two options:                                                      |

- `Key Sentences` – Bullet-point summary
    
- `Paragraph` – Written summary in paragraph form | | 📏 **Summary Length Slider (Top-right)** | Adjustable levels:
    
- Short
    
- Regular
    
- Medium
    
- Long |
    



---

#### Right panel – **Output Section**

**Function:**

Displays the generated summary after processing.

**Components & Features:**

| Element                 | Description                             |
| ----------------------- | --------------------------------------- |
| **Summarized Text Box** | Output panel titled “Summarized text”   |
| **Summarize Button**    | Primary CTA; triggers summarization     |
| **Status Feedback**     | Displays “Analyzing…” during processing |
|  **Formatted Output**   | Output styled based on format selected: |

- Bullet points for `Key Sentences`
    
- Full paragraph for `Paragraph` | |  **Sentence Count Indicator** | Shown below output (e.g., “3 Sentence”) | |  **Copy Icon** | Copies summary to clipboard | |  **Download Icon** | Exports summary as `.txt` or `.pdf` |
    

---

**User Flow (Step-by-Step)**

1. **Text Input**

- User types or pastes content into the left panel
    
- OR uploads a `.pdf` or `.docx` file
    

---

2. **Choose Summary Format**

- User selects either:
    
    - **Key Sentences**: Extracts top sentences
        
    - **Paragraph**: Generates a coherent paragraph summary
        

---

3. **Set Summary Length**

- User adjusts **Length Slider** (Top-right):
    
    - Short → Long
        
    - Affects how much content is included in the summary
        

---

4. **Generate Summary**

- Clicks **Summarize**
    
- Tool processes the input and displays result in the right panel
    

---

 5. **Export or Copy**

- User may:
    
    -  Copy summary text
        
    -  Download summary file
        
    - See number of sentences generated (e.g., “3 Sentence”)
        

       
