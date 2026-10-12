# version 1:
# Stage 3: Plan the product and requirements

This turns the Version 1 scope into behaviors that can be implemented and checked.

## User and outcome

**Primary user:** A student who wants to remember and present projects, courses, events, volunteering, and other learning experiences.

**Desired outcome:** The user can record an experience, find it later, and deliberately share selected information in a portfolio.

## Functional requirements

### Accounts and ownership

- **FR-01:** A person can create an account, sign in, and sign out.
- **FR-02:** Each journal entry, link, and attachment belongs to the account that created it.
- **FR-03:** A user can read, change, and delete only their own private journal data.
- **FR-03a:** A user can recover account access through an email-based password reset flow.
- **FR-03b:** A user can delete their account. Account deletion removes their journal entries, attachments, portfolio data, and public portfolio page.

### Journal entries

- **FR-04:** A signed-in user can create, view, edit, and delete a journal entry.
- **FR-05:** An entry requires a title and one category. Date and notes are optional.
- **FR-05a:** Categories include projects, work experience, education, courses or certifications, workshops or events, achievements, volunteering, research or publications, and other experiences.
- **FR-06:** A user can add project or reference links to an entry. Journal links remain private unless deliberately added to portfolio content.
- **FR-07:** A user can upload supporting files or photos from a phone or laptop browser and associate them with an entry.
- **FR-08:** A user can browse their entries and search entry titles, notes, and categories later.

### Portfolio

- **FR-09:** A signed-in owner can open an owner-only portfolio editor from their private journal area. Visitors to a public portfolio cannot edit it.
- **FR-10:** The owner can edit portfolio details and section content, preview the portfolio, and publish or unpublish it at a shareable web address.
- **FR-11:** The portfolio supports About Me (name, profile picture, introduction); Education (degree, college, academic details); Skills (technical and soft skills); Projects (description, technologies, GitHub links); Experience (internships, jobs, work experience); Achievements (awards, rankings, competition results); Certifications and completed courses; Workshops and Events; Research and Publications; a downloadable Resume; Contact (email and professional links); and Social Links (LinkedIn, GitHub, personal blog).
- **FR-12:** Testimonials and Interests are optional portfolio sections.
- **FR-13:** The owner can choose which portfolio sections to show and add, edit, or remove content in each section.
- **FR-14:** Empty sections are omitted from the public portfolio without an empty-state message.
- **FR-15:** Journal entries can be selected for portfolio use and given a public description separate from private journal notes. The entry's category maps it to an appropriate portfolio section.
- **FR-16:** The published portfolio is viewable by anyone with its shareable web address, but Version 1 does not request search-engine indexing. It does not expose the journal or editor.
- **FR-17:** Attachments are private by default. The owner must deliberately add a specific file to a portfolio section before it can be viewed or downloaded publicly. Selecting an entry for the portfolio does not publish its attachments.
- **FR-18:** Removing content from the portfolio or unpublishing the portfolio removes it from the public page.

## Quality requirements

- **QR-01 — Privacy:** A visitor who is not signed in cannot access private journal entries or private attachments.
- **QR-02 — Account isolation:** One signed-in user cannot read, modify, or delete another user's private entries or files, including by changing an identifier in a request or URL.
- **QR-03 — Explicit sharing:** Public pages expose only the fields and attachments the owner deliberately selected for sharing.
- **QR-04 — Responsive use:** The main flows work in a modern mobile browser and a desktop browser, including choosing files through the device's browser file picker.
- **QR-05 — Clear feedback:** The app confirms successful saves and shows a useful error when a save or upload fails; it must not silently lose the user's input.
- **QR-06 — Accessible forms:** Form controls have labels, can be used with a keyboard, and communicate validation errors in text.
- **QR-07 — Portfolio access:** The portfolio editor checks the signed-in user's ownership on the server; hiding its button from visitors is not sufficient access control.
- **QR-08 — No empty sections:** Public portfolio pages render only sections with content.
- **QR-09 — Search visibility:** Version 1 portfolio pages are not submitted for search-engine indexing; direct-link visitors can still view published content.

## Acceptance criteria

These are examples of observable checks for the requirements. Stage 6 will plan and perform the actual testing.

### Save and retrieve an entry

- **Given** a signed-in user, **when** they create an entry and save it, **then** it appears in their journal.
- **Given** a saved entry, **when** the user signs out and later signs back in, **then** the entry and its saved details are still available to that user.
- **Given** multiple entries, **when** the user searches for a word in a title, note, or category, **then** matching entries are shown and non-matching entries are hidden.
- **Given** a signed-in user, **when** they request a password reset, **then** the app provides an email-based recovery flow.
- **Given** a user who chooses to delete their account, **when** deletion is completed, **then** their journal data, uploaded files, portfolio content, and public portfolio page are removed.

### Keep accounts and files private

- **Given** two different user accounts, **when** one user tries to open or change the other user's private entry or file, **then** access is denied.
- **Given** an uploaded attachment, **when** it has not been explicitly made public, **then** a logged-out visitor cannot view or download it.

### Publish selected portfolio content

- **Given** a journal entry that has not been selected for the portfolio, **when** a visitor opens the public portfolio, **then** that entry and its private notes are not shown.
- **Given** a selected entry, **when** its owner publishes a portfolio description, **then** visitors can see the description and only the links intended for the portfolio.
- **Given** an owner who is signed in, **when** they open the portfolio editor from their journal, **then** they can edit their portfolio; another account and logged-out visitors cannot.
- **Given** a portfolio section with no content, **when** a visitor opens the published portfolio, **then** the section heading and an empty-state message are not shown.
- **Given** a portfolio with content in some sections, **when** the owner changes that content and publishes the changes, **then** the public page shows the updated content.
- **Given** an attachment on a published entry, **when** that file has not separately been made public, **then** the portfolio does not expose the file.
- **Given** a file deliberately added to a published portfolio section, **when** a visitor opens that section, **then** the file is clearly presented as public and can be downloaded.
- **Given** published content, **when** the owner removes it from the portfolio or unpublishes the portfolio, **then** it is no longer available from the public portfolio page.

### Use on phone and laptop

- **Given** a phone or laptop browser, **when** a user signs in, creates an entry, adds a link, and uploads a supported file, **then** the main journey can be completed without layout or file-picker blockers.
- **Given** an owner using the portfolio editor, **when** they update a profile section or a journal-derived portfolio entry, **then** the change can be saved and previewed before publishing.

## decisions to make for v1 currently:

Resolve these before designing the detailed data model and interface:

1. Which exact file formats and maximum file size should Version 1 support? The user needs PDFs, images, and documents.
2. Should users be allowed to create custom journal categories beyond the listed categories and “Other”?

## Release checks

Before inviting other people to use Version 1:

- The create, find, select, publish, and unpublish journey works end to end.
- The owner can edit portfolio information from the private journal area, preview changes, and publish them.
- Empty sections are hidden; the public portfolio contains no private journal details.
- Account-isolation and private-file checks pass for at least two separate accounts.
- The same core journey works on phone and laptop browsers.
- Upload types and size limits are visible to the user, and rejected uploads get a clear explanation.
- The deployed app does not expose private credentials or private user content.
