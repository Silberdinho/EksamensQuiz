# EksamensQuiz

Quiz and flashcard trainer for my NTNU Information Security courses (autumn 2026):

| Course | Exam |
|---|---|
| IMT4110 – Scientific Methodology and Communication | 26 Nov 2026 |
| IMT4115 – Introduction to Information Security Management | 11 Dec 2026 |
| IMT4113 – Introduction to Cyber and Information Security Technology (final) | 17 Dec 2026 |
| IMT4133 – Data Science for Security and Forensics | 30 Nov 2026 |

Open `index.html` in a browser. Everything is in one file; no build step.

## Features
- Home page with countdown and progress per course
- Topic cards per lecture (PowerPoint), quiz or flashcards per topic
- "All topics", "Former exam questions only" (⭐) and "Practice my mistakes"
- Essay questions (IMT4115) with key points and model answer
- Shuffle, score at the end of each round, works on phone and computer
- Progress is saved in the browser (localStorage)
- **Terms quiz** per course: key terms by chapter (lecture order), term → definition, definition → term and flashcards; wrong options are other terms from the same chapter
- **Key models**: 84 interactive diagrams (SVG, drawn in code) for the most important topics, shown at the top of each chapter, after answering linked questions and on the back of linked flashcards; tap a part of a model to see what it means
- Celebration when you finish a chapter with 80% or more
- Back up progress: download a backup file or copy a backup code, and restore it in any browser (home page)

## Structure of `index.html`
1. `<head>` – design (CSS tokens, one colour per course)
2. **Question data** – one `<script>` block per course (`COURSES.push({...})`)
3. **Terms data** – one `<script>` block per course (`TERMS.push({...})`)
4. **Visuals** – a small SVG engine (`V.*` builders) and one block of diagrams per course (`VIS.push({...})`)
5. **App logic** – the last `<script>` block (no course content)

### Question format
```js
{ t: "topic-id", k: "mc" | "def" | "case" | "tf" | "calc" | "essay",
  q: "Question", o: ["A", "B", "C", "D"], a: 0,   // index of correct option
  e: "Short explanation", x: "2024 Q7",           // optional: former exam tag → ⭐
  chk: true,                                      // optional: "Needs checking"
  kp: ["key point", ...], m: "model answer" }     // essay only
```

### Terms format
```js
TERMS.push({ code: "IMT4110", chapters: [
  { t: "topic-id", terms: [
    { n: "Term", d: "Short definition", ex: "Example (optional)", x: "Ex-4", chk: true } ] } ] });
```
Chapters use the topic ids, so they follow the lecture order. Each chapter needs at least 4 terms.

### Visual format
```js
VIS.push({ c: "IMT4110", t: "topic-id", id: "unique-id", icon: "🔄", title: "Title", x: "Ex-4",
  draw: () => V.flow([{ k: "part", l: "Label", s: "Sub-label" }]),   // or V.cycle, V.grid, V.compare, V.stacks, V.seq, V.rings
  info: { part: "What this part means" },                              // shown when a part is tapped
  fact: "Did you know?",
  q: ["question text pattern"], terms: ["Term name"] });               // where the visual appears after answering
```

## Adding a course
Push one more `COURSES` block (and optionally a `TERMS` block) in the same format.
