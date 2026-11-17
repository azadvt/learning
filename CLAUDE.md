# CLAUDE.md — Learning repo

Personal knowledge base. **Current priority: passing the MSc Computer Science exams.** Most requests in this repo will be exam study help: writing answer sheets, explaining topics, quizzing, marking answers and building study pages.

---

## 1. Student context

- **Course:** M.Sc. Computer Science, **SDE (School of Distance Education), University of Kerala**, 2017-admission-onwards scheme (course codes `DCSxx`).
- **Time:** only a few days to study, so be efficient and exam-focused.
- **Registered exams. Only these matter; ignore all other subjects.**

| Exam date (Nov 2026) | Code | Subject | Folder |
|---|---|---|---|
| Mon 23 Nov | DCS31 | Data Mining & Warehousing | `msc-cs/semester-3/DCS31-data-mining-warehousing/` |
| Fri 27 Nov | DCS33 | Information Security | `msc-cs/semester-3/DCS33-information-security/` |
| Wed 2 Dec | DCS35B | Digital Image Processing (Elective I) | `msc-cs/semester-3/DCS35B-digital-image-processing/` |
| Fri 4 Dec | DCS41 | Research & Technical Writing | `msc-cs/semester-4/DCS41-research-technical-writing/` |
| Mon 7 Dec | DCS42C | Neural Networks & Fuzzy Systems (Elective II) | `msc-cs/semester-4/DCS42C-neural-networks-fuzzy-systems/` |

Official timetable (Univ. of Kerala, approved 13-Nov-2026): 1.30–4.30 pm, but **Fridays 2.00–5.00 pm**. Details and study plan: `msc-cs/timetable/README.md`.

- **Not registered:** DCS32 (Distributed Systems & Cloud) and DCS34 (Compiler Design). Don't write material for them unless asked.
- Write in **simple, clear English**: short sentences, no unnecessary jargon. Define a term the first time you use it.

## 2. Exam pattern (every paper)

- **3 hours, 75 marks.** The pass mark is unconfirmed; don't state a number unless the student provides it.
- **Part A:** 9 questions × 3 marks = 27. Answer **all**. Usually 3 questions per module.
- **Part B:** 3 questions per module; answer **any 2 per module**. 6 × 8 = 48.
- Each subject has **3 modules**. The modules are defined in `msc-cs/syllabus.pdf`.

**Strategy:** knowing 2 strong long answers per module secures Part B. Part A rewards broad, short coverage.

## 3. Sources of truth

| File | Use |
|---|---|
| `msc-cs/syllabus.pdf` | **The authoritative syllabus.** Every topic listed here must be covered. |
| `msc-cs/question-papers/` | Past papers (see its `README.md` index). Use them **only to understand the pattern and emphasis**. |
| `<subject>/README.md` | Syllabus per module, past questions grouped by module, references |
| `<subject>/exam-answers.md` | The main study sheet (see §4) |
| `<subject>/module-N/notes.md` | Older detailed notes (DCS31 only, so far) |

**Rule: cover the complete syllabus.** The student said past papers are "just reference, that is pattern". Never limit material to repeated questions. Past questions decide **priority and order**, not **scope**.

When the student adds new papers (usually to `~/Downloads`):
1. Hash them against `msc-cs/question-papers/*.pdf` and skip duplicates.
2. Read every new PDF and identify the exam, date and subjects.
3. Rename it as `YYYY-mon-semN-subjects.pdf`, move it into `msc-cs/question-papers/` and update its `README.md`.
4. Check the scans for **other students' names or registration numbers** and warn before pushing.
5. Report which new questions are **not yet covered** by the subject's `exam-answers.md`, and offer to add them.

## 4. Answer sheet format (`exam-answers.md`)

One file per subject, in its subject folder. `DCS31` and `DCS35B` are the reference examples. Copy their structure.

**File structure, in order:**
1. Title + a "How to use" note + the ⭐ legend + a line naming the most-asked topics.
2. **Syllabus coverage checklist:** a table of every syllabus topic → where it is answered (`Q#`, or `Notes M# §#`). Nothing in the syllabus may be missing from it.
3. `# MODULE 1`, `# MODULE 2` and `# MODULE 3` sections with numbered long answers (`## Q1.` …).
4. Extra long answers (for example "MORE 8-MARK ANSWERS"), when added later.
5. `# PART A — Short answers (3 marks each)`.

**Every 8-mark answer must have:**
- A heading line `## Q#. ⭐ <question in exam wording>`, followed by `**Asked:** <paper(s) + part>` when it has been asked before.
- A one- or two-line **definition / introduction**.
- **6–10 headed points or steps**. This skeleton is what the student memorizes.
- **At least one** ASCII diagram, table, formula or algorithm block (inside a code fence when it's a diagram).
- **A worked example** for anything numerical (k-means, Bayes, info gain, DES rounds, histogram equalization, perceptron updates, and so on).
- A short conclusion or advantages/disadvantages when relevant.
- About a page long. It must be **writable in about 20 minutes by hand**.

**Every Part A answer:** bold the question, then 2–4 lines of answer. Refer to the long answer (`see Q#`) when one exists.

**⭐ markers:**
- ⭐ = asked in at least one past paper, test paper or assignment
- ⭐⭐ = asked in two or more
- Only mark questions that really appear in the files in `msc-cs/question-papers/`. **Never invent past-paper history.**

## 5. Accuracy rules

- **Recompute every worked example** (distances, probabilities, entropies, matrix steps) before saving. A wrong number in a study sheet costs marks.
- Use standard textbook definitions and notation from the syllabus references, for example Han and Kamber for DCS31, Gonzalez and Woods for DCS35B, and Mark Stamp for DCS33.
- If unsure about a fact, say so instead of guessing.
- Don't claim exam dates, pass marks or rules that the student hasn't confirmed.

## 6. Tutoring modes

Recognize these requests and behave accordingly:

| Student says… | Do this |
|---|---|
| "Explain X" / "I don't understand X" | A simple explanation first, then an analogy, then a small example. Keep it short and offer to go deeper. |
| "Quiz me on …" | Ask **one question at a time**, wait for the answer, then give feedback: what was right, what was missing, and the correct points. Track the score. Mix Part A and Part B styles. |
| "Check / mark my answer" (text or photo) | Mark like a university examiner, **out of 3 or 8**. List the points awarded, the points missing, and how to get full marks. Be honest; don't inflate marks. |
| "Give me a problem" | A new numerical in the exam style. Let the student solve it, then show the full working. |
| "Mock paper" | A new paper in the exact pattern in §2. Don't copy past questions verbatim; cover all 3 modules. Mark it when the student submits answers. |
| "Make a plan" | Ask for the days left and hours per day if unknown. Plan module by module: learn → write the skeleton from memory → check. End with Part A and a timed mock. |
| "Cheat sheet / formulas" | A one-page summary: formulas, diagrams and key definitions only. |

Prioritize **active recall** (quizzing, writing from memory) over re-reading.

## 7. Study pages (Artifacts)

The student wants an interactive study page they can open on their **phone**. Build it as a claude.ai **Artifact**, and optionally save a copy as `<subject>/study.html` for offline use.

Required features:
- **One page per subject** (or one page with subject tabs). **Module tabs** M1, M2, M3.
- Each long answer is a card showing the **question first**. Tapping it **reveals the answer** (active recall).
- A **"Learned ✓"** toggle on each card and a **progress bar per module**. Persist progress per viewer.
- **Part A flashcards** (question → tap to flip).
- **Priority badges** (⭐ / ⭐⭐), plus a filter for "most-asked first".
- A **formula sheet** view.
- **Mock exam mode**: a random paper (9 Part A + 3 per module) with a **3-hour timer**.
- **Mobile-first**: readable on a phone, with a 16 px gutter and no horizontal scrolling. Light and dark themes.
- Content comes **only from that subject's `exam-answers.md`**. Don't write new or different answers in the page. Update the markdown first, then rebuild the page.

## 8. Repo conventions

- Folders are `msc-cs/semester-N/<CODE>-<kebab-name>/`. Keep the file names `README.md`, `exam-answers.md` and `module-N/notes.md`.
- Commit messages are short and lower-case, for example `add DCS33 exam answer sheet` or `DCS31: add Bayes and temporal mining answers`.
- **Commit after each meaningful change. Push only when the student asks.** The student pushes to `origin master` (GitHub). If a push is blocked, tell them to run `! git push origin master`.
- Don't delete the student's files. Downloads are moved into the repo only after the duplicate check in §3.
