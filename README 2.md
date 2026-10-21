# Balaji Transport Company — Official Web Portal

A complete, responsive, and bilingual (Hindi & English) business website for **Balaji Transport Company**, based in Mehdawel, Sant Kabir Nagar, Uttar Pradesh, India.

Built with **React**, **Vite**, **React Router v6**, **Lucide Icons**, and clean modular CSS.

---

## 1. Verified Business Profile

* **Company Name:** Balaji Transport Company
* **Chief Executive Officer (CEO):** H. D. Pathak (25+ Years of Industry Experience since 2001)
  * Narayan Transport Group: Branch General Manager (2001–2020)
  * Mehta Transport: Branch General Manager (2020–2026, Previous Position)
  * Balaji Transport Company: Chief Executive Officer (2020–Present)
* **Company Representative Role:** External Deals & Social Media *(Name and bio pending official release)*
* **Contact Phones:**
  * Primary: `+91 9517137669`
  * Secondary: `+91 7668744025`
* **Official Email:** `balajitransportservices21@gmail.com`
* **Business Address:** Mehdawel, Sant Kabir Nagar, Uttar Pradesh, India
* **Core Offerings:** All-India Goods Booking & Freight Enquiries
* **Prominent Corridor:** Mumbai / Bhiwandi to Mehdawel

---

## 2. Project Architecture & Directory Structure

```
balaji-transport-website/
├── index.html                   # HTML5 shell with Open Graph and fonts
├── package.json                 # Node dependencies and build scripts
├── vite.config.js               # Vite bundler configuration
├── .env.example                 # Configurable API base URL blueprint
├── README.md                    # Project documentation & integration guide
├── public/
│   ├── favicon.svg              # Brand truck monogram icon
│   ├── images/
│   │   └── hero-truck.jpg       # High-definition logistics hero banner
│   └── documents/
│       └── README.md            # Document repository guidelines
└── src/
    ├── main.jsx                 # React root entrypoint
    ├── App.jsx                  # Application routing and shell wrapper
    ├── config/
    │   ├── business.js          # Centralized verified business information
    │   └── documents.js         # Document library metadata repository
    ├── content/
    │   └── translations.js      # Bilingual dictionary (English & Hindi)
    ├── context/
    │   └── LanguageContext.jsx  # Global language provider with persistence
    ├── services/
    │   ├── api.js               # Configurable API client with base URL
    │   └── contactService.js    # Contact form service and submission logic
    ├── utils/
    │   └── validation.js        # Strict client validation & WhatsApp URL generator
    ├── styles/
    │   ├── variables.css        # CSS design tokens (Navy, Orange, Slate)
    │   └── global.css           # Global typography, layout, and reset styles
    ├── components/
    │   ├── Header.jsx           # Responsive header with mobile hamburger drawer
    │   ├── Footer.jsx           # Business footer with verified contact details
    │   ├── LanguageSwitcher.jsx # Instant English/Hindi toggle
    │   ├── WhatsAppButton.jsx   # Inline and floating WhatsApp action buttons
    │   ├── ContactCTA.jsx       # High-conversion booking callout banner
    │   ├── ServiceCard.jsx      # Reusable service card with direct prefilled CTA
    │   └── DocumentCard.jsx     # PDF library card with view/download triggers
    └── pages/
        ├── Home.jsx             # Hero banner, route highlight, and service preview
        ├── About.jsx            # CEO career timeline, representative, proposed draft
        ├── Services.jsx         # All-India booking, freight rates, route enquiries
        ├── Documents.jsx        # Company PDF library with empty state
        ├── Contact.jsx          # Direct phone links, WhatsApp, Google Maps, contact form
        └── NotFound.jsx         # Custom accessible 404 page
```

---

## 3. Installation & Local Development

### Prerequisites
* Node.js v18.0.0 or higher
* npm v9.0.0 or higher

### Step 1: Install Dependencies
```bash
npm install
```

### Step 2: Start Development Server
```bash
npm run dev
```
The website will launch at `http://localhost:3000`.

### Step 3: Production Build
```bash
npm run build
```
The optimized production bundle will be generated inside the `dist/` directory.

### Step 4: Preview Production Build
```bash
npm run preview
```

---

## 4. How to Add Real PDFs, Logo, and Images

### Adding Official Company Documents (PDFs)
1. Export your verified document as a PDF (e.g. `balaji-profile-2026.pdf`).
2. Copy the file into `public/documents/`:
   ```bash
   cp my-verified-doc.pdf public/documents/balaji-profile-2026.pdf
   ```
3. Open `src/config/documents.js` and register the document in `DOCUMENTS_CONFIG`:
   ```javascript
   {
     id: "balaji-profile-2026",
     title: {
       en: "Balaji Transport Company Profile",
       hi: "बालाजी ट्रांसपोर्ट कंपनी प्रोफाइल"
     },
     description: {
       en: "Official goods booking information and service routes.",
       hi: "आधिकारिक माल बुकिंग जानकारी एवं सेवा मार्ग।"
     },
     fileName: "balaji-profile-2026.pdf",
     fileSize: "PDF Document (1.2 MB)",
     uploadDate: "2026",
     isAvailable: true
   }
   ```
4. Save the file. The `/documents` page will instantly render the new document with View and Download buttons.

### Replacing Hero Image & Logo
* **Hero Image:** Replace `public/images/hero-truck.jpg` with an authentic transport photo.
* **Logo:** Replace `public/favicon.svg` or update the brand mark in `src/components/Header.jsx`.

---

## 5. Deployment Instructions (Vercel)

### SEO URL setting
After the first deployment, copy the exact production URL from Vercel and add it in Project Settings → Environment Variables:
- Key: `VITE_SITE_URL`
- Value: `https://your-exact-project.vercel.app` (no trailing slash)

Redeploy after saving. The build script creates `sitemap.xml` and `robots.txt` using this URL. Do not use a guessed URL; it must match the actual deployed domain.



### Option A: Via Vercel CLI
```bash
npm install -g vercel
vercel
```

### Option B: Via Vercel Dashboard (GitHub)
1. Push this project to your GitHub repository.
2. Sign in to [Vercel](https://vercel.com) and click **"Add New Project"**.
3. Import your repository. Vercel automatically detects **Vite**.
4. Set Build Command: `npm run build`
5. Set Output Directory: `dist`
6. Add Environment Variable:
   * Key: `VITE_API_BASE_URL`
   * Value: `https://api.yourdomain.com/api` (or leave empty for client demonstration mode)
7. Click **Deploy**.

For single-page client routing on Vercel, a `vercel.json` rewrite file is pre-configured:
```json
{
  "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }]
}
```

---

## 6. Future Backend Integration Blueprint (Node.js, Express & MySQL)

The frontend is architected to integrate seamlessly with a future Node.js/Express REST API without modifying UI components:

### API Endpoints Specification
1. **Contact & Booking Enquiry API:**
   * `POST /api/enquiries`
   * Request Payload: `{ name, phone, enquiryType, message, submittedAt, source }`
   * Response: `{ success: true, enquiryId: "BTC-1001" }`
2. **Document Management API:**
   * `GET /api/documents` — Fetch published verified documents dynamically.
   * `POST /api/admin/documents` — Secure admin upload for new PDF circulars.
3. **Future Consignment / LR Tracking:**
   * `GET /api/tracking/:consignmentNumber` — Look up goods receipt/consignment status.
4. **Admin Dashboard:**
   * Authenticated routes for managing inbound leads, enquiry triage, and route updates.

To connect the frontend:
1. In your `.env` file, set:
   ```env
   VITE_API_BASE_URL=https://api.balajitransport.com/api
   ```
2. The existing `src/services/contactService.js` and `src/services/api.js` modules will automatically route submissions to the live endpoint.

---

## 7. Quality & Verification Checklist

- [x] **Verified Facts Only:** No fabricated customer counts, fleet numbers, delivery guarantees, or fake tracking claims.
- [x] **Full Bilingual Support:** Instant client-side switching between Hindi and English with persistent selection.
- [x] **Click-to-Call Links:** Direct links to `tel:+919517137669` and `tel:+917668744025`.
- [x] **Direct WhatsApp Links:** `https://wa.me/919517137669` and `https://wa.me/917668744025` with prefilled enquiry text.
- [x] **Google Maps Navigation:** Non-hallucinated search link targeting Mehdawel, Sant Kabir Nagar, Uttar Pradesh.
- [x] **Client Validation:** Form enforces 10-digit Indian numbers, required names, and category selection.
- [x] **Responsive Mobile Layout:** Accessible hamburger drawer on mobile, responsive grids on tablet and desktop.
- [x] **Document Safety:** Empty state with admin instructions; no nonfunctional download links.
