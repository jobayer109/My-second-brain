The **Account Settings** section of Shothik AI is where users manage their personal and billing information. It consists of two tabs:

- **General Tab**: Allows users to update personal details such as name, address, and profile picture.
    
- **Billing Tab**: Provides users with access to their subscription plan, invoice history, and billing-related actions.
    

This combined PRD outlines the functional, design, and user experience requirements for both tabs to ensure consistency, usability, and responsiveness across all platforms.

---

#### **2. Objectives**

- Allow users to manage and update personal and billing information easily.
    
- Maintain a consistent and accessible user experience on all devices.
    
- Provide secure data handling with validations and confirmations.
    
- Offer clear visibility of subscription plans and payment records.
    

---

#### **3. User Stories**

##### General Tab:

1. As a user, I want to upload a profile picture and update my personal details.
    
2. As an authenticated user, I expect pre-filled, validated, and restricted fields as needed.
    
3. As a mobile user, I want a responsive form layout that’s easy to navigate.
    

##### Billing Tab:

1. As a subscribed user, I want to view my current plan, upgrade options, and download invoices.
    
2. As an unauthenticated user, I want to explore available subscription plans.
    
3. As a mobile user, I want accessible billing information without excessive scrolling.
    

---

#### **4. Functional Requirements**

##### **4.1 Navigation**

- **Tabs**: Switchable between **General** and **Billing**.
    
- Highlighted tab indicates the currently selected section.
    

---

##### **4.2 General Tab**

**Profile Picture Upload**

- Circular placeholder with 📷 icon.
    
- Supported formats: `.jpeg`, `.jpg`, `.png`, `.gif`.
    
- Visual feedback for upload progress and success.
    

**Personal Information Fields**

- **Name**: Editable text field with validation.
    
- **Email**: Read-only field with green "Verified" badge.
    
- **Address, Country, City, Postal Code**: Editable fields with optional/required settings and validations.
    

**Save Changes Button**

- Validates input before submitting.
    
- Displays success/failure messages.
    
- Shows inline validation errors for invalid fields.
    

---

##### **4.3 Billing Tab**

**Current Plan Information**

- Displays active plan details (e.g., Pro Plan).
    
- Includes "Upgrade Plan" button with diamond icon.
    
- Plan description to encourage upgrades.
    

**Invoice History**

- Table format listing:
    
    - Plan Name, Payment Date, Expiration Date, Amount, Status, and Download option.
        
- Color-coded status badges (e.g., green for "Active").
    
- Downloadable PDF invoices.
    

---

#### **5. Design Specifications**

##### **Layout**

- **Desktop**: Two-column layout for both tabs.
    
    - General Tab: Left – Profile picture, Right – Personal info form.
        
    - Billing Tab: Left – Current Plan, Right – Invoice History.
        
- **Mobile**: Stacked vertical layout.
    

##### **Interaction & Feedback**

- Hover and active states for buttons.
    
- Real-time validation with inline messages.
    
- Toast notifications for success actions.
    
- Smooth animations for visual feedback.
    

##### **Accessibility**

- High contrast text/background.
    
- Alt text for all images/icons.
    
- Keyboard navigability.
    

---

#### **6. Key Features**

1. **Profile Picture Upload** with file validations and live preview.
    
2. **Editable Personal Info** form with real-time validation.
    
3. **Read-only Verified Email** field.
    
4. **Current Plan Display** with upgrade call-to-action.
    
5. **Invoice Table with Download Links** and payment statuses.
    
6. **Fully Responsive Design** for mobile and desktop.
    
7. **Accessibility Compliant UI** across both tabs.
    
