# Respiratory Study OS — Documentation
**Batch 62 · Al-Azhar University**
**Live:** https://resp-exam-os.vercel.app
**GitHub:** https://github.com/sohailcollege2032008-tech/resp-exam-os

---

## Overview

A static web app that aggregates all Respiratory module study files in one place. No login, no server — everything runs in the browser. Progress is saved automatically per device using `localStorage`.

---

## Site Sections

| Section | Files | Questions |
|---|---|---|
| 📋 كتاب القسم | 7 dept book files | ~402 |
| 📅 السنين السابقة | 7 previous exam files | ~373 |
| 📚 مجمع MCQ بالمادة | 8 subject-grouped files | ~373 (same Qs, different view) |
| 📄 الشيتات | 2 sheets | ~29 |
| **Total unique** | **16 files** | **~804** |

> The "by subject" section contains the same questions as "by exam" — just regrouped by subject. The grand total shown in the hub counts each question once.

---

## Hub Page Features

### Progress Bar (top nav)
Shows overall percentage of answered questions across all files (unique files only, not by-subject duplicates).

### Summary Bar
| Stat | Meaning |
|---|---|
| أسئلة أُجيبت | Total questions answered across all files |
| سؤال فريد | Total unique questions in the module |
| ملفات ✓ | Files you manually marked as "✓ تمام" |
| محفوظ ★ | Total starred questions across all files |

### Card Status Badges
Click the status button on any card to cycle through:

| Badge | Meaning |
|---|---|
| — | Not started |
| مراجعة | In progress / reviewing |
| ✓ تمام | Done |
| ⚠ ضعيف | Needs more work |

Status is saved per device. Progress bars update every 30 seconds automatically.

### Download Button (⬇)
Downloads the HTML file to your device for offline use.

---

## Inside Each Study File

Each HTML file has three study modes (switch from the top nav):

| Mode | Behavior |
|---|---|
| **Study** | Answer shown immediately, Arabic explanation visible |
| **Test** | Click an option → reveals if correct/wrong → then show explanation |
| **Marker** | Correct answer highlighted in yellow, no explanation shown |

### Filters (filter bar below nav)
- **All / Wrong / Correct / Starred / Unanswered** — filter visible questions
- **Retry** button appears when "Wrong" or "Starred" filter is active — re-solves only those questions in-place without losing the rest of your progress

### Settings Panel (⚙️)
- Font size (S / M / L / XL)
- Content width (600–1200px)
- Arabic font family
- Explanation color theme

### New Attempt vs Full Reset
- **New Attempt** (`▶`) — clears answers only, keeps stars, theme, settings
- **Full Reset** (`↺`) — clears everything including settings and stars

All settings persist in `localStorage` per file.

---

## File Map

```
index.html              ← Hub page (this site's homepage)
dept-bio.html           ← بيوكيمستري القسم
dept-histo1.html        ← هستو القسم — ج١
dept-histo2.html        ← هستو القسم — ج٢
dept-micro.html         ← مايكرو القسم
dept-para.html          ← بارا القسم
dept-pharma.html        ← فارما القسم
dept-physio.html        ← فسيو القسم
exam-61.html            ← امتحان 61
exam-end-mod-57.html    ← إند موديول 57
exam-end-sem-55.html    ← إند سميستر 55
exam-form-55.html       ← فورماتيف 55
exam-dor-55.html        ← دور تاني 55
exam-55-p1.html         ← امتحان 55 — ج١
exam-55-p2.html         ← امتحان 55 — ج٢
subj-anatomy.html       ← أناتومي (prev years grouped)
subj-physio.html        ← فسيولوجيا (prev years grouped)
subj-pharma.html        ← فارماكولوجيا (prev years grouped)
subj-histo.html         ← هستولوجيا (prev years grouped)
subj-patho.html         ← باثولوجيا (prev years grouped)
subj-micro.html         ← مايكرو (prev years grouped)
subj-para.html          ← باراسيتولوجيا (prev years grouped)
subj-bio.html           ← بيوكيمستري (prev years grouped)
sheet-patho-mcq.html    ← شيت باثو MCQ
sheet-micro-written.html← شيت مايكرو ريتن
vercel.json             ← Vercel config (cleanUrls: true)
```

---

## How to Update

When new HTML files are added or existing ones are rebuilt:

```bash
cd "D:/Projects/study for the exam"

# 1. Rebuild the deploy folder
python build_resp_deploy.py

# 2. Push to GitHub (Vercel auto-deploys on push)
cd resp-exam-os
git add .
git commit -m "update: <description>"
git push
```

> Vercel is connected to the GitHub repo — every push to `main` triggers an automatic deployment. No manual Vercel steps needed.

To add a new file to the hub, edit `DEPT_MAP`, `EXAM_MAP`, `SUBJ_MAP`, or `SHEETS_MAP` in `build_resp_deploy.py`, then rebuild and push.

---

## Tech Stack

- **Pure static HTML/CSS/JS** — no framework, no build step
- **localStorage** — progress storage, no backend needed
- **Vercel** — hosting (free tier, static)
- **GitHub** — source: `sohailcollege2032008-tech/resp-exam-os`
- **html_template_v2.py** — shared engine that generates all study HTML files
