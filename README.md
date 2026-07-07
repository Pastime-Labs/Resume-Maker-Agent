# Resume Maker Agent

manually tweaking your resume for every single job application is exhausting. This project automates the entire process using a squad of cooperative AI agents powered by **CrewAi** and **Google Gemini 2.5 Flash**. 

Give it a job description and your raw profile text, and the agents will rewrite your experience to match the role perfectly—exporting everything into a clean, presentation-ready Markdown (`.md`) file.

---

## How the Crew Works

Instead of asking a single AI prompt to do everything (which usually results in generic fluff), this pipeline splits the work across four distinct, specialized agents:

1. **The Market Analyst (Recruiter Agent):** Reads the job description to figure out what the hiring manager is *actually* looking for, mapping out the non-negotiable tech stack and the core engineering problems the team is facing.
2. **The Career Coach (Strategist Agent):** Rewrites your experience bullets using **Google's X-Y-Z formula** (*Accomplished [X], measured by [Y], by doing [Z]*). It swaps out passive phrases for punchy, impact-driven statements.
3. **The ATS Engineer (Optimizer Agent):** Makes sure the resume passes modern parsing filters (Workday, Greenhouse, etc.) by naturally weaving in missing technical keywords without making it look like spam.
4. **The Clean Designer (Formatter Agent):** Takes the optimized text and structures it into a pristine Markdown layout. It also acts as a guardrail to ensure your real personal data (like Name, Contacts, or College) never gets replaced by placeholder brackets.

---

## How Tasks Are Divided

The workflow is treated like a modern corporate assembly line. The output of one task feeds perfectly into the next:

```text
[Raw Input] ──> (Task 1: Deconstruct JD) ──> (Task 2: Rewrite to X-Y-Z) ──> (Task 3: Optimize ATS Keywords) ──> (Task 4: Polish Layout) ──> [Final Markdown File]
```
1. **Task 1**: Job Specification Deconstruction: The Recruiter Agent analyzes the target job description to extract the mandatory technical stack, core engineering problems, and latent hiring signals.
2. Task 2: Profile Transformation: The Strategy Agent takes your raw background text and matches it against Task 1's findings, converting flat descriptions into high-impact X-Y-Z bullet points.
3. Task 3: Keywords & ATS Alignment: The Compliance Agent audits the rewritten profile to make sure key semantic terms are naturally integrated so the resume doesn't get instantly filtered out by automated screening systems.
4. Task 4: Markdown Layout Design: The Formatter Agent takes the final optimized copy and builds a beautiful, readable Markdown structure, ensuring critical fields (like your Name or Contact info) are cleanly preserved without weird placeholder brackets.

---

## Tools

**ScrapeWebsiteTool** (Assigned to recruiter agent): Instead of forcing you to manually copy and paste long, messy text from a web page, the Recruiter Agent watches the job_input. If it detects an incoming URL (http:// or https://), it automatically spins up the scraper to extract clean text straight from the job listing link.

**SerperDevTool** (Assigned to recruiter agent): If a job description mentions a highly proprietary company tool or a vague internal architecture problem, the Recruiter Agent uses this tool to search the live web. It gathers supplemental market intelligence about the company's engineering ecosystem before building the blueprint.

**FileReadTool** (Assigned to strategy agent): This tool provides modular flexibility for your raw profile. The Strategy Agent evaluates your profile_input. If you pass a local file path string (like documents/my_old_resume.txt), it bypasses raw text variables and parses the file directly from your system.


## Setup

1. Clone the Repo
2. Install the Requirements(pip install -r requirements.txt)
3. Add Your API Key
   (**If running locally**: Duplicate the .env.example file, rename it to .env, and paste your key , GEMINI_API_KEY=your_key)
   (**If running in Google colab**: Add your key to Colab's Secrets panel with the name GEMINI_API_KEY and toggle on "Notebook access".)
