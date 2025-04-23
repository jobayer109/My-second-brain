### 🧠 Step 1: Update Memory Bank (activeContext & progress)

**Instruction to CLINE:**

```
🧠 Please update the internal memory bank to track the following:
- activeContext: Maintain which PDF file is currently being previewed.
- progress: Track user interaction stages like "initial_preview", "highlighted", "action_triggered", etc.

Ensure these values are globally accessible within Doclyze state management so we can coordinate AI responses, highlights, and chat actions more precisely.
```

---

### 🐛 Issue 1: AI Response Flickering on File Preview

**Instruction to CLINE:**

```
🛠️ Problem:
When a PDF file is previewed for the first time, an auto AI response is streamed. But it doesn't appear smoothly—it flickers or delays due to multiple re-renders or retries.

✅ Goal:
Ensure the **initial AI response** is shown **smoothly and instantly** after file upload, without flickering or multiple retries.

🔧 Steps:
1. Investigate how the AI response is being fetched and rendered—likely through useEffect or stream callback.
2. Ensure that the response state is not resetting/retriggering due to component re-renders.
3. Apply memoization or conditional flags to prevent multiple stream retries for the same file.
4. Add a loading skeleton or shimmer only once before the response arrives. Once streamed, keep it rendered.

🧪 Test Case:
Upload a file → preview opens → AI response appears **once**, smoothly → suggestion buttons show correctly underneath.
```

---

### 🐛 Issue 2: Duplicate Messages from `TextSelectionMenu`

**Instruction to CLINE:**

```
🛠️ Problem:
When clicking an action from the `TextSelectionMenu`, the same message is sent twice to the ChatPanel, resulting in **duplicate response blocks**.

✅ Goal:
Ensure that a **single action click** triggers only **one message** and **one response**.

🔧 Steps:
1. Trace the onClick handler inside `TextSelectionMenu` actions.
2. Check if there's a double trigger from both parent and child components or a repeated dispatch.
3. Add safeguards (debounce, `isSending` flag) to ensure only one dispatch happens per interaction.
4. Ensure that response appending in the chat panel is tied to unique message IDs or timestamps to avoid duplication.

🧪 Test Case:
Select text → click any action → see **only one** message + one response.
```

---

### 🎨 Issue 3: Highlight Colors Not Applying or Persisting

**Instruction to CLINE:**

```
🛠️ Problem:
1. Highlight colors from `TextSelectionMenu` are **not applied** to selected text.
2. If a user visits another file and returns, previously highlighted text is **not shown**.

✅ Goal:
Make highlight functional and **persistent per file**.

🔧 Steps:
1. Ensure selected color gets applied to the actual text layer of the PDF viewer using annotations or overlay.
2. Store the highlight data (text + coordinates + color) in a per-file context or database (temp memory if needed for now).
3. When a file is reopened, fetch and render all associated highlights properly.
4. Handle color styles using either inline spans or viewer-layer rendering depending on react-pdf v9 constraints.

🧪 Test Case:
Highlight a sentence → change file → come back → highlight should still be visible with the correct color.
```
