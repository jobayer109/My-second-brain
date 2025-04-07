
This PRD outlines the requirements for the blog listing and exploration page on the Shothik AI platform. The purpose of this page is to allow users to browse blog content by category, search through the blog database, explore additional platform features, and subscribe to the newsletter.

## **2. Objectives**

- Enable users to explore blogs by category.
- Provide search functionality across all blog posts.
- Display a list of recent or relevant blogs.
- Allow users to subscribe to a newsletter.
- Promote key platform features and UX use cases through callout cards.

## **3. User Stories**

### **As a reader:**
- I want to view all blog categories in one place.
- I want to search blog content using keywords.
- I want to explore the latest or most relevant blog posts.
### **As a prospective user:**
- I want to understand the features and benefits of Shothik AI.
- I want to be informed of platform updates via newsletter.
### **As a returning visitor:**
- I want to quickly identify blog categories that interest me.
- I want a consistent layout with intuitive navigation.

## **4. Functional Requirements**

### **4.1 Sidebar Navigation (Left Side Panel)**

#### **Component: Category Filter**

- **Title:** "All Topics"
- **Elements:**
    - Category List (This will come from Database by API)
    - Highlight selected category.
    - Clicking a category filters blog results accordingly.
#### **Component: Quick Links**
- **Links:**
    - “Tutorial series —”
    - “Product tutorials —”
    - “Browse all tools →”
- **Behaviour:**
    - Redirect to respective sections or pages.
#### **Component: Feature Callout Card**
- **Title:** "Explore All Features and Enhance Your Experience with Shothik AI"
- **Content:** Short description of platform benefits.
- **CTA Button:** “Explore the features”
    - Action: Redirects to a features or tools page.

### **4.2 Blog Search Section (Top Body Area)**

#### **Component: Search Card**
- **Title:** “Search our 8,000+ development and sysadmin blogs.”
- **Input Field:**
    - Placeholder: "Search Blogs..."
    - Accompanied by a search icon (mascot included for branding).
- **Functionality:**
    - Live search suggestions or search results on enter.

### **4.3 Blog Listing (Results Section)**

#### **Component: Blog Cards Grid**
- **Layout:** 2–3 columns depending on layout width.
- **Each Blog Card Includes:**
    - **Category Tag:** e.g., “// Nothing //” or “// Development //”
    - **Title:** Blog post title
    - **Date:** e.g., “February 13, 2025”
    - **Card Style:** Rounded corners with light background
- **Behaviour:**
    - Clicking a card user redirect to the blog details page.
    - Cards are populated based on selected category or search.

### **4.4 Newsletter Subscription Section**

#### **Component: Newsletter Signup**
- **Label:** “Get our newsletter”
- **Description:** “Stay up to date by signing up for Shothik AI Infrastructure as a Newsletter.”
- **Input Field:** Email address input
- **Button:** “Submit”
    - Color: Primary color of the theme
- **Behaviour:**
    - Validate email format
    - On success: confirmation message
    - On error: user feedback (e.g., invalid email)

### **4.5 Promotional UX Cards (Bottom Callouts)**

#### **Card 1: Shothik AI for Writing Solutions**

- **Title:** “Shothik AI for Writing Solutions”
- **Content:** Describes AI writing tools and benefits.
- **CTA Button:** “View all tools”
    - Color: primary color of the theme
    - Action: Redirects to tools overview.
#### **Card 2: Explore the Features**
- **Title:** “Explore the features”
- **Content:** Highlights the range of Shothik AI tools.
- **CTA Button:** “Explore”
    - Color: primary color of the theme
    - Action: Redirects to feature detail page.

## **5. Design Specifications**

### **5.1 Layout**
- **Sidebar (Left Column):**
    - Vertical stack with categories, quick links, and feature card.
- **Main Body:**
    - Search bar at top
    - Blog cards in grid below
    - Newsletter form below blog grid
    - Two promotional cards at the bottom

## **6. Key Features**
1. **Category Filtering**
2. **Blog Search**
3. **Blog Listing Grid**
4. **Newsletter Subscription**
5. **UX and Feature Promotion Cards**