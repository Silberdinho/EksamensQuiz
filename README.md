# EksamensQuiz

Quiz and flashcard trainer for my NTNU Information Security courses (autumn 2026):

| Course | Exam |
|---|---|
| IMT4110 – Scientific Methodology and Communication | 26 Nov 2026 |
| IMT4115 – Introduction to Information Security Management | 11 Dec 2026 |
| IMT4113 – Introduction to Cyber and Information Security Technology (final) | 17 Dec 2026 |
| IMT4133 | Coming soon |

Open `index.html` in a browser. Everything is in one file; no build step.

## Features
- Home page with countdown and progress per course
- Topic cards per lecture (PowerPoint), quiz or flashcards per topic
- "All topics", "Former exam questions only" (⭐) and "Practice my mistakes"
- Essay questions (IMT4115) with key points and model answer
- Shuffle, score at the end of each round, works on phone and computer
- Progress is saved in the browser (localStorage)
- Back up progress: download a backup file or copy a backup code, and restore it in any browser (home page)

## Structure of `index.html`
1. `<head>` – design (CSS tokens, one colour per course)
2. **Question data** – one `<script>` block per course (`COURSES.push({...})`)
3. **App logic** – the last `<script>` block (no course content)

### Question format
```js
{ t: "topic-id", k: "mc" | "def" | "case" | "tf" | "essay",
  q: "Question", o: ["A", "B", "C", "D"], a: 0,   // index of correct option
  e: "Short explanation", x: "2024 Q7",           // optional: former exam tag → ⭐
  chk: true,                                      // optional: "Needs checking"
  kp: ["key point", ...], m: "model answer" }     // essay only
```

## Adding a course (e.g. IMT4133)
Replace the IMT4133 block: set `status: "active"`, fill in `exam`, `topics` and `questions` in the same format.
