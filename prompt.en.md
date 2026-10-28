# Create a SaaS Application Called Grounded (Functional MVP)

## 1. PRODUCT VISION AND TOP PRIORITY

Grounded is a resume optimization platform designed for job application processes.

- The application must be 100% functional from the very first generation, running entirely in the browser (client-side) without relying on external AI services or backend integrations to deliver its initial value.
- No authentication or registration required: users should be able to access and use the platform immediately.
- History and clips must be stored in `localStorage` to ensure persistence across page refreshes.

## 2. DESIGN SYSTEM AND VISUAL IDENTITY

- Name: Grounded
- Slogan: "Turn job openings into opportunities."
- Style: Inspired by Notion, Linear, and Stripe Dashboard (minimalist, professional, rounded corners, and soft shadows).
- Components: Use exclusively shadcn/ui components and Lucide icons.
- Colors:
  - Primary: #6D1F33 (Burgundy)
  - Earth Brown: #8B5E3C
  - Concrete Gray: #A7A6A1
  - Charcoal: #3A3A3A
  - Light Beige: #EAE3D9
  - Default Background: #F7F3EE (Light mode with Dark mode support).
- Internationalization (i18n): Global language selector at the top of the application allowing users to switch between Portuguese (Brazil) and English (US).

## 3. HOMEPAGE (ONBOARDING & INSTANT TESTING)

Create a featured section called **"Try It in 30 Seconds"**:

- Two pre-configured job posting buttons:
  - 🏢 Test with a Microsoft Job Posting (Software Engineer)
  - 💜 Test with a Nubank Job Posting (Product Engineer)

- Quick resume button:
  - 📄 Load Sample Resume (Realistic Full Stack Developer)

When users click these buttons, the corresponding forms must be automatically populated with sample data.

### Manual Input Fields

- Job Posting:
  - URL input field
  - Alternative textarea with the placeholder:
    **"Or paste the full job description here"**

- Resume:
  - Upload area (simulated PDF/DOCX upload)
  - Button to paste/edit structured resume content

- Main Action Button:
  - **"Analyze ATS Compatibility"**

## 4. LOCAL ATS ENGINE (CLIENT-SIDE)

Implement decoupled TypeScript services (`AtsAnalyzer` and `ResumeOptimizer`) that:

- Extract keywords and skills from job descriptions (e.g., React, TypeScript, Azure, CI/CD, Docker, Git).
- Compare job requirements against the candidate's skills and experience.
- Calculate an ATS Score from 0% to 100% based on the matching rate.
- Separate results into:
  - ✅ Matched Skills (green badges)
  - ❌ Missing Skills (red warning badges)
- Generate rule-based recommendations, such as:
  - "Docker appears in the job description but not in the resume."
  - "Highlight your TypeScript projects more prominently."

## 5. OPTIMIZED RESUME GENERATOR AND COMPARISON TOOL

The system must generate an optimized version of the resume without fabricating or hallucinating information.

Features:

- Prioritize and move matching skills to the top of the resume.
- Reorder work experience and projects to highlight relevant technologies and competencies.
- Comparison screen using tabs or side-by-side columns:
  - Original Resume vs. Optimized Resume
  - Include a visual diff showing highlighted and reordered content.
- "Export" button:
  - ATS-friendly layout optimized for recruiters and Applicant Tracking Systems.
  - Trigger PDF generation through browser printing (`window.print()`).

## 6. CIVI ASSISTANT (LOCAL CHAT)

Create a side chat panel featuring the assistant **"Civi"**.

The chat should include clickable quick questions such as:

- "Why is my score X%?"
- "How can I improve for this position?"
- "Which skills should I prioritize learning?"
- "What am I missing for this role?"

Responses must be generated using only the results from the locally calculated ATS analysis.

## 7. RESUME CLIPS AREA AND DASHBOARD

- Every saved analysis becomes a **"Clip"**, combining:
  - Job Posting
  - Optimized Resume
  - Status (Optimized, Under Analysis, Exported)

- The application should start with 3 sample clips already stored in the user's history.

### Dashboard

Display KPIs including:

- Analyzed Job Postings
- Average ATS Score
- Optimized Resumes

Include a Recharts visualization comparing:

- Most Requested Skills
- Most Frequently Missing Skills