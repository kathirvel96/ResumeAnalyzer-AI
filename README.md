# Smart Resume Reviewer & ATS Matcher

A single-page web app that compares your resume against a job description and shows how an Applicant Tracking System (ATS) is likely to read it. You get a match score, the keywords you are missing, and a prioritized list of fixes.

Everything runs in the browser. Your resume is never uploaded or stored.

**Live demo:** https://claude.ai/artifact/6f1JABGQVBb9G98mjdP1CG

## Features

- **ATS score (0 to 100)** with an animated ring and a short verdict
- **Keyword matching** between the job description and your resume, shown as matched and missing chips
- **Resume health checks** for Summary, Experience, Education and Skills sections, contact details, profile links, measurable results and weak phrases
- **Prioritized fixes** that tell you what to change first
- **File upload** for PDF, Word (.docx) and .txt, or paste text directly
- **Toast alerts** for success, warnings and errors, with clear messages for empty fields, unsupported files, large files and scanned PDFs
- **Animations** for the score ring, progress bars, chips, result cards and field validation
- **Light and dark theme** toggle, plus automatic dark mode from your system setting
- **Responsive layout** that works on phones, tablets and desktops
- **Accessible** with visible keyboard focus, live regions for alerts, and reduced-motion support

## Tech stack

| Part | Used for |
| --- | --- |
| HTML5 | Page structure |
| CSS3 | Layout, theming with CSS variables, animations |
| JavaScript (vanilla) | Analysis, file reading, alerts, rendering |
| Bootstrap-style classes | `container`, `row`, `btn`, `card`, `form-control` |
| [PDF.js](https://mozilla.github.io/pdf.js/) 3.11.174 | Extracting text from PDFs |
| [Mammoth](https://github.com/mwilliamson/mammoth.js) 1.6.0 | Extracting text from .docx files |
| Manrope (Google Fonts) | Typography |

## Getting started

1. Download `resume-ats-matcher.html`.
2. Open it in any modern browser. No build step or server is needed.
3. Paste or upload your resume, paste a job description, and click **Analyze match**.

Click **Load sample** to try it with example data.

## How the score works

The final score is a weighted sum of five parts, minus a small penalty for weak phrases.

| Part | Weight | Full marks when |
| --- | --- | --- |
| Keyword match | 50% | Every keyword from the job description appears in the resume |
| Structure and contact | 20% | Summary, Experience, Education, Skills, email and phone are all present |
| Measurable impact | 15% | At least 5 results with numbers (percentages, money, user counts) |
| Action verbs | 10% | At least 6 different strong verbs (built, led, optimized, and so on) |
| Length | 5% | Between 300 and 900 words |

- Each weak phrase found (for example "responsible for" or "worked on") subtracts 2 points.
- 75 and above is a strong match, 50 to 74 is decent, and below 50 needs work.

**How keywords are found:** the app looks for about 55 common skills and tools in the job description, then adds up to 8 other terms that appear at least twice. Common filler words are ignored.

## Using the file upload

| Format | Supported | Notes |
| --- | --- | --- |
| PDF | Yes | Text-based PDFs only. Scanned or image-only PDFs have no readable text. |
| Word (.docx) | Yes | |
| Text (.txt) | Yes | |
| Word (.doc) | No | Save as .docx or PDF first. |

- Maximum file size is 10 MB.
- Extracted text appears in the resume box so you can check and edit it before analyzing.
- Resumes with multi-column layouts can come out in a jumbled order from PDFs. Review the text before you rely on the score.

## Using real Bootstrap

The demo uses Bootstrap-style class names with equivalent CSS written inline, so it works as a single file with no external stylesheet. To use the real framework in your own project, add this to the `<head>`:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
```

Then replace the inline `.container`, `.row`, `.btn` and `.card` rules with Bootstrap's own classes.

## Customizing

All of these are near the top of the `<script>` block.

- **Skills list:** edit the `SKILLS` array to add terms for your industry.
- **Ignored words:** edit the `STOP` set.
- **Action verbs:** edit the `VERBS` array.
- **Weak phrases:** edit the `WEAK` array.
- **Colors:** change the CSS variables in `:root` (light) and the dark theme blocks.
- **Score weights:** change the formula inside the `analyze()` function.

## Limitations

- Scoring is a keyword and structure heuristic. It does not reproduce any specific ATS, and real systems vary.
- Matching is exact, so "JS" will not match "JavaScript". Add synonyms to your resume where they are honest.
- Only add keywords you can back up with real experience.

## Browser support

Current versions of Chrome, Edge, Firefox and Safari.

## License

Free to use and modify for personal and commercial projects.
