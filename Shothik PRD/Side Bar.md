### **Product Requirements Document (PRD): side bar**

#### **1. Introduction**

The sidebar in Shothik AI includes two modes: **Mini Mode** and **Expanded Mode**, catering to different user needs and device sizes. These modes ensure that users can efficiently navigate the application while maintaining a clean, responsive, and visually appealing design.

- **Mini Mode:** A compact version of the sidebar that focuses on essential services and conserves screen space.
- **Expanded Mode:** A detailed version of the sidebar that provides access to all services, account information, and subscription details.

On **mobile devices**, only expanded mode is implemented as a **drawer** that slides in and out of view, ensuring usability on smaller screens.

#### **2. Objectives**

- Provide easy access to core services via click interactions.
- Hide non-essential sections (e.g., account details) in mini mode to conserve space.
- Display all features and personalized information in expanded mode for comprehensive navigation.
- Ensure seamless interaction and accessibility across devices.
- Implement a drawer-style interface for mobile devices to toggle between mini and expanded modes.

#### **3. User Stories**

1. **As a user on any device, I want to access core services quickly without clutter.**
   - The sidebar should display all core services in a compact format (mini mode) while allowing access to expanded details when needed.
1. **As an authenticated user, I expect my subscription plan to be visible even in mini mode.**
   - The sidebar should prominently display the user's current subscription plan (e.g., "Pro Plan") in a dedicated area.
1. **As an unauthenticated user, I want to see options to log in or sign up.**
   - While the account section is hidden in mini mode, the sidebar should still encourage users to log in or sign up by providing clear CTAs.
1. **As a user, I expect the sidebar to adapt seamlessly to different screen sizes.**
   - The sidebar should toggle between mini mode and expanded mode based on device size or user preference.
1. **As a mobile user, I want a quick way to access the full sidebar menu.**
   - On mobile devices, provide a button to open the expanded sidebar (drawer), revealing all services, account information, and subscription details.

#### **4. Functional Requirements**

##### **4.1 Core Services Menu**

- **Services List:**
  - Paraphrase
  - Humanize GPT
  - AI Detector
  - Grammar Fix
  - Summarize
  - Translator
  - Research
- **Icons:**
  - Each service should have a unique icon to enhance visual recognition.
- **Navigation:**
  - Clicking on any service should redirect the user to the corresponding feature page.
  - The sidebar should dynamically highlight the currently active service (e.g., using a background color or border).
  
##### **4.2 Account Section**

- **In Mini Mode:**  
  The account section is **hidden** to conserve space. Instead, the sidebar focuses on:
  - Displaying the user's subscription plan (e.g., "Pro Plan") in a dedicated area at the bottom.
  - Providing a prominent button for upgrading plans if the user is on a free or limited plan.

- **In Expanded Mode:**
  - The account section is fully visible, showing:
    - User's avatar and name.
    - Current subscription plan (e.g., "Pro Plan").
    - Buttons for managing the account (e.g., "Upgrade Plan," "Logout").

##### **4.3 Subscription Status**

- **Plan Display:**
  - In mini mode, only the **plan name** is displayed (e.g., "Free Plan," "Pro Plan").
  - No additional icons or colors are used to differentiate plans in this mode.
- **Upgrade Option:**
  - For users on free or limited plans, display a prominent button labeled "Upgrade Plan."
  - For users on paid plans, display a button labeled "Manage Subscription" or similar.
##### **4.4 Responsive Design**

- **Toggle Between Mini Mode and Expanded Mode:**
  - **Mini Mode:** 
    - Compact sidebar with icons and text labels.
    - Services are accessible via click.
    - Account section is hidden.
  - **Expanded Mode:**
    - Full-width sidebar with icons and text labels.
    - Displays all services and account information.
    - Provides detailed subscription status and CTAs.
  - **Toggle Button (Mobile Drawer):**
    - On mobile devices, a button (e.g., hamburger menu or arrow icon) is placed prominently to open the expanded sidebar (drawer).
    - When clicked, the sidebar slides out from the side, overlaying the main content temporarily.
    - The drawer can be closed by clicking outside the sidebar or using a close button.

#### **5. Design Specifications**

##### **5.1 Layout**
- **Sidebar Width:**
  - **Mini Mode:** Fixed width of **64px**.
  - **Expanded Mode:** Fixed width of **280px**.
- **Services Section:**
  - Displays all core services vertically with icons aligned to the left.
  - Active service is highlighted with a distinct background color or border.
- **Account Section:**
  - Positioned at the bottom of the sidebar in expanded mode.
  - Includes:
    - User avatar and name.
    - Subscription plan indicator.
    - Buttons for upgrading or logging out.

##### **5.4 Interactions**
- Hover State:
  - Services: Light background color change on hover.
  - Buttons: Slight shadow effect on hover.
- Active State:
  - Currently selected service: Highlighted with a distinct background color (e.g., light green).
  - Buttons: Pressed state with reduced opacity or shadow effect.

#### **6. Conclusion**

The sidebar in Shothik AI is designed to adapt seamlessly to different screen sizes and device types by offering two modes: **mini mode** and **expanded mode**. On mobile devices, the sidebar operates as a drawer, ensuring users can easily access the full menu when needed. This PRD outlines the functional and design requirements necessary to build and maintain this critical feature.

