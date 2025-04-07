### **Product Requirements Document (PRD): Header and Account Menu**
  
#### **1. Introduction**
The header of Shothik AI serves as the primary navigation and branding element for the application. It provides users with quick access to core features, account management, and additional resources. The header adapts based on whether the user is logged in or logged out, ensuring a personalized experience.

This PRD outlines the functional and design requirements for the header, including:
- Branding and navigation elements.
- User authentication status handling.
- Dynamic content updates based on user actions (e.g., switching tools).
- Responsive behavior across devices.

#### **2. Objectives**
- Provide clear branding and easy access to core features.
- Display user-specific information (e.g., subscription plan, profile details) when logged in.
- Offer seamless navigation to account settings, help resources, and other utilities.
- Dynamically update the header based on the active tool or page.
- Ensure responsiveness and consistency across desktop and mobile devices.

#### **3. User Stories**
1. **As an unauthenticated user:**
   - I want to see options to log in or sign up.
   - I expect to see a prominent "Upgrade Plan" button to encourage subscription upgrades.
   - I want quick access to help resources like the Help Center and Contact Us.

1. **As an authenticated user:**
   - I expect my profile details (e.g., avatar, username) to be visible.
   - I want to see my current subscription plan and options to upgrade or manage it.
   - I need easy access to account settings, such as dark mode toggle, help resources, and logout functionality.

1. **As a user navigating tools:**
   - I expect the header to dynamically display the name of the active tool (e.g., "Paraphrase," "Grammar Fix").
   - I want consistent visibility of branding and essential navigation elements regardless of the tool I'm using.

#### **4. Functional Requirements**

##### **4.1 Branding and Navigation**

- **Navigation icon:**
  - In the mobile screen a navigation bar icon always visible right of the header.
  - when click on it the sidebar will appear from left as drawer.
- **Logo:**
  - Displays the Shothik AI logo (`SHOTHIKAI`) prominently on the left side of the header.
  - Clicking the logo should redirect users to the home/dashboard page.
- **Tool Name Display:**
  - When a user navigates to a specific tool (e.g., Paraphrase, Grammar Fix), the header dynamically updates to show the name of the active tool in the center.
  - Example: "Paraphrase," "Grammar Fix," etc.
- **Upgrade Plan Button:**
  - Always visible on the right side of the header.
  - For unauthenticated users: Label reads "Upgrade Plan."
  - For authenticated users: Label reads "Upgrade Premium."
  -  For mobile device: Label reads "Upgrade."

  
##### **4.2 Account Menu**
- **Unauthenticated Users:**
  - A circular icon with the letter "M" (placeholder for future avatars) is displayed on the far right.
  - Hovering over the icon reveals a dropdown menu with the following options:
    - **Login / Sign Up:** Redirects to the login/sign-up page.
    - **Dark Mode:** Toggle switch to enable/disable dark mode.
    - **Help Center:** Redirects to the help center page.
    - **Contact Us:** Opens a contact form or email client.
    - **Join Us on Discord:** Redirects to the Discord server link.
- **Authenticated Users:**
  - The circular icon displays the user's avatar (if available) or initials.
  - Hovering over the icon reveals a dropdown menu with the following options:
    - **My Profile:** Redirects to the user's profile page.
    - **Dark Mode:** Toggle switch to enable/disable dark mode.
    - **Help Center:** Redirects to the help center page.
    - **Contact Us:** Opens a contact form or email client.
    - **Join Us on Discord:** Redirects to the Discord server link.
    - **Log Out:** Allows the user to log out of their account.


##### **4.3 Dynamic Updates**
- **Active Tool Detection:**
  - The header dynamically updates the central text to reflect the name of the active tool (e.g., "Paraphrase," "Grammar Fix").
  - This ensures users always know which tool they are currently using.


#### **5. Design Specifications**

##### **5.1 Layout**

- **Header Width:**
  - Full-width, spanning the entire viewport.
- **Elements Alignment:**
  - **Left Side:** Logo (`SHOTHIKAI`).
  - **Center:** Active tool name (dynamic based on the current page).
  - **Right Side:**  
    - "Upgrade Plan" button.  
    - Account menu icon (circular with avatar or placeholder).


##### **5.2 Styling**
- **Typography:**
  - Tool name: Bold font style, size 18px.
  - Other text: Regular font style, size 16px.
- **Icons:**
  - Avatar icon: Circular with a placeholder letter "M" for unauthenticated users.
  - Dark mode toggle: Standard toggle switch icon.
  - Other icons (Help Center, Contact Us, Discord): Material Design icons.

##### **5.3 Interactions**
- **Hover States:**
  - Account menu icon: Slight shadow effect on hover.
  - Dropdown menu items: Background color change on hover.
- **Active States:**
  - Dark mode toggle: Highlighted when enabled.
  - Buttons: Pressed state with reduced opacity or shadow effect.
- **Transitions:**
  - Dropdown menu: Smooth slide-in/slide-out animation.
  - Tool name update: Instant update without flicker.


#### **6. Key Features**

1. **Dynamic Tool Name Display:**
   - Automatically updates the header to show the name of the active tool.
1. **User Authentication Handling:**
   - Displays different content based on whether the user is logged in or logged out.
1. **Responsive Design:**
   - Adapts to both desktop and mobile devices with collapsible menus.
1. **Account Management:**
   - Provides quick access to profile, settings, and help resources.

#### **7. Conclusion**

The header of Shothik AI is designed to provide a clean, intuitive, and responsive user experience. It dynamically adapts to the user's authentication status and active tool, ensuring that users have easy access to essential features and account information. By leveraging modern web technologies and adhering to best practices in UI/UX design, the header enhances the overall usability and engagement of the platform.

**