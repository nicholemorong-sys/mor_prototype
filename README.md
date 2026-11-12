# ISKOLAR MARSU

Responsive, multi-page scholarship application and monitoring prototype for Marinduque State University. Built with semantic HTML, CSS, and vanilla JavaScript; no framework or package installation is required.

## Run locally

Serve this folder with a local web server and open `index.html`. For example:

```powershell
python -m http.server 8000
```

Then visit `http://localhost:8000`. A local or hosted web server is recommended for the Web Crypto API and document storage.

The official MarSU seal is bundled at `assets/marsu_logo.png`; a MarSU-colored monogram appears if the image is unavailable.

## Account access

- Staff provision student accounts using the student's assigned Student ID Number and contact/profile information. Students create their own password on first access, then sign in using Student ID Number and that password.
- Student and Staff / Admin users have separate sign-in pages and dashboards. The landing page lets users choose the appropriate portal.
- Staff / Admin users sign in with their institutional email or authorized personal Gmail address and assigned password.
- Staff credentials are not embedded in or displayed by the public interface; this project includes no demo staff account.
- Authorized staff can assign student IDs from the staff-only Student accounts page. No student password is set or distributed by staff.
- The first Staff / Admin account must be provisioned by a trusted administrator or authentication service. There is intentionally no public way to create a privileged account.

Student records use `studentId`, `email` (for application contact and records), `role` (`student` or `admin`), and `status`. A student's first password setup stores a salted PBKDF2 hash in this browser prototype. Production deployments should integrate institution-managed authentication and server-side authorization.

## Pages

- `index.html` — Role portal chooser.
- `login.html` — Student ID and password sign-in.
- `student-setup.html` — First-time student password creation for a staff-provisioned Student ID.
- `staff-login.html` — Dedicated Staff / Admin sign-in.
- `student-access.html` — Student account access help; it does not create accounts.
- `register.html` — Legacy link to the same account access help page; no registration form.
- `student-dashboard.html` — Student applications, scholarship summaries, and announcements.
- `admin-dashboard.html` — Staff overview, application review queue, and CSV export.
- `student-accounts.html` — Staff-only Student ID assignment, directory, and access management.
- `scholarships.html` — Searchable scholarship catalog; staff can add and edit programs.
- `application.html` — Scholarship requirements, application details, and document uploads.
- `profile.html` — Student profile and optional photo management.
- `tracking.html` — Student-only application status timeline and decision notes.
- `announcements.html` — Student announcement board; staff can publish and remove notices.
- `payouts.html` — Payout schedule list; staff can publish, edit, or remove entries.

Shared behavior is in `app.js`; visual styles and responsive rules are in `styles.css`.

## Features

- Separate student and Staff / Admin sign-in flows with separate dashboards.
- Staff-assigned Student ID accounts; students set their own password on first access. There is no public account registration.
- Student and staff dashboards, student profiles, scholarship search and filters, requirements, applications, and document uploads.
- Student-visible status tracking; only staff-facing review controls can update application decisions.
- Staff review includes documents, applicant verification, student account management, application CSV export, scholarship programs, announcements, and payout schedules.
- Notification panel, responsive navigation, accessible status feedback, and input/file validation.

The initial scholarships, announcements, and payout dates are sample content. Confirm eligibility, deadlines, award amounts, and release dates with MarSU and each provider before relying on them.

## Accessibility and responsive design

- Semantic landmarks, headings, lists, forms, labels, and data tables.
- Skip link, visible keyboard focus, native controls, and keyboard-operable actions.
- Accessible names and state attributes for menus, notification panel, review dialog, status updates, and file selection.
- Text alternatives for the university seal and profile image; decorative icons are hidden from assistive technology.
- Desktop uses a persistent side navigation and multi-column layouts; tablet and mobile reduce columns and stack content.
- Mobile navigation collapses into an accessible menu. Tables scroll horizontally on narrow screens.
- Reduced-motion preferences are respected.

## Testing procedures

1. Start the local server. Confirm the role chooser links to separate Student and Staff / Admin sign-in pages, with no displayed Staff / Admin credentials.
2. Provision a Staff / Admin account through a trusted account service before testing staff tools. No starter staff credentials are included.
3. Sign in as staff, assign a student account with a unique Student ID, and verify that no password is requested or stored by the assignment form.
4. Open first-time student setup: confirm an unassigned ID is rejected and a valid assigned ID can set a matching password of at least 8 characters. Confirm the ID cannot be used to set a second password.
5. Sign out; sign in as the student using Student ID and password, update the profile, and submit an application with a small PDF or image.
6. Confirm the student sees only their own application status, cannot access staff pages, and has no decision controls.
7. Sign in as staff using an authorized email account, review the application, verify applicant information, download its uploaded document, and save a status decision.
8. Test program search/filters, program edits, announcement publishing, payout schedule management, CSV export, sign-out, and duplicate application prevention.
9. Test keyboard navigation and visible focus, then check layouts at approximately 375 px, 768 px, and 1280 px widths.

## Prototype security boundary

This is a browser-only prototype, not a production scholarship service. Salted, iterated password hashes, account records, profiles, decisions, and schedules live in the current browser's local storage; uploaded files are held in that browser's IndexedDB. First-time setup currently verifies only that the Student ID exists; a Student ID alone is not proof of identity. Before production, add server-verified one-time activation or another identity check, institution-managed authentication, server-enforced role permissions, protected document storage, validation, audit logging, and approved privacy/security practices. A user with browser developer tools can alter local data. Do not enter real student data in this prototype.
