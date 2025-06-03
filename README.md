## Introduction

This Product Requirements Document (PRD) outlines the front-end specifications for a modern, clean, elegant, and professional Asset Management Software (AMS) user interface. The software is intended for a mid-to-large-sized enterprise with a budget exceeding INR 10 lakh. The goal is to deliver a high-quality, responsive, and intuitive front-end using **HTML**, **CSS**, **JavaScript**, **Tailwind CSS**, **AJAX**, and **jQuery** (no React or other component frameworks).

All functionality described here applies strictly to the front-end; back-end endpoints (APIs) are assumed to exist or will be developed separately. Where AJAX calls are referenced, they map to RESTful endpoints (e.g., `/api/assets`, `/api/users`, etc.). The design must accommodate efficient data flow via AJAX, dynamic DOM updates with jQuery, and consistent styling with Tailwind CSS.

## Objectives

1. **User Experience (UX):** Provide an intuitive, role-based interface for administrators, asset managers, and general employees.
2. **User Interface (UI):** Implement a visually appealing, professional design that reflects a high-value investment (> 10 lakh), leveraging clean layouts, consistent spacing, and a polished color palette.
3. **Responsiveness:** Ensure seamless functionality on desktop, tablet, and mobile browsers (minimum supported: Chrome, Firefox, Edge, Safari).
4. **Performance:** Optimize front-end asset delivery (minimized CSS/JS, lazy-loading where appropriate) to meet enterprise SLAs (page load < 2s on 4G).
5. **Accessibility & Compliance:** Follow WCAG 2.1 AA guidelines, ensuring keyboard navigation, sufficient color contrast, and screen-reader compatibility.
6. **Maintainability:** Structure code (HTML templates, CSS classes, JS modules) so that future front-end developers can extend features easily.
7. **Scalability:** Use Tailwind’s utility-first approach and modular jQuery scripts so new modules (e.g., inventory forecasting, mobile-only dashboards) can be added without refactoring core CSS/JS.

## Target Users & Roles

* **System Administrator:** Configures global settings, user roles, permission levels, and oversees system security.
* **Asset Manager:** Creates/edits/deletes assets, assigns assets to users or departments, schedules maintenance, generates reports.
* **Department Head:** Views assets assigned to their department, approves asset requests, reviews maintenance logs.
* **Employee (End User):** Requests new assets, views assigned assets and their statuses, raises maintenance tickets, acknowledges asset acceptance.

Role-based dashboards and menu items must be displayed/hidden dynamically based on the logged-in user’s permissions. All data interactions occur through AJAX calls, and login/session information is assumed to be available via a secure token or session cookie.

## Technology Stack

* **Markup:** HTML5 (semantic tags—`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`)
* **Styling:**

  * Tailwind CSS (v3.x) for utility classes, customizing a central `tailwind.config.js` for color palettes, typography, spacing scales, and breakpoints.
  * Minimal custom CSS (for very specific overrides or third-party plugin styling) placed in a separate file (`custom.css`) and minified for production.
* **Scripting:**

  * JavaScript (ES6+) for application logic.
  * jQuery (v3.x) for DOM manipulation, event handling, and AJAX.
  * AJAX (jQuery’s `$.ajax`, `$.get`, `$.post`) to communicate with back-end endpoints.
* **Icons & Graphics:**

  * Heroicons (outline/solid) or Font Awesome Pro (latest) integrated via CDN or local assets.
  * SVG-based logos and illustrations, optimized (SVGO).
* **Build Tools & Workflow:**

  * Node.js environment for Tailwind compilation (PostCSS) and asset bundling (if required, minimal bundling with Rollup or webpack).
  * Linting: ESLint (JavaScript), Stylelint (CSS).
  * Prettier for consistent formatting.
* **Testing & QA:**

  * BrowserStack (or equivalent) for cross-browser testing.
  * Lighthouse audits (performance, accessibility, best practices).

## High-Level Architecture

```
[ Browser (HTML + Tailwind CSS + jQuery) ]
      │
      │ AJAX JSON requests/responses (RESTful)
      ▼
[ Back-end API Server (assumed pre-built) ]
      │
      ▼
[ Database & Business Logic Layer ]
```

The front-end is a pure Static Single-Page Application (SPA) pattern, but built without a client-side framework. Views (HTML templates) are either rendered server-side initially or delivered as static files; dynamic content is injected via jQuery/AJAX.

## UI Design Guidelines

1. **Color Palette:**

   * **Primary Accent:** Deep Indigo (#4F46E5) and Indigo (#6366F1) for buttons, active states, and highlights.
   * **Secondary Accent:** Teal (#14B8A6) for success messages, confirmations, and secondary buttons.
   * **Neutral Tones:**

     * Gray-50 (#F9FAFB) background,
     * Gray-100 (#F3F4F6) section backgrounds,
     * Gray-300 (#D1D5DB) borders/dividers,
     * Gray-700 (#374151) primary text,
     * Gray-900 (#111827) headings.
   * **Feedback Colors:**

     * Success (#10B981)
     * Warning (#F59E0B)
     * Error (#EF4444)
     * Info (#3B82F6)

2. **Typography:**

   * **Font Family:** Inter (system-fallback: `sans-serif`).
   * **Base Font Size:** 16px (1rem).
   * **Scale:**

     * Headings: `text-3xl` (2rem) for page titles, `text-2xl` (1.5rem) for section headings, `text-xl` (1.25rem) for subheadings.
     * Body: `text-base` (1rem), `leading-relaxed` (1.625).
     * Smaller text: `text-sm` (0.875rem), `text-xs` (0.75rem).
   * **Font Weights:**

     * Headings: `font-semibold` or `font-bold`.
     * Body: `font-normal`.

3. **Spacing & Layout:**

   * Consistent 8px (0.5rem) base spacing unit (Tailwind default).
   * Sections typically have `py-8` (2rem) vertical padding, container width `max-w-7xl mx-auto px-4 sm:px-6 lg:px-8`.
   * Use Flexbox (`flex`, `justify-between`, `items-center`) and CSS Grid (`grid`, `grid-cols-3`, `gap-6`) where appropriate.
   * All forms/elements should have at least `mb-4` (1rem) spacing between form rows, `px-4 py-2` padding on inputs/buttons.

4. **Components & Styles:**

   * **Buttons:**

     * Primary: `bg-indigo-600 hover:bg-indigo-700 text-white font-medium rounded-md px-4 py-2 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2`.
     * Secondary: `bg-white border border-gray-300 text-gray-700 hover:bg-gray-50 font-medium rounded-md px-4 py-2`.
     * Disabled: `bg-gray-200 text-gray-400 cursor-not-allowed`.
   * **Forms & Inputs:**

     * Input/Textarea: `block w-full border border-gray-300 rounded-md shadow-sm px-3 py-2 placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm`.
     * Select: same as input, plus arrow-icon styling.
     * Checkboxes/Radios: `h-4 w-4 text-indigo-600 border-gray-300 rounded focus:ring-indigo-500`.
   * **Cards & Panels:**

     * Use `bg-white shadow sm:rounded-lg p-6` containers for core content areas.
     * Section headers inside cards: `text-lg font-semibold text-gray-900 mb-4`.
   * **Tables:**

     * Table wrapper: `min-w-full dividing-y divide-gray-200`.
     * Table header (`<th>`): `px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider`.
     * Table row (`<tr>`): `bg-white`, alternates: `odd:bg-gray-50`.
     * Table cell (`<td>`): `px-6 py-4 whitespace-nowrap text-sm text-gray-700`.
   * **Alerts & Notifications:**

     * Success: `bg-green-50 border-l-4 border-green-400 text-green-700 p-4`.
     * Warning: `bg-yellow-50 border-l-4 border-yellow-400 text-yellow-700 p-4`.
     * Error: `bg-red-50 border-l-4 border-red-400 text-red-700 p-4`.
     * Info: `bg-blue-50 border-l-4 border-blue-400 text-blue-700 p-4`.

5. **Icons & Illustrations:**

   * Use SVG icons with `class="h-5 w-5 text-gray-500"` or colored appropriately for interactive elements.
   * Use minimal, flat illustrations (SVG) for empty states (e.g., “No assets found”).
   * All interactive icons (e.g., trash/delete, edit, view) should have hover states: `hover:text-indigo-600 cursor-pointer`.

6. **Navigation & Layout Patterns:**

   * **Header (Global Nav):**

     * `fixed top-0 inset-x-0 bg-white shadow z-50` with `h-16` (4rem).
     * Contains: company logo (left), search bar (center), user avatar/menu & role indicator (right).
     * Use Tailwind’s `flex justify-between items-center px-6`.
   * **Side Navigation (Collapsible):**

     * Hidden on mobile (hamburger toggles slide-in drawer), visible on desktop (`w-64 bg-gray-50 h-screen fixed top-16 left-0`).
     * Menu items: `py-2 px-4 flex items-center text-gray-700 hover:bg-indigo-100 rounded-md`.
     * Active item: `bg-indigo-100 text-indigo-700 font-semibold`.
   * **Breadcrumbs & Page Header:**

     * Page header: `mt-20` (to offset fixed nav), `bg-white shadow px-6 py-4 flex justify-between items-center`.
     * Breadcrumbs: `text-sm text-gray-500` with separators (`/`) in between.
   * **Content Area:**

     * `ml-0 lg:ml-64 mt-4 mb-8 px-4 sm:px-6 lg:px-8` (responsive margin/padding).
     * All pages are structured in `<section>` blocks with clear headings and subheadings.

7. **Modal & Popover Patterns:**

   * Use Tailwind’s transition utilities (`transition ease-in-out duration-150 transform`) for fade/scale animations.
   * Backdrop: `fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity`.
   * Modal container: `inline-block align-bottom bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:max-w-lg sm:w-full`.
   * Modal header: `bg-indigo-600 px-4 py-2 flex justify-between items-center text-white`.
   * Modal body: `bg-white px-4 py-5 sm:p-6`.
   * Modal actions: `bg-gray-50 px-4 py-3 sm:px-6 flex justify-end space-x-2`.

8. **Responsive Breakpoints (Tailwind defaults):**

   * **sm:** ≥ 640px
   * **md:** ≥ 768px
   * **lg:** ≥ 1024px
   * **xl:** ≥ 1280px
   * **2xl:** ≥ 1536px

All layouts must gracefully collapse on mobile: side nav becomes an off-canvas drawer, tables become horizontally scrollable (`overflow-x-auto`), forms stack vertically, and cards span full width (`w-full`) at smaller breakpoints.

## Functional Requirements

### 1. Authentication & Authorization

* **Login Page**

  * Fields: Email, Password.
  * “Remember Me” checkbox.
  * “Forgot Password?” link.
  * On successful login, store JWT/session token in a secure, HttpOnly cookie.
  * On failure, display inline error below form (`text-red-600 text-sm mt-1`).
  * Tailwind classes for form styling, submit button styled as Primary.

* **Logout**

  * Accessible from user menu in header.
  * Clicking “Logout” triggers an AJAX POST to `/api/logout` then redirects to login page.

* **Role‐Based Menu**

  * After login, fetch user profile (`GET /api/profile`) to determine role (Admin, Asset Manager, Department Head, Employee).
  * Based on role, show/hide side nav items.

### 2. Dashboard (Landing Page After Login)

* **Summary Cards (Top Row)**

  * “Total Assets”: number card with icon (box icon).
  * “Assets In Use”: number card with icon (check-circle).
  * “Assets Under Maintenance”: number card with wrench icon.
  * “Pending Requests”: number card with clock icon.
  * Each card: `bg-white shadow rounded-lg p-6 flex items-center justify-between`. Number styled `text-3xl font-bold text-indigo-600`, label `text-sm text-gray-500`.
* **Recent Activity Feed**

  * List of 5–10 most recent asset assignments, maintenance completions, or requests with timestamp.
  * Each item: `flex items-start space-x-3` with icon, description, and relative time (`2 hours ago`).
  * “View All” link bottom, pointing to Activity page.
* **Departmental Asset Distribution (Chart Placeholder)**

  * Area reserved for a pie or bar chart (front-end placeholder `<canvas>`). Later integration with Chart.js or similar.
  * For now, display “Coming Soon” illustration or dummy data.
* **Quick Actions**

  * Buttons: “Add New Asset,” “View All Assets,” “Raise Maintenance Ticket.”
  * Use Tailwind’s button styles (Primary and Secondary).
  * Positioned at top-right of dashboard header.

### 3. Asset Management

#### 3.1 Asset Listing Page

* **Search & Filter Section** (`<div class="flex flex-col md:flex-row md:items-center md:justify-between mb-6">`)

  * **Search Input:**

    * Tailwind classes: `w-full md:w-1/3 border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500`.
    * Placeholder: “Search by Asset Name or ID…”.
    * On `keyup` (with debounce), AJAX call to `/api/assets?search=<term>`.
  * **Filter Dropdowns:**

    * Status (All, In Use, Available, Maintenance, Retired).
    * Category (Electronics, Furniture, Vehicle, Machinery, etc.).
    * Department (HR, IT, Finance, Operations).
    * Each dropdown: `w-full md:w-1/5 border border-gray-300 rounded-md px-3 py-2`.
    * On change, AJAX call to `/api/assets?status=<>&category=<>&department=<>`.
  * **“Add Asset” Button:** Right-aligned on large screens; styled Primary (`bg-indigo-600 text-white px-4 py-2 rounded-md hover:bg-indigo-700`). Opens modal (see 3.2).

* **Table of Assets** (`<div class="overflow-x-auto"> <table class="min-w-full divide-y divide-gray-200"> … </table> </div>`)

  * Columns:

    1. **Asset ID** (`text-indigo-600 font-medium cursor-pointer hover:underline`). Clicking opens Asset Detail Modal.
    2. **Asset Name** (`text-gray-700`).
    3. **Category** (`text-gray-500`).
    4. **Department** (`text-gray-500`).
    5. **Status** (Badge with Tailwind classes:

       * In Use: `bg-teal-100 text-teal-800`
       * Available: `bg-gray-100 text-gray-800`
       * Maintenance: `bg-yellow-100 text-yellow-800`
       * Retired: `bg-red-100 text-red-800`
         )
    6. **Assigned To** (`text-gray-700`, or “–” if unassigned).
    7. **Last Updated** (`text-sm text-gray-500`).
    8. **Actions**:

       * **Edit** (pencil icon, `hover:text-indigo-600`).
       * **Delete** (trash icon, `hover:text-red-600`).
       * **Assign / Unassign** (user-plus or user-minus icon).
       * All icons are SVGs wrapped in `<button>` with `aria-label`.
  * Pagination controls at bottom: “Showing 1–10 of 324”—use `flex items-center justify-between py-3`. Prev/Next page buttons styled with `border border-gray-300 text-gray-700 px-3 py-1 rounded-md hover:bg-gray-100 disabled:opacity-50`.
  * Table should support lazy loading or dynamic paging: clicking a pagination link triggers AJAX load of next page.

#### 3.2 Asset CRUD Modals

* **Add New Asset Modal** (`id="modal-add-asset"`)

  * Trigger: “Add Asset” button.

  * AJAX `GET /api/categories`, `/api/departments` to populate dropdowns.

  * Form Fields (two-column grid on desktop, one-column on mobile):

    1. Asset Name (required, `text-base`, placeholder “Dell Laptop Model X”).
    2. Asset ID (auto-generated or manual—toggle).
    3. Category (dropdown)
    4. Department (dropdown)
    5. Purchase Date (date picker)—use `<input type="date">` styled with Tailwind.
    6. Cost (number, with currency symbol prefix inside input).
    7. Warranty Expiry (date).
    8. Serial Number (text).
    9. Location (text, placeholder “Floor 5, IT Room”).
    10. Status (dropdown: Available/In Use/Maintenance/Retired; default = Available).
    11. Assigned To (conditional dropdown, disabled if status != “In Use”). On change, AJAX `/api/users?role=employee&department=<selected>`.
    12. Image Upload (optional) – display a drag-and-drop zone styled `border-2 border-dashed border-gray-300 rounded-md p-4 text-center text-gray-500`. Use AJAX to upload when file selected.
    13. Description (textarea, `rows=3`).

  * **Validation:**

    * All required fields flagged with `*`.
    * On Submit (`Save`), use jQuery to validate mandatory fields; if any missing, highlight in red (`border-red-500` + display error message below).
    * If validation passes, send AJAX `POST /api/assets` with JSON payload.
    * On success: close modal, refresh listing via AJAX. Show toast notification (`“Asset created successfully”`) at top-right corner with `bg-teal-100 text-teal-800 px-4 py-2 rounded shadow`.
    * On failure: display server-returned error messages inline.

* **Edit Asset Modal** (`id="modal-edit-asset"`)

  * Similar layout to Add, but fields pre-populated via AJAX `GET /api/assets/{id}`.
  * Status and Assigned To fields should dynamically enable/disable based on the other (as above).
  * On Submit, AJAX `PUT /api/assets/{id}`.
  * On success: close modal, refresh table row via AJAX (only update changed row data).

* **Delete Confirmation Modal**

  * Simple confirmation: “Are you sure you want to delete Asset {Asset Name} (ID: {ID})?”
  * Buttons: “Cancel” (secondary style), “Delete” (error style: `bg-red-600 text-white hover:bg-red-700`).
  * On Delete click, AJAX `DELETE /api/assets/{id}`. On success: remove row from table, show toast.

* **Asset Detail Modal**

  * Displays read-only fields: Asset Name, ID, Category, Department, Status, Assigned To, Purchase Date, Cost, Warranty Expiry, Serial Number, Location, Description, Image (if any).
  * “Edit” button in top-right corner opens Edit Modal.
  * “Close” button.

#### 3.3 Asset Assignment & Unassignment

* **Inline Assignment (from Listing)**

  * Click “Assign” icon: opens a small popover anchored to the row (`absolute bg-white shadow p-4 rounded`).
  * Popover Fields: “Assign To” (dropdown populated via AJAX `/api/users?role=employee&department=<asset.department>`), “Assign Date” (date).
  * On selection and “Confirm,” AJAX `POST /api/assets/{id}/assign` with payload `{ userId: <>, assignDate: <> }`.
  * On success: update Status badge to “In Use,” Assigned To column, show toast.
* **Unassign**

  * Click “Unassign” icon (only visible if `status == 'In Use'`). Confirmation popover: “Are you sure you want to unassign this asset?”
  * On confirm, AJAX `POST /api/assets/{id}/unassign`. Update Status to “Available,” clear Assigned To, show toast.

#### 3.4 Asset Maintenance

* **Maintenance Tab / Section** (on Asset Detail or separate page)

  * List of maintenance records (date, description, performed by, cost, status).
  * “Add Maintenance Record” button opens a modal with:

    1. Maintenance Date (date).
    2. Description (textarea).
    3. Performed By (text or dropdown to service vendors).
    4. Cost (number).
    5. Status (dropdown: Pending/Completed).
  * On Submit: AJAX `POST /api/assets/{id}/maintenance`. On success: refresh maintenance table.
  * Each record row: “Edit” and “Delete” icons; same modal for editing (`PUT /api/assets/{id}/maintenance/{recordId}`) and `DELETE` for removal.
  * Overdue maintenance alert: If `(today > lastMaintenanceDate + maintenanceInterval)` highlight with `text-red-600` icon on main Asset Listing (e.g., small wrench icon next to status).

#### 3.5 Asset Request & Approval Workflow

* **Request New Asset Page** (for Employees)

  * Form fields:

    1. Asset Name (autocomplete or free text).
    2. Justification (textarea).
    3. Department (pre-filled from profile).
    4. Desired Date of Issue (date).
    5. Category (dropdown, optional).
  * On Submit: AJAX `POST /api/asset-requests`. On success: show “Request submitted” confirmation.
* **Pending Requests Page** (for Department Heads & Asset Managers)

  * Similar table to Asset Listing, but pulls from `/api/asset-requests?status=pending&department=<user.department>`.
  * Columns: Request ID, Requested By, Asset Name, Justification (truncate to 50 chars + tooltip for full), Date Requested, Desired Issue Date, Actions (Approve, Reject).
  * **Approve Button:** Immediately triggers a modal:

    * “Assign Asset?” If available assets exist in same category, show dropdown “Select Asset to Assign” with search.
    * If no asset available, link to “Create New Asset” modal.
    * On confirm, AJAX `POST /api/asset-requests/{id}/approve` with payload `{ assetId: <> }`. Updates request status.
  * **Reject Button:** Opens a small popover: “Reason for rejection” (textarea), “Confirm Reject.” On confirm: AJAX `POST /api/asset-requests/{id}/reject`.

#### 3.6 Reporting & Exporting

* **Reports Page** (for Admins & Managers)

  * Tabs or filters at top:

    1. “Assets by Department”
    2. “Assets by Status”
    3. “Maintenance Summary”
    4. “Asset Depreciation” (if back-end supports depreciation calculations)
  * Each report:

    * Date Range Picker (`<input type="date">` for “From” and “To”), “Generate” button.
    * AJAX `GET /api/reports/{reportType}?from=<>&to=<>`.
    * Display results in a table (as defined in 3.1) plus chart placeholder below.
    * “Export to CSV” button triggers file download (`window.location = '/api/reports/{reportType}/export?from=<>…'`).
  * Example Report: Assets by Department

    * Table columns: Department, Total Assets, In Use, Available, Maintenance, Retired.
    * Chart: a bar chart (placeholder `<canvas>`) that can be wired to Chart.js later.

* **Custom Report Builder** (Optional / Advanced)

  * Drag-and-drop fields: Users select data fields (Asset Name, Category, Department, Status, Purchase Date, Cost, etc.)
  * Filter criteria builder: UI controls built via jQuery to add multiple filter conditions
  * “Run Report” button: AJAX `POST /api/reports/custom` with JSON describing fields + filters.
  * Display results in dynamic table.

### 4. User Management (Admin-Only)

* **User Listing Page**

  * Similar layout to Asset Listing (search, filter by role, department).
  * Table Columns: User ID, Name, Email, Role, Department, Status (Active/Inactive), Actions (Edit, Deactivate/Activate, Reset Password).
  * Pagination as above; AJAX calls to `/api/users`.

* **Add/Edit User Modal**

  * Fields:

    1. First Name, Last Name (required).
    2. Email (required, validated format).
    3. Role (dropdown: Admin, Asset Manager, Dept Head, Employee).
    4. Department (dropdown; required if Role != Admin).
    5. Status (Active/Inactive).
    6. Temporary Password (if creating); “Send Activation Email” checkbox (default checked).
  * On Submit:

    * Creation: AJAX `POST /api/users`.
    * Edit: AJAX `PUT /api/users/{id}`.
  * On success: update listing row (without full page reload).
  * On error: show inline form validation errors.

* **Deactivate / Activate User**

  * Click “Deactivate” icon: confirmation popover (“Are you sure?”). AJAX `POST /api/users/{id}/deactivate`. On success: update status badge to “Inactive.”
  * If “Inactive,” show “Activate” icon: AJAX `POST /api/users/{id}/activate`.

* **Reset Password**

  * Click “Reset Password” icon: opens small modal with “Send password reset email to user?” On confirm: AJAX `POST /api/users/{id}/reset-password`. Show toast.

### 5. Settings & Configuration (Admin)

* **Global Settings Page**

  * **Company Profile**

    * Company Name, Logo upload (file upload via AJAX), Address, Contact Email, Phone.
  * **Asset Categories Management**

    * Table: Category Name, Description, Actions (Edit, Delete).
    * “Add Category” button opens modal with fields: Name, Description.
    * CRUD via `/api/categories`.
  * **Departments Management**

    * Same pattern as categories.
  * **System Preferences**

    * Default Currency (dropdown),
    * Default Maintenance Interval (number + unit dropdown: days/weeks/months),
    * Notification Settings (toggle checkboxes: Email, SMS, In-App).
  * **Audit Log Access**

    * Link to a separate Audit Log Page (if back-end supports it) to view system-level changes (user logins, role changes, critical actions).

### 6. Notifications & Alerts

* **In-App Toast Notifications**

  * Position: top-right corner (`fixed top-16 right-4`).
  * Types: success (`bg-teal-100`), error (`bg-red-100`), info (`bg-blue-100`), warning (`bg-yellow-100`).
  * Auto-dismiss after 5 seconds; manual close button (`×`) to dismiss immediately.
  * Implementation: jQuery appends a `<div id="toast-container">` if not exists, then injects new `<div class="toast …">` with Tailwind styling and fade-out animation via `setTimeout`.

* **Error Handling**

  * **Global AJAX Error Handler:** using `$.ajaxSetup({ error: function(xhr) { … } })` to catch 401 (redirect to login), 403 (show “Access Denied”), 500 (show generic “Something went wrong”).
  * Inline form errors displayed below relevant field in red (`text-red-600 text-sm mt-1`).

* **Email/SMS Triggers**

  * Though actual sending is back-end’s responsibility, front-end provides toggles in Settings. If toggles changed, AJAX `PUT /api/settings/notifications`.

## Non-Functional Requirements

1. **Performance**

   * **Asset Bundle Sizes (post-build):**

     * CSS (Tailwind + custom) ≤ 150 KB (gzipped).
     * JS (jQuery + custom scripts) ≤ 100 KB (gzipped).
   * **HTTP Requests:** Minimize duplicate calls; implement caching headers where possible.
   * **Lazy Loading / Code Splitting:**

     * Load non-critical JS (e.g., reporting charts) only when user navigates to Reports page.
   * **Image Optimization:** All SVGs inline; PNG/JPEG assets pre-optimized (compressed).

2. **Accessibility (WCAG 2.1 AA)**

   * **Color Contrast:** Minimum 4.5:1 for normal text, 3:1 for large text.
   * **Keyboard Navigation:** All buttons, inputs, links, modals focusable (`tabindex="0"` where needed), focus ring visible (Tailwind: `focus:outline-none focus:ring-2 focus:ring-indigo-500`).
   * **ARIA Attributes:**

     * Modals: `role="dialog" aria-modal="true" aria-labelledby="modal-title"`.
     * Tables: `<table role="table">`, `<th scope="col">`, `<td role="cell">`.
     * Alerts: `role="alert"`.
   * **Labels & Instructions:** All form inputs must have associated `<label>` elements or `aria-label` attributes.
   * **Skip to Content Link:** A hidden “Skip to main content” link (`sr-only`) at top for screen readers.

3. **Security (Front-End)**

   * **XSS Prevention:**

     * Escape all dynamic content injected via jQuery/AJAX before inserting into DOM (e.g., use `text()` instead of `html()` when rendering user-provided strings).
   * **CSRF Protection:** Include CSRF token (if back-end requires) in all AJAX headers (`$.ajaxSetup({ headers: { 'X-CSRF-Token': token } })`).
   * **HTTPS Only:** All calls over HTTPS; enforce `Content-Security-Policy` header set by server (front-end assumes it’s present).
   * **Sensitive Data Handling:** Never expose API keys or secrets in front-end.
   * **Session Timeout:** After 30 minutes of inactivity, automatically redirect to login (via AJAX heartbeat or inactivity timer).

4. **Maintainability & Scalability**

   * **Folder Structure (suggested):**

     ```
     /assets/
       /css/
         tailwind.css       ← Tailwind output (minified)  
         custom.css         ← Custom overrides  
       /js/
         jquery.min.js  
         main.js            ← Entry point (imports modules)  
         /modules/
           auth.js          ← Login/logout logic  
           dashboard.js     ← Dashboard AJAX + UI logic  
           assets.js        ← Asset listing, CRUD, maintenance, requests  
           users.js         ← User management  
           reports.js       ← Reporting logic  
           settings.js      ← Settings page logic  
           notifications.js ← Toast & global AJAX handlers  
       /images/
         logo.svg  
         icons.svg  
     /templates/
       /partials/  
         header.html  
         sidebar.html  
         footer.html  
         modal.html        ← Base modal HTML structure  
       login.html  
       dashboard.html  
       assets.html  
       users.html  
       reports.html  
       settings.html  
     index.html           ← Server-rendered login redirect or single-page container  
     ```
   * **Naming Conventions:**

     * JavaScript functions & variables use `camelCase`.
     * CSS/Tailwind classes follow functional naming (no custom classes in HTML other than for unique IDs/overrides).
     * IDs prefixed by component (e.g., `#modal-add-asset`, `#tbl-assets`).
     * Data attributes use `data-` prefix for jQuery to select (`data-asset-id`, `data-user-role`).
   * **Code Comments & Documentation:**

     * Each JS module should begin with a header comment: filename, purpose, author, date.
     * Functions should have JSDoc-style comments for complex logic.
   * **Version Control & CI/CD:**

     * Front-end code resides in a GitHub repository with `main` and feature branches.
     * On `main` merge, automated build (Tailwind compilation, CSS/JS minification) and deployment to staging.
     * Lint checks (ESLint & Stylelint) in pre-commit hooks via Husky.

5. **Localization & Internationalization (Optional / Future)**

   * All visible text wrapped in data structures so that switching language strings is possible (e.g., `window.translations["en"].dashboard.title`).
   * No hard-coded strings directly in HTML; use placeholders or data attributes, or server-rendered templates that inject localized text.

## Page-by-Page Specification

### 1. Login Page

**URL:** `/login.html`

* Simple two-column layout on desktop: left side an illustration (`hidden md:flex w-1/2 bg-indigo-100 items-center justify-center`), right side form (`w-full md:w-1/2 px-8 py-12`).
* Form container: `max-w-md w-full bg-white shadow rounded-lg p-8`.
* Logo at top (`mb-6`).
* Title: `text-2xl font-semibold text-gray-900 mb-4`.
* Fields stacked with `mb-4`.
* “Login” button full width: `w-full bg-indigo-600 hover:bg-indigo-700 text-white py-2 rounded-lg font-medium`.
* Links: “Forgot Password?” (left under form), “Back to Home” (right).

### 2. Dashboard Page

**URL:** `/dashboard.html`

* Includes common header & sidebar (via server-side include or client-side injection).
* Main content under `<main>`:

  * **Page Title:** “Dashboard” (`text-3xl font-bold text-gray-900 mb-6`).
  * **Summary Cards Row** (flex grid, gap-6):

    ```html
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
      <!-- Card 1: Total Assets -->
      <div class="bg-white shadow rounded-lg p-6 flex items-center justify-between">
        <div>
          <p class="text-xs font-medium text-gray-500 uppercase">Total Assets</p>
          <p class="mt-1 text-3xl font-semibold text-indigo-600" id="lbl-total-assets">—</p>
        </div>
        <svg class="h-10 w-10 text-indigo-200" ...> <!-- Icon SVG --></svg>
      </div>
      <!-- Repeat for other cards -->
    </div>
    ```
  * **Recent Activity Section**:

    ```html
    <section class="bg-white shadow rounded-lg p-6 mb-8">
      <div class="flex justify-between items-center mb-4">
        <h2 class="text-xl font-semibold text-gray-900">Recent Activity</h2>
        <a href="/activity.html" class="text-sm text-indigo-600 hover:underline">View All</a>
      </div>
      <ul id="ul-recent-activity" class="space-y-3">
        <!-- Dynamically populated via AJAX -->
      </ul>
    </section>
    ```
  * **Departmental Distribution Section**:

    ```html
    <section class="bg-white shadow rounded-lg p-6">
      <h2 class="text-xl font-semibold text-gray-900 mb-4">Assets by Department</h2>
      <div class="w-full h-64 bg-gray-50 rounded-lg flex items-center justify-center">
        <p class="text-gray-400">Chart coming soon</p>
      </div>
    </section>
    ```
  * **Quick Actions**: Positioned in header area (above cards) or as a floating action button on bottom right:

    ```html
    <div class="fixed bottom-8 right-8 space-y-2">
      <button id="btn-add-asset" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-3 rounded-full shadow-lg flex items-center space-x-2">
        <svg class="h-5 w-5" ...></svg><span>Add Asset</span>
      </button>
      <button onclick="window.location='/assets.html'" class="bg-white border border-gray-300 text-gray-700 px-4 py-3 rounded-full shadow flex items-center space-x-2">
        <svg class="h-5 w-5" ...></svg><span>All Assets</span>
      </button>
    </div>
    ```

### 3. Asset Listing Page

**URL:** `/assets.html`

* **Header & Breadcrumbs:**

  ```html
  <div class="bg-white shadow px-6 py-4 flex justify-between items-center mb-6">
    <div>
      <nav class="text-sm text-gray-500" aria-label="Breadcrumb">
        <ol class="list-reset flex space-x-2">
          <li><a href="/dashboard.html" class="hover:underline">Dashboard</a></li>
          <li>/</li>
          <li class="text-gray-700">Assets</li>
        </ol>
      </nav>
      <h1 class="text-2xl font-bold text-gray-900">Asset Management</h1>
    </div>
    <button id="btn-add-asset" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-md">Add Asset</button>
  </div>
  ```
* **Search & Filter Row**:

  ```html
  <div class="flex flex-col lg:flex-row lg:items-center lg:justify-between mb-6 space-y-4 lg:space-y-0">
    <div class="flex-1 lg:mr-4">
      <input type="text" id="input-search-asset" placeholder="Search by Asset Name or ID…" class="w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500" />
    </div>
    <div class="flex flex-wrap gap-4">
      <select id="filter-status" class="w-full sm:w-48 border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
        <option value="">All Status</option>
        <option value="available">Available</option>
        <option value="in_use">In Use</option>
        <option value="maintenance">Maintenance</option>
        <option value="retired">Retired</option>
      </select>
      <select id="filter-category" class="w-full sm:w-48 border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
        <option value="">All Categories</option>
        <!-- Dynamically populated -->
      </select>
      <select id="filter-department" class="w-full sm:w-48 border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
        <option value="">All Departments</option>
        <!-- Dynamically populated -->
      </select>
    </div>
  </div>
  ```
* **Asset Table**:

  ```html
  <div class="overflow-x-auto bg-white shadow rounded-lg">
    <table class="min-w-full divide-y divide-gray-200">
      <thead class="bg-gray-50">
        <tr>
          <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Asset ID</th>
          <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Asset Name</th>
          <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Category</th>
          <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Department</th>
          <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
          <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Assigned To</th>
          <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Last Updated</th>
          <th class="px-6 py-3 text-center text-xs font-medium text-gray-500 uppercase tracking-wider">Actions</th>
        </tr>
      </thead>
      <tbody id="tbody-assets" class="bg-white divide-y divide-gray-200">
        <!-- Rows injected via jQuery/AJAX -->
      </tbody>
    </table>
  </div>
  <!-- Pagination -->
  <div class="flex items-center justify-between py-3">
    <div class="text-sm text-gray-700">
      Showing <span id="lbl-start">1</span> to <span id="lbl-end">10</span> of <span id="lbl-total">0</span> assets
    </div>
    <div class="flex space-x-2">
      <button id="btn-prev-page" class="border border-gray-300 px-3 py-1 rounded-md text-gray-700 hover:bg-gray-100 disabled:opacity-50" disabled>Previous</button>
      <button id="btn-next-page" class="border border-gray-300 px-3 py-1 rounded-md text-gray-700 hover:bg-gray-100 disabled:opacity-50" disabled>Next</button>
    </div>
  </div>
  ```
* **JavaScript Behavior (assets.js):**

  1. On page load:

     * Populate category and department filters using AJAX `GET /api/categories`, `/api/departments`.
     * Load initial asset list: `GET /api/assets?page=1&limit=10`.
  2. **Search Input:** Debounce 300ms on `keyup`, then call `loadAssets({ search: value, status: selectedStatus, category: selectedCategory, department: selectedDepartment, page: 1 })`.
  3. **Filter Dropdowns:** On `change`, call same `loadAssets(...)`.
  4. **Pagination Buttons:** Maintain `currentPage`, `totalPages` from API response. On click, call `loadAssets({ page: currentPage ± 1, …otherFilters })`.
  5. **Row Actions:**

     * Clicking Asset ID link: open Asset Detail Modal (`openAssetDetail(id)`).
     * Clicking Edit icon: open Edit Modal (`openEditAssetModal(id)`).
     * Clicking Delete icon: open Delete Confirmation (`openDeleteModal(id, name)`).
     * Clicking Assign/Unassign icon: call `openAssignPopover($(this), assetId, assetDept, assetStatus)`.

### 4. User Management Page

**URL:** `/users.html`

* Very similar to Asset Listing in layout.
* **Search & Filter:** by Name/Email, Role, Department, Status.
* **Table Columns:** User ID, Name, Email, Role, Department, Status Badge (Active = `bg-green-100 text-green-800`; Inactive = `bg-gray-100 text-gray-800`), Actions (Edit, Deactivate/Activate, Reset Password).
* **Modals & Popovers:**

  * Add/Edit User: two-column form for desktop, single column mobile.
  * Confirmation popovers for deactivate/activate; small modal for reset password confirmation.

### 5. Reports Page

**URL:** `/reports.html`

* **Tabs or Pills:** Use Tailwind’s `flex border-b border-gray-200` with `-mb-px`. Each tab: `px-4 py-2 text-sm font-medium text-gray-600 hover:text-indigo-700 cursor-pointer` with `border-b-2 border-indigo-500 text-indigo-600` for active.
* **Date Range Picker Section:**

  ```html
  <div class="flex flex-col sm:flex-row sm:items-center sm:space-x-4 mb-6">
    <div class="flex-1">
      <label for="report-from" class="block text-sm font-medium text-gray-700">From:</label>
      <input type="date" id="report-from" class="mt-1 block w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500" />
    </div>
    <div class="flex-1 mt-4 sm:mt-0">
      <label for="report-to" class="block text-sm font-medium text-gray-700">To:</label>
      <input type="date" id="report-to" class="mt-1 block w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500" />
    </div>
    <div class="mt-4 sm:mt-6">
      <button id="btn-generate-report" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-md">Generate</button>
    </div>
  </div>
  ```
* **Report Table & Chart Placeholder:**

  ```html
  <div id="report-section" class="bg-white shadow rounded-lg p-6">
    <!-- Table injected here -->
    <div class="overflow-x-auto mb-6">
      <table id="tbl-report" class="min-w-full divide-y divide-gray-200">
        <!-- Dynamic header/rows -->
      </table>
    </div>
    <div class="w-full h-64 bg-gray-50 rounded-lg flex items-center justify-center">
      <p class="text-gray-400">Chart will render here</p>
    </div>
    <div class="mt-4 text-right">
      <button id="btn-export-csv" class="bg-white border border-gray-300 text-gray-700 px-4 py-2 rounded-md hover:bg-gray-50">Export to CSV</button>
    </div>
  </div>
  ```
* **JavaScript Behavior (reports.js):**

  1. On tab click: set `currentReportType` and update UI.
  2. On “Generate” click: read dates, validate (`from ≤ to`), AJAX `GET /api/reports/{type}?from=<>&to=<>`.
  3. Populate `#tbl-report` with header/rows.
  4. On “Export to CSV” click: if a report has been generated, `window.location = '/api/reports/{type}/export?from=<>&to=<>'`.
  5. Optionally initialize Chart.js when real data arrives (placeholder for integration).

### 6. Settings Page

**URL:** `/settings.html`

* **Tabs on Left (Vertical Nav):**

  * Company Profile
  * Asset Categories
  * Departments
  * System Preferences
  * Audit Logs (link)

* **Company Profile Section:**

  ```html
  <section class="bg-white shadow rounded-lg p-6 mb-8">
    <h2 class="text-xl font-semibold text-gray-900 mb-4">Company Profile</h2>
    <form id="form-company-profile" class="grid grid-cols-1 md:grid-cols-2 gap-6">
      <div>
        <label for="company-name" class="block text-sm font-medium text-gray-700">Company Name</label>
        <input type="text" id="company-name" class="mt-1 block w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500" />
      </div>
      <div>
        <label for="company-logo" class="block text-sm font-medium text-gray-700">Logo</label>
        <div id="logo-upload" class="mt-1 flex items-center">
          <img id="img-logo-preview" src="/images/default-logo.svg" alt="Company Logo" class="h-12 w-12 rounded-full object-cover mr-4" />
          <input type="file" id="company-logo" accept="image/*" class="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:border file:border-gray-300 file:rounded-md file:text-sm file:font-medium file:bg-white file:text-gray-700 hover:file:bg-gray-50" />
        </div>
      </div>
      <div>
        <label for="company-address" class="block text-sm font-medium text-gray-700">Address</label>
        <textarea id="company-address" rows="3" class="mt-1 block w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"></textarea>
      </div>
      <div>
        <label for="contact-email" class="block text-sm font-medium text-gray-700">Contact Email</label>
        <input type="email" id="contact-email" class="mt-1 block w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500" />
      </div>
      <div>
        <label for="contact-phone" class="block text-sm font-medium text-gray-700">Contact Phone</label>
        <input type="tel" id="contact-phone" class="mt-1 block w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500" />
      </div>
      <div class="col-span-1 md:col-span-2 text-right">
        <button type="submit" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-md">Save Changes</button>
      </div>
    </form>
  </section>
  ```

* **Asset Categories Section:**

  ```html
  <section class="bg-white shadow rounded-lg p-6 mb-8">
    <div class="flex justify-between items-center mb-4">
      <h2 class="text-xl font-semibold text-gray-900">Asset Categories</h2>
      <button id="btn-add-category" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-md">Add Category</button>
    </div>
    <div class="overflow-x-auto">
      <table id="tbl-categories" class="min-w-full divide-y divide-gray-200">
        <thead class="bg-gray-50">
          <tr>
            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Name</th>
            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Description</th>
            <th class="px-6 py-3 text-center text-xs font-medium text-gray-500 uppercase tracking-wider">Actions</th>
          </tr>
        </thead>
        <tbody class="bg-white divide-y divide-gray-200">
          <!-- Populated via AJAX -->
        </tbody>
      </table>
    </div>
  </section>
  ```

* **Departments Section:** Same pattern as Categories (change labels accordingly).

* **System Preferences Section:**

  ```html
  <section class="bg-white shadow rounded-lg p-6 mb-8">
    <h2 class="text-xl font-semibold text-gray-900 mb-4">System Preferences</h2>
    <form id="form-system-preferences" class="space-y-6">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div>
          <label for="default-currency" class="block text-sm font-medium text-gray-700">Default Currency</label>
          <select id="default-currency" class="mt-1 block w-full border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
            <option value="INR">INR</option>
            <option value="USD">USD</option>
            <option value="EUR">EUR</option>
            <!-- etc. -->
          </select>
        </div>
        <div>
          <label for="maintenance-interval" class="block text-sm font-medium text-gray-700">Default Maintenance Interval</label>
          <div class="flex space-x-2">
            <input type="number" id="maintenance-interval" class="mt-1 block w-1/2 border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500" min="1" />
            <select id="maintenance-unit" class="mt-1 block w-1/2 border border-gray-300 rounded-md px-3 py-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
              <option value="days">Days</option>
              <option value="weeks">Weeks</option>
              <option value="months">Months</option>
            </select>
          </div>
        </div>
        <div class="col-span-1 md:col-span-2">
          <fieldset>
            <legend class="text-sm font-medium text-gray-700">Notification Methods</legend>
            <div class="mt-2 space-y-2">
              <div class="flex items-center">
                <input id="notif-email" name="notification[]" type="checkbox" value="email" class="h-4 w-4 text-indigo-600 border-gray-300 rounded focus:ring-indigo-500" />
                <label for="notif-email" class="ml-2 block text-sm text-gray-700">Email</label>
              </div>
              <div class="flex items-center">
                <input id="notif-sms" name="notification[]" type="checkbox" value="sms" class="h-4 w-4 text-indigo-600 border-gray-300 rounded focus:ring-indigo-500" />
                <label for="notif-sms" class="ml-2 block text-sm text-gray-700">SMS</label>
              </div>
              <div class="flex items-center">
                <input id="notif-inapp" name="notification[]" type="checkbox" value="inapp" class="h-4 w-4 text-indigo-600 border-gray-300 rounded focus:ring-indigo-500" />
                <label for="notif-inapp" class="ml-2 block text-sm text-gray-700">In-App</label>
              </div>
            </div>
          </fieldset>
        </div>
      </div>
      <div class="text-right">
        <button type="submit" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-md">Save Preferences</button>
      </div>
    </form>
  </section>
  ```

* **Audit Logs Link:** A simple link or button: `<a href="/audit-logs.html" class="text-indigo-600 hover:underline">View Audit Logs</a>`.

### 7. Audit Logs Page (Optional / If API Available)

**URL:** `/audit-logs.html`

* Simple table listing (Date/Time, User, Action, Entity, Details).
* Search by User, Date Range, Action Type.
* Pagination as before.

## UI/UX Considerations & Interaction Flows

1. **Loading States & Spinners**

   * Whenever an AJAX call is in progress for a container (table, card metrics, form submission), display a centered spinner overlay:

     ```html
     <div class="absolute inset-0 bg-white bg-opacity-75 flex items-center justify-center z-10">
       <svg class="animate-spin h-8 w-8 text-indigo-600" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
         <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
         <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4z"></path>
       </svg>
     </div>
     ```
   * Each container (`#tbody-assets`, `#tbl-users`, `#report-section`) should have a relative container for spinner overlay insertion by jQuery.

2. **Empty States**

   * If listing yields zero results, show a friendly illustration (SVG) with text “No assets found” or “No users found” and a link/button to “Add New Asset” / “Add User.”
   * Use `flex flex-col items-center justify-center py-20` with `text-gray-500`.

3. **Confirmation & Danger States**

   * Deletion/Destructive actions always require a confirmation modal with red highlight for “Delete” button.
   * Assign/Unassign popovers use neutral backgrounds but clickable areas highlighted in primary accent.
   * If an asset is overdue for maintenance, show a small warning icon next to status, with a tooltip (“Maintenance overdue by X days”).

4. **Form Validation Feedback**

   * On blur of required fields, validate non-empty; if invalid, apply `border-red-500` and show `<p class="text-red-600 text-sm mt-1">This field is required</p>`.
   * For email/password, validate format.
   * Prevent form submission if any errors; show an aggregated error summary at the top (`<div class="bg-red-50 border-l-4 border-red-400 text-red-700 p-4 mb-4">Please fix the errors below.</div>`).

5. **Mobile Responsiveness**

   * **Header** collapses: hamburger toggles side nav overlay.
   * **Side Nav** becomes an off-canvas panel: `fixed inset-y-0 left-0 w-64 bg-white shadow-lg transform -translate-x-full transition-transform`. Revealed by toggling `translate-x-0`.
   * **Tables**: wrap inside `<div class="overflow-x-auto">`.
   * **Forms**: two-column grids collapse to one column (`grid-cols-1`).
   * **Buttons & Touch Targets**: minimum size `44px × 44px` tappable area (Tailwind’s default `px-4 py-2` is sufficient).

6. **Feedback Loops**

   * After a successful create/update/delete, show a non-intrusive toast and refresh affected UI section rather than full page reload.
   * Use jQuery’s `$.ajax().done()` and `fail()` callbacks to handle these feedback loops.

## Non-UI Deliverables

1. **Design Assets**

   * **Tailwind Configuration** (`tailwind.config.js`): Contains custom colors, font families, extended spacing scale if needed.
   * **SVG Icon Set**: All required icons (assets, users, maintenance, reports, settings) exported as an SVG sprite or individual SVG files optimized.
   * **Mockups (Optional)**: Static Figma/Sketch/Adobe XD layouts for major pages (Dashboard, Asset Listing, Asset Detail, Add/Edit Asset Modals) so developers know final look.

2. **Implementation Artifacts**

   * **HTML Templates:** All page templates with semantic structure and Tailwind classes. Use partials for header, sidebar, footer, modals. Provide comments indicating where dynamic content should be inserted (via jQuery).
   * **CSS Files:**

     * `tailwind.css` (compiled, minified for production).
     * `custom.css` for any minor override or vendor patches.
   * **JavaScript Modules:**

     * `main.js`: initializes global handlers, imports other modules.
     * Module files (`auth.js`, `dashboard.js`, `assets.js`, etc.) exporting an initialization function (`initAssetsModule()`) to wire up event listeners.
   * **Utility Scripts:**

     * `ajax-setup.js` (sets up CSRF headers, global error handlers).
     * `toast.js` (functions to show/hide toast notifications).
     * `modal.js` (generic open/close modal logic using jQuery).

3. **Documentation & Comments**

   * **README.md**: High-level setup instructions (install Node, run `npm install`, `npm run build`, point web server to `dist` folder).
   * **Component Usage Guide**: A brief markdown file explaining how to use common UI patterns (cards, modals, tables, forms) with Tailwind classes and jQuery hooks.
   * **API Contract Document (Front-End Perspective)**: List of all expected endpoints, HTTP methods, request/response schemas, and possible error codes—so front-end developers know exactly how to structure AJAX calls.

## Timeline & Milestones

*Assuming a dedicated front-end team of 2 developers + 1 designer, working full time for a high-priority project. All dates relative to Project Kick-Off (Week 0).*

| Milestone                                | Deliverable                                                                             | Timeline      |
| ---------------------------------------- | --------------------------------------------------------------------------------------- | ------------- |
| 1. Project Kick-Off & Requirement Review | Finalized PRD (you are here), wireframes approved                                       | Week 0        |
| 2. Design System Setup                   | Tailwind config, color palette, typography, icon set                                    | End of Week 1 |
| 3. Static Templates & Layout             | HTML templates for Login, Dashboard skeleton, common partials (header, sidebar, footer) | End of Week 2 |
| 4. Authentication Module                 | Login page JS/AJAX, session handling, global error handler                              | Mid Week 3    |
| 5. Dashboard Implementation              | Summary cards, Recent Activity, placeholders for charts                                 | End of Week 3 |
| 6. Asset Listing & Filters               | Table layout, search/filter logic, pagination, modals for Add/Edit/Delete               | End of Week 4 |
| 7. Asset Detail & Maintenance            | Detail modal, maintenance CRUD modals, assignment logic                                 | Mid Week 5    |
| 8. Asset Request & Approval Workflow     | Request form, Pending Requests page, approval/rejection modals                          | End of Week 5 |
| 9. User Management Module                | User listing, CRUD modals, role/department filters                                      | Mid Week 6    |
| 10. Reporting Module                     | Report tabs, date-range filters, dynamic table, CSV export                              | End of Week 6 |
| 11. Settings Module                      | Company Profile, Categories, Departments, Preferences                                   | Mid Week 7    |
| 12. QA & Accessibility Testing           | Cross-browser, screen-reader tests, performance audit                                   | End of Week 7 |
| 13. Polish & Bug Fixing                  | Final UI tweaks, optimize assets, documentation update                                  | Week 8        |
| 14. UAT & Deployment                     | Stakeholder review, user acceptance testing, live deploy                                | End of Week 8 |

This timeline assumes no major backend API delays. Any changes to API contracts must be communicated promptly to front-end developers to avoid rework.

## Deliverables Checklist

* [ ] **PRD** (this document)
* [ ] **Design System Assets** (Tailwind config, color palette spec, icon set)
* [ ] **HTML Templates** (all pages & partials)
* [ ] **CSS Files** (`tailwind.css`, `custom.css`)
* [ ] **JavaScript Modules** (`auth.js`, `dashboard.js`, `assets.js`, `users.js`, `reports.js`, `settings.js`, plus utilities)
* [ ] **Mockups / Wireframes** (if provided by design)
* [ ] **API Contract Reference** for front-end
* [ ] **README & Developer Setup Guide**
* [ ] **Accessibility & Performance Audit Report** (post-QA)

## Success Metrics & KPIs

1. **Time to First Contentful Paint (FCP):** < 1.5 seconds on 4G.
2. **Time to Interactive (TTI):** < 2.5 seconds on 4G.
3. **Lighthouse Score:** ≥ 90 in Performance, ≥ 95 in Accessibility, ≥ 90 in Best Practices.
4. **User Satisfaction Survey (post-UAT):** Overall UI/UX rating ≥ 4.5 out of 5.
5. **Defect Rate:** < 2 critical UI/UX bugs in UAT.

## Appendix

### A. Example AJAX Calls (jQuery)

```js
// Global AJAX setup (ajax-setup.js)
$.ajaxSetup({
  headers: {
    'X-CSRF-Token': window.csrfToken  // injected by server on page load
  },
  error: function(xhr, status, error) {
    if (xhr.status === 401) {
      window.location.href = '/login.html';
    } else if (xhr.status === 403) {
      showToast('Access Denied', 'error');
    } else {
      showToast('An unexpected error occurred', 'error');
    }
  }
});

// Load Assets (assets.js)
function loadAssets(params) {
  const spinner = showSpinner('#tbody-assets');
  $.get('/api/assets', params)
    .done(function(res) {
      renderAssetRows(res.data);
      updatePagination(res.meta);
    })
    .always(function() {
      spinner.hide();
    });
}

// Create Asset
$('#form-add-asset').on('submit', function(e) {
  e.preventDefault();
  const payload = {
    name: $('#asset-name').val().trim(),
    categoryId: $('#asset-category').val(),
    // ...other fields
  };
  // Client-side validation omitted for brevity
  $.post('/api/assets', payload)
    .done(function(res) {
      $('#modal-add-asset').modal('hide');
      showToast('Asset created successfully', 'success');
      loadAssets({ page: 1 });
    })
    .fail(function(xhr) {
      displayFormErrors(xhr.responseJSON.errors);
    });
});
```

### B. Sample Tailwind Configuration (`tailwind.config.js`)

```js
module.exports = {
  mode: 'jit',
  purge: ['./templates/**/*.html', './assets/js/**/*.js'],
  darkMode: false,
  theme: {
    extend: {
      colors: {
        indigo: {
          50: '#EEF2FF',
          100: '#E0E7FF',
          200: '#C7D2FE',
          300: '#A5B4FC',
          400: '#818CF8',
          500: '#6366F1',
          600: '#4F46E5',
          700: '#4338CA',
          800: '#3730A3',
          900: '#312E81'
        },
        teal: {
          50: '#F0FDFA',
          100: '#CCFBF1',
          200: '#99F6E4',
          300: '#5EEAD4',
          400: '#2DD4BF',
          500: '#14B8A6',
          600: '#0D9488',
          700: '#0F766E',
          800: '#115E59',
          900: '#134E4A'
        }
      },
      fontFamily: {
        sans: ['Inter', 'ui-sans-serif', 'system-ui', 'sans-serif']
      }
    }
  },
  variants: {
    extend: {
      opacity: ['disabled'],
      ringWidth: ['focus']
    }
  },
  plugins: []
};
```

### C. Accessibility Checklist

* [ ] All interactive elements have visible focus states.
* [ ] ARIA roles/labels are applied on modals, alerts, and form elements.
* [ ] Color contrast meets minimum ratios.
* [ ] Tables have proper `<th scope="col">` and `<caption>` if needed.
* [ ] Images have `alt` attributes (or are marked decorative).
* [ ] Dropdowns and popovers are keyboard-navigable (Esc to close, arrow keys where applicable).

---

By following this PRD, front-end developers will have a clear, detailed roadmap to implement a polished, professional Asset Management Software interface using only HTML, CSS, JavaScript, Tailwind CSS, AJAX, and jQuery. The result should reflect the organization’s investment level (> 10 lakh) through a modern, performant, and accessible design.
