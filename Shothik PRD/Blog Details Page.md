This PRD outlines the requirements for the Blog Details Page on the Shothik AI platform. The purpose of this page is to present an individual blog post in a detailed and interactive format while encouraging users to engage with the content and explore more platform features.

## **2. Objectives**

- Present a single blog post with full details.
- Provide interaction options: like, dislike, share, and comments.
- Drive user engagement through CTA prompts and related content.
- Encourage platform exploration through callouts and redirections.
- Support SEO with dynamic meta tags and structured layout.  

## **3. User Stories**

### **As a reader:**
- I want to read a blog post in full detail.
- I want to like or dislike the post based on usefulness.
- I want to leave a comment and see what others have said.
- I want to share the blog on social media easily.
### **As a prospective user:**
- I want to understand Shothik AI’s offerings through helpful blog content.
- I want to explore tools and pricing if the blog seems helpful.
### **As a contributor or existing user:**
- I want to comment and interact with other readers.
- I want to promote the blog by sharing it with others.
## **4. Functional Requirements**

### **4.1 Blog Content Display**

#### **Component: Blog Body Section**
- **Elements:**
    - Title
    - Blog image (cover photo)
    - Author name and date
    - Main blog content (HTML rich text)
- **Behaviour:**
    - Dynamically rendered via SSR/CSR
    - Responsive typography and spacing
### **4.2 Interactive Footer Section (Under Blog Body)**

#### **Component: Like / Dislike + Share**
- **Icons:** 👍 Like, 👎 Dislike
- **Functionality:**
    - Users can like or dislike the blog
    - Counts are displayed
    - Stores user/IP to prevent duplicate reactions
- **Share Options:**
    - Facebook, Twitter, LinkedIn
    - Native share API (mobile)
### **4.3 Comment Section**

#### **Component: Comment Input**
- **Editor:** Rich text input (Tiptap)
- **Validation:** Minimum 5 characters
- **Permissions:** Only logged-in users can comment
#### **Component: Comment List**
- **Elements:**
    - User profile name or avatar
    - Comment content (HTML)
    - Like/Dislike per comment
    - Date of comment
- **Actions:**
    - Comment deletion (only by owner)
    - Comment like/dislike
- **Order:** Newest comments first

### **4.4 Engagement CTA Blocks**

#### **Component: Pricing Redirect Section**
- **Title:** “Thank you for being a part of the Shothik AI community.”
- **CTA Button:** “Explore the pricing”
    - Action: Redirects to `/pricing`

#### **Component: Explore More Prompt**
- **Title:** “Still Looking for an Answer?”
- **Text:** Encourages readers to continue exploring
- **CTA Button:** “Search for more help”
    - Action: Redirects to `/blogs`

## **5. Design Specifications**

### **5.1 Layout**
- **Top Area:**
    - Large title, blog image, meta info
- **Body Area:**
    - Rich text content
- **Interactive Section:**
    - Like/dislike + Share (centered or inline)
- **Comments Section:**
    - Input followed by comment list
- **CTA Sections:**
    - Full-width cards with heading, text, and CTA
## **6. Key Features**
1. **Full Blog Rendering**
2. **Blog Like / Dislike Interaction**
3. **Social Sharing Integration**
4. **Rich Commenting System**
5. **Pricing & Help Callout CTAs**