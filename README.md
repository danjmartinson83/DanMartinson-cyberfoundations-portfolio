# CyberVisionaries Institute (CVI) — Cyber Foundations Student Portfolio

**New here? Read [START-HERE.md](START-HERE.md) first — it walks you through your very first commit, step by step.**

This repository documents your hands-on learning through the **CyberVisionaries Institute Cyber Foundations (Tier I)** program.

This is your working portfolio — **not the instructor repository.** All lesson content and lab instructions live here, in your own repo — you never need to pull anything from an instructor repo.

New to GitHub in general (not just this repo)? See the [CVI GitHub Handbook](https://github.com/CyberVisionariesInstitute/cvi-github-handbook) for accounts, key terms, and how templates work.

## 1. Repository Purpose

This repository is:

1. A structured lab documentation workspace
2. A technical reflection journal
3. A growing cybersecurity portfolio
4. Evidence of hands-on capability you can show an employer

Everything committed here should reflect professional standards — this is the first thing a hiring manager might look at.

## 2. Repository Structure

Each week has its own folder:

```
week-0X/
├── README-week0X-root.md      (that week's overview, outcomes, and checklist)
├── notes.md                    (key concepts, in your own words)
├── reflection.md                (weekly reflection)
└── labs/
    ├── README-week0X-submissions.md   (submission guide for that week's lab(s))
    └── lab-0X-[name].md                (the actual lab file(s))
```

Plus two shared top-level folders used across every week:

- `projects/` — mini-projects and the Week 12 capstone
- `assets/` — screenshots, diagrams, and supporting images (organized by week, e.g. `assets/screenshots/week-02/`)

**Weeks 1 and 2 are already built for you** — `week-01/` and `week-02/` are already in this repo, ready to fill in. From Week 3 on, you create the next `week-0X/` folder yourself, matching this exact structure (`README-week0X-root.md`, `notes.md`, `reflection.md`, `labs/README-week0X-submissions.md`, `labs/lab-0X-....md`). No one hands you a `week-03` template — matching a convention consistently on your own is part of what's being evaluated.

## 3. Embedding Screenshots (Relative Paths Only)

When documenting labs, you'll often include screenshots of terminal output, certificate details, or command results.

**Step 1 — Store screenshots properly.** All screenshots go in `assets/screenshots/week-0X/` (adjust the week number). Don't store screenshots in the root directory.

**Step 2 — Embed using a relative path.** From a file in `week-0X/labs/`, reference an image like this:

```markdown
![Description](../../assets/screenshots/week-0X/filename.png)
```

**Do NOT use:**
- Absolute file paths from your computer (e.g. `C:\Users\YourName\Desktop\image.png`)
- Drag-and-drop links that reference your local machine
- Public URL links unless explicitly instructed

If your image doesn't render, your path is incorrect — fix it before submitting.

## 4. Weekly Workflow

1. Review that week's `README-week0X-root.md` for the overview, outcomes, and checklist
2. Complete the lab in the Lab Portal — for lab weeks, submitting there writes your work directly into `week-0X/labs/`. You can also open the file there and fill it in yourself.
3. Summarize key concepts in your own words in `week-0X/notes.md`
4. Submit your reflection in `week-0X/reflection.md`
5. Commit with a clear, professional message — see that week's `labs/README-week0X-submissions.md` for exact commit instructions

## 5. Document Standards

Every entry should demonstrate:

1. Clear technical reasoning
2. Structured thinking
3. Concise explanations
4. Professional tone

Avoid vague summaries, copying definitions without understanding them, and single-word commit messages.

## About CVI

CyberVisionaries Institute builds sustainable, demonstrable technical capability in cybersecurity through structured training and mentorship. This portfolio reflects that progression.
