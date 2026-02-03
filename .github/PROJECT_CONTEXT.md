1. PROJECT OVERVIEW
• Project Name: Project Cousteau (DAN Southern Africa Member & Admin Portal)
• Purpose: To develop a unified digital platform for DAN Southern Africa that consolidates membership management, training administration, and partner relationships into a single ecosystem.
• Description: The project replaces disparate manual systems (Google Sheets, Access DB, legacy portals) with a modern web application. It consists of a Member Portal for divers, instructors, and commercial entities to manage their profiles, payments, and training, and an Admin Portal ("God Mode") for DAN staff to manage applications, approvals, medical reviews, and financial reconciliation. The system aims to streamline the complex logic regarding membership tiers, medical clearances, and training certifications.
• Repository URL: [TODO: Repository URL not provided in sources]
• Key Source Documents: "Project Cousteau - Proposal", "Membership Portal User Stories", "Annual DAN Membership", "Netcash Workshop Notes".
2. TECH STACK
• Frontend:
    ◦ Framework: Next.js (Web App & Admin App)
    ◦ Language: TypeScript/JavaScript (implied by Next.js)
    ◦ Styling: [TODO: CSS framework - Tailwind/MUI? Not specified]
    ◦ Forms: Custom form components/templates to replace/integrate with existing Elfsight logic.
• Backend:
    ◦ Framework: Nest.js
    ◦ Language: TypeScript (implied by Nest.js)
    ◦ Infrastructure: AWS (Lambda, S3 mentioned for file storage).
• Database:
    ◦ Type: [TODO: SQL/NoSQL? Likely Relational given the data structure, hosted on AWS]
    ◦ Schema: Must handle hierarchical relationships (Main Member -> Family -> Training) and Company -> Staff slots.
• File Storage:
    ◦ Service: AWS S3 (for medical certs, ID documents, member cards).
    ◦ Purpose: Storage of sensitive user uploads and generated PDFs (Member Cards, Travel Letters).
• Auth:
    ◦ Admin: Microsoft SSO (Azure AD integration via AWS Identity Center).
    ◦ Members: Email/Password with 2FA via Email/OTP.
• APIs/Integrations:
    ◦ Payments: Netcash (Debit Orders, Credit Card, E-mandates).
    ◦ Training LMS: Teachable (External link integration; Admin manages coupon codes generated here).
    ◦ Legacy Forms: Elfsight (Initially used, potentially being replaced or scraped; transition to internal form components preferred).
    ◦ Magazines: Issuu (External links for digital publications).
3. USER ROLES
• Super Admin
    ◦ Access: Full System Access.
    ◦ Capabilities: Manage other Admins, System Configuration (pricing, course visibility), View/Edit all records.
    ◦ Auth: Microsoft SSO.
• Admin (Staff)
    ◦ Access: General management (Membership, Training, Commercial).
    ◦ Capabilities: Process applications, view payments, manage training packs.
    ◦ Restrictions: Cannot view medical information (Confidentiality Rule).
    ◦ Auth: Microsoft SSO.
• Admin Medic (Internal)
    ◦ Access: Full Member + Medical Data.
    ◦ Capabilities: Review "Medic Pending" applications, approve/reject based on health data, edit medical fields.
• External Medic
    ◦ Access: Restricted View.
    ◦ Capabilities: View member status/contact info, edit medical fields only. Cannot approve memberships, only recommend/comment.
• Annual Member (Main)
    ◦ Types: Standard, Plus, Master (Pro/Tech).
    ◦ Capabilities: Manage profile, add family (dependents), pay fees, view digital card, log travel.
• Industry Partner
    ◦ Prerequisite: Must be an active Master Annual Member.
    ◦ Capabilities: Buy/Assign temporary coverage credits, invite temporary members.
• Commercial Company Admin
    ◦ Capabilities: Purchase "Slots", assign staff to slots (active/inactive toggling), upload staff medicals. No personal diving coverage.
• Instructor / Instructor Trainer
    ◦ Capabilities: Buy training packs, register students, view student certification history.
4. KEY DATA MODELS/ENTITIES
• Member (Individual)
    ◦ Key Fields: DAN Number (PK - generated), First Name, Last Name, Email, Membership Type (Standard/Plus/Master), Status (Active/Inactive/Pending), Medical Flags (Boolean).
    ◦ Business Rules: Main member and family must be on the same tier. Children age limit 21 (27 if dependent).
• Membership Application
    ◦ Status States: Pending, Medic Pending (if medical=yes), Under Review, Approved, Rejected.
    ◦ Relationships: Linked to Payment Transaction.
• Commercial Company
    ◦ Key Fields: Company Name, Slot Count, Staff List.
    ◦ Business Rules: Slots are purchased; Staff are assigned to slots. Staff must have valid medical/commercial certs.
• Training Course
    ◦ Key Fields: Course Name, Price, Linked Teachable URL.
    ◦ Relationships: Has many Training Packs (Codes).
• Training Pack/Code
    ◦ Key Fields: Code String (from Teachable), Status (Used/Unused), Purchased By (Instructor ID).
• Travel Notification
    ◦ Key Fields: Destination, Start Date, End Date, Family Members included.
    ◦ Business Rules: Triggers admin alert; generates travel letter PDF upon approval.
• Temporary Membership
    ◦ Key Fields: Duration (Days), Start Date, Assigned By (Industry Partner ID or Self-Pay).
5. STANDARD PATTERNS
• Frontend:
    ◦ Dashboard: "God Mode" for Admins reuses Member Portal components (dashboard views) for consistency.
    ◦ Navigation: Persistent sidebar (Admin), Tile-based dashboard (Member).
    ◦ Visuals: Status flags (Active=Green, Inactive=Grey, Pending=Yellow).
• Backend:
    ◦ Code Structure: Nest.js modular architecture.
    ◦ Export: CSV generation for financial reconciliation and Mailchimp imports.
• API:
    ◦ Netcash: SOAP/REST integration for E-mandates and polling payment status.
    ◦ Pattern: Request validation -> Business Logic -> DB Transaction -> Email Notification trigger.
• Naming:
    ◦ DAN Number: Unique identifier, format varies by member type (e.g., standard vs. commercial).
    ◦ Pack Codes: String-based codes for Teachable access.
• Error Handling:
    ◦ Validation: Inline form validation (e.g., age limits, missing medical docs).
    ◦ System: "Validation error" displayed if Industry Partner has insufficient credits for a request.
6. NON-FUNCTIONAL REQUIREMENTS
• Performance:
    ◦ Must handle monthly debit order batch processing/reconciliation.
    ◦ Estimated dev effort: 2,400 - 3,000 hours.
• Security:
    ◦ Medical Data: Strict visibility controls (Admin vs. Medic Admin).
    ◦ Payments: PCI compliance handled via Netcash redirect/E-mandate; no sensitive banking data stored directly on app servers if possible (tokenized).
• Browsers: Mobile-responsive web app required.
• Scalability: AWS Cloud infrastructure to handle file storage and user load.
7. PROJECT-SPECIFIC CONFIGURATIONS
• File Uploads:
    ◦ Types: Medical Certificates, ID/Passport, Dive Qualifications.
    ◦ Formats: PDF, JPEG.
• Automated Workflows:
    ◦ Renewal: Automatic email reminders for expiring memberships/certifications.
    ◦ Status Changes: If a "Medic Pending" application is approved by a Medic, it automatically moves to "Admin Approved" (or "Admin Pending" depending on payment).
    ◦ Commercial Expiry: Staff set to "Inactive" automatically if medical cert expires.
• Export Formats:
    ◦ Finance: CSV with specific columns (GL Codes, VAT, Amount) to match Pastel/Accounting needs.
    ◦ Mailchimp: CSV export of member emails/status.
• Domain-Specific Rules:
    ◦ Cross-Border: Temporary members must cross borders (unless booked via Industry Partner).
    ◦ Family: Main member pays; dependents linked to main member's payment method.
    ◦ Debit Orders: New mandates required if bank details change or amount exceeds mandate range.