# Vishwas — Our Voice Matters

> **Civic Issue Reporting, Tracking & Community Verification Platform**  
> *"Our Voice Matters"*

---

## 1. Project Overview

**Vishwas** is a community-powered civic-tech platform that empowers ordinary citizens to report local civic issues, track municipal progress in real time, and independently verify whether reported problems have actually been resolved on the ground.

Traditional grievance portals stop the moment an official clicks *"Closed"*. Vishwas introduces an independent **Community Verification Protocol**: an issue is only certified as **"Community Verified"** when **at least three independent local residents** inspect the repair and endorse it with photographic proof.

### Supported Civic Categories
- **Road Damage:** Potholes, broken asphalt, cave-ins, and dangerous road craters.
- **Waste Management:** Overflowing secondary dumpsters, delayed trash collection, and scattered garbage.
- **Streetlights:** Dark pedestrian corridors, faulty lamps, and exposed electrical cables.
- **Water Leaks:** Fractured underground pipelines, open valves, and potable water wastage.
- **Public Facilities:** Damaged footbridges, unsafe park equipment, and broken bus shelters.
- **Other:** Local community hazards and infrastructure grievances.

---

## 2. Technology Stack & Architecture

- **Frontend Core:** React 18, Vite 6, Modern Vanilla CSS (tailored navy, civic teal, and off-white design system).
- **Icons:** Lucide React (`lucide-react`).
- **Database & Auth:** Supabase PostgreSQL with Row Level Security (RLS) policies, phone OTP authentication, and Storage buckets for evidence media.
- **Deployment Ready:** Vercel / GitHub.
- **Location Hierarchy:** Structured Indian administrative dataset covering 28 States, 8 Union Territories, filtered districts, verified Municipal Corporations, Municipalities, and Gram Panchayats.

---

## 3. How to Run the Project Locally

### Prerequisites
- Node.js (v18 or higher recommended, tested on Node v26)
- npm (v9 or higher)

### Installation & Launch
```bash
# 1. Install dependencies
npm install

# 2. Start the Vite development server
npm run dev
```

Open your browser at:
```
http://localhost:5173/
```

### Production Build
```bash
npm run build
npm run preview
```

---

## 4. Supabase Setup Guide (Backend & PostgreSQL)

Vishwas is designed to run in two seamless modes:
1. **Interactive Demo Mode (Default):** Runs immediately out of the box with persistent local storage and realistic Indian civic issues.
2. **Live Supabase Mode:** Connects to your PostgreSQL database with full Row Level Security (RLS) policies.

### Step-by-Step Supabase Setup
1. Create a free project at [supabase.com](https://supabase.com).
2. Open the **SQL Editor** in your Supabase Dashboard.
3. Open the file [`supabase/schema.sql`](file:///c:/Users/abhin/OneDrive/Desktop/ANTIGRAVITY%20PROJECTS/Vishwas%20Our%20Voice%20Matters/supabase/schema.sql) in this repository, copy its entire contents, paste it into the Supabase SQL Editor, and click **Run**.
4. Retrieve your credentials:
   - Go to **Project Settings** → **API**.
   - Copy **Project URL** and **Project API Key (anon/public)**.
5. Either:
   - Click the **"Supabase Settings & SQL"** button in the top banner of the Vishwas app and paste your credentials directly into the UI; **OR**
   - Create a `.env` file in the project root:
     ```env
     VITE_SUPABASE_URL=https://your-project-ref.supabase.co
     VITE_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
     ```

---

## 5. Key Civic Features

### A. Structured 4-Tier Location Selector
Rather than requiring users to drop a pin on an unconfigured map, Vishwas uses a structured administrative location hierarchy:
1. **State / UT:** Searchable dropdown of all 36 Indian States and Union Territories.
2. **District:** Searchable suggestions strictly filtered according to the selected State (auto-clears if the State changes).
3. **Municipality / Gram Panchayat:** Filtered verified local body suggestions (Municipal Corporations, Town Municipal Councils, Gram Panchayats) or free-text with an *"Unverified Typed Entry"* badge.
4. **Local Place Name with Landmark:** Free-text field (e.g., *"Near the main bus stop, opposite the public library"*).

### B. Community Confirmation of Existing Reports (+1)
Prevents duplicate identical tickets. When multiple neighbors encounter the same pothole or broken streetlight, they click **"+1 Confirm This Issue Exists"**, raising its civic urgency score.

### C. Authority Resolution with Evidence
Verified municipal engineers or representatives submit:
- Detailed resolution and materials note
- Post-repair photographic proof

The issue status transitions to: **"Awaiting Community Verification"**.

### D. The 3-Resident Verification Standard
- Local residents review the authority's before-and-after photographic evidence.
- Residents vote:
  - **"Yes, Problem is Resolved"** (requires 3 independent endorsements to reach **"Community Verified"**)
  - **"Still Unresolved"** (instantly flags the issue as **"Disputed — Under Review"** and escalates it to the civic moderation cell).

### E. Timestamped Audit Trail
Maintains an immutable chronological record of:
- Citizen report submission
- Moderator triage and verification
- Authority dispatch and deployment
- Official repair evidence
- Resident verification votes and dispute comments

---

## 6. Project Directory Layout

```
├── .env.example              # Sample environment configuration
├── index.html                # Entry HTML with Outfit & Plus Jakarta Sans fonts
├── package.json              # Project dependencies & scripts
├── vite.config.js            # Vite configuration
├── supabase/
│   └── schema.sql            # PostgreSQL schema, RLS policies & triggers
└── src/
    ├── main.jsx              # React app entry point
    ├── App.jsx               # Main router & modal controller
    ├── index.css             # Navy, teal & off-white civic design system
    ├── data/
    │   ├── indiaLocations.js # States, districts, and local body datasets
    │   └── initialDemoData.js# Preloaded realistic civic issues & audit history
    ├── lib/
    │   └── supabaseClient.js # Supabase client wrapper & dynamic credential manager
    ├── context/
    │   ├── AuthContext.jsx   # Phone OTP authentication & test role switcher
    │   └── IssueContext.jsx  # Issues CRUD, confirmations & verification logic
    ├── components/
    │   ├── Navbar.jsx        # Sticky navigation with branding & test role selector
    │   ├── Footer.jsx        # Civic accountability footer
    │   ├── AuthModal.jsx     # Phone OTP login modal & demo login
    │   └── SupabaseConfigModal.jsx # In-app Supabase connection wizard
    └── pages/
        ├── HomePage.jsx      # Hero ("Our Voice Matters"), live stats, recent issues
        ├── ExploreIssuesPage.jsx # Multi-facet search & filtering
        ├── ReportIssuePage.jsx   # 4-tier structured location reporting form
        ├── IssueDetailPage.jsx  # Complete detail view, authority proof, voting
        ├── ModeratorDashboard.jsx# Triage queue, duplicate linking & dispute review
        ├── AuthorityDashboard.jsx# Jurisdiction queue & resolution submission
        └── MyReportsPage.jsx     # Citizen submitted reports & confirmations
```

---

## 7. Security & Privacy Highlights

- **Row Level Security (RLS):** Policies prevent ordinary users from escalating their role or updating authority fields.
- **Privacy Protection:** Citizen phone numbers and personal contact information are never exposed on public issue pages.
- **Duplicate Prevention:** Database constraints enforce exactly one active confirmation and one active resolution vote per authenticated user.
- **No Secret Exposure:** Only public anonymous keys (`anon_key`) are used on the frontend; service-role keys are never embedded in client code.
