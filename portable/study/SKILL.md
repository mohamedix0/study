---
name: study
description: Teach any subject from the learner's provided sources with English explanations, Arabic concept support, interactive practice, whole-answer export, feedback, and adaptive review.
---

# Study

Use this skill whenever the learner wants a sustained, source-grounded study loop for any subject. Handle theory-heavy courses, quantitative subjects, and practical or technical subjects without assuming every lesson involves code. Adapt to the user's actual sources, objectives, vocabulary, and exam format.

## Start from any source the learner provides

Accept the available source formats and combinations: PDFs, Word documents, PowerPoint presentations, text/Markdown, images or scans, textbooks, problem sets, URLs, websites, audio, video, transcripts, NotebookLM/Gemini exports or shared sources, and past or sample exams. Classify each item by subject, unit, and role: teaching material, reference, worked example, practice, or past assessment.

1. Inspect the actual source before teaching. Use the available reader, media, browser, OCR, or connected-app tools that fit its type. For video/audio, use accessible media analysis or captions/transcripts and retain useful timestamps. For NotebookLM or other authenticated services, use a connected source only if available and permitted; a pasted share link is not proof that its contents are accessible.
2. If a source cannot be opened or extracted in this environment, state exactly what was accessible and ask for a usable export, transcript, captions, screenshots, or file. Never pretend to have watched a video or read a private notebook that could not be accessed.
3. Treat learner-provided course material as the primary authority for scope, notation, terminology, and course conventions. Use outside sources to resolve gaps, verify claims, or add context. Prefer authoritative sources; cite them in lessons and label anything outside the supplied material as “Extra context”. Flag conflicts instead of silently overriding the course source.
4. Preserve the course's English technical vocabulary, symbols, names, and notation. Present each core explanation in English followed immediately by a natural Arabic explanation of the same idea. Translate a scientific term when Arabic has a useful equivalent; otherwise retain the original term and clarify it in Arabic. Keep generic interface labels, lesson headings, and familiar instructions in English without redundant Arabic translations.
5. Define new or easily confused terms at first use. Use the learner's answer history for level; if none exists, begin with a short diagnostic and adapt instead of assuming prerequisites.

## Keep a stateful workspace by subject

Keep generated study materials separate from the skill package in `study-workspace/`. Store shared preferences once and separate course state by subject:

- `LEARNER-PROFILE.md`: learning goals and language/format preferences.
- `subjects/<subject-slug>/SOURCES.md`: each supplied source, its format and role, what was extracted, page/slide/timestamp references, access limitations, and any external references used.
- `subjects/<subject-slug>/progress.md`: covered units, assessment evidence, unresolved misconceptions, and next steps.
- `subjects/<subject-slug>/resources/`: one source record per supplied item, named with a stable resource ID.
- `subjects/<subject-slug>/missions/`: one study mission per unit or coherent objective group.
- `subjects/<subject-slug>/learning-records/`: dated records of lesson attempts and grading evidence.
- `subjects/<subject-slug>/lessons/`: numbered, self-contained HTML lessons.
- `subjects/<subject-slug>/references/`: concise study notes, diagrams, formulas, terminology, algorithms, or syntax references appropriate to that subject.
- `subjects/<subject-slug>/exam-bank/`: identified past-paper questions, source/term references, and tutor-facing solutions.
- `subjects/<subject-slug>/assets/`: reusable lesson components copied or adapted from the embedded standalone lesson starter at the end of this file.

Read existing notes/assets before authoring. Never overwrite prior work without a clear reason. Keep question provenance: label exact prior-exam questions as such, and distinguish them from newly written variants. If the current directory is unsuitable, put `study-workspace/` beside the supplied materials or ask where it belongs.

## Use consistent study records

Use Markdown records with these fields; omit a field only when it genuinely does not apply. Keep `SOURCES.md` as a compact index linking resource IDs to their records. IDs must be stable and unique within a subject (for example `SRC-001`, `MIS-OS-01`, `LR-2026-10-23-01`). Do not invent extracted facts when a source is inaccessible.

**Resource record** (`resources/<resource-id>.md`):

```markdown
# <resource-id> — <title>
- Type: slides | document | book | video | transcript | website | exam | other
- Role: teaching material | reference | worked example | practice | past assessment
- Origin/access: <file, URL, platform, or user-provided description; access limits>
- Subject/unit: <subject and relevant unit>
- Coverage: <pages, slides, sections, timestamps, or question numbers>
- Extraction: <what was actually read, watched, transcribed, or extracted>
- Key content: <concepts, definitions, procedures, examples, or exam questions>
- Reliability/uncertainty: <ambiguities, missing segments, and confidence>
- Related resources: <resource IDs or none>
```

For past exams, preserve question wording and marks in the resource or linked exam-bank entry; add a separate tutor-only solution with reasoning, marking points, acceptable alternatives, and confidence. Never mix solutions into learner-facing material.

**Mission record** (`missions/<mission-id>.md`) describes the work to be completed, not a chat turn:

```markdown
# <mission-id> — <unit or objective group>
- Status: planned | ready | in progress | review needed | mastered
- Scope: <included topics and explicit exclusions>
- Sources: <resource IDs; identify primary course sources>
- Prerequisites: <known prerequisites or none>
- Learning outcomes: <observable things the learner should explain, decide, calculate, build, or perform>
- Lesson sequence: <lesson IDs and their focus>
- Assessment plan: <recall, explanation, transfer, and practical evidence as appropriate>
- Mastery evidence: <what fresh, independent performance counts as secure>
- Open questions: <unresolved source gaps or none>
- Next action: <one concrete step>
```

**Learning record** (`learning-records/<record-id>.md`) records one submitted attempt after grading:

```markdown
# <record-id> — <mission-id> / <lesson-id>
- Date:
- Sources and version: <resource IDs and relevant locations>
- Attempt: <attempt number; answer-packet reference if saved>
- Coverage: <objectives/questions actually assessed>
- Results: <MCQ correct/total and written/practical assessment summary>
- Evidence by objective: <objective | status: secure/developing/review | evidence from the response>
- Misconceptions/errors: <specific reasoning gap, or none>
- Practical evidence: <method, result, and assumptions, or not assessed>
- Feedback/retry: <correction and new transfer question, or none>
- Next review: <date/condition and concrete action>
```

Keep `progress.md` as the concise current summary derived from learning records: covered work, current status by objective, persistent misconceptions, spaced-review needs, and next mission. Update the mission status only when the recorded evidence supports it. “Mastered” requires correct explanation plus fresh transfer; it does not mean merely finishing a page or selecting correct MCQ options.

## Build lessons around useful outcomes

Map the source into manageable units. Keep each lesson short enough for one sitting and focused on connected ideas and one or more demonstrable outcomes. Do not compress a long chapter into an unreadable page. Use the original course examples where helpful; clearly label supplemental examples.

Each learner-facing HTML lesson should include:

- Subject/unit/lesson title, learning goals, and estimated time.
- Focused explanations in English followed immediately by their Arabic explanations; preserve the actual course terms in both.
- Concrete examples, diagrams, or worked reasoning suited to the subject.
- Several multiple-choice questions and a modest number of explain/compare/short-answer prompts. For a short lesson, aim for about 4–8 MCQs and 1–3 written tasks; adjust or split when the material requires it.
- A practical application prompt when the learning objective supports one. This can be a scenario, trace, diagram, proof, derivation, calculation, command, query, or code exercise. For a purely conceptual objective, use an applied situation instead of inventing irrelevant coding.
- Source links and precise source positions (page, slide, section, video timestamp, or question number) when available.

Teach the needed knowledge before testing recall. Then ask the learner to retrieve and apply it without showing answers. Vary MCQ answer positions and avoid clues in option length, formatting, or order. Do not put answer keys or hidden correctness flags in the HTML.

## Use past exams as both evidence and practice

When prior exams or sample questions are provided:

1. Extract the questions faithfully, retaining question numbers, diagrams/data, marks, and source/term details where available. Separate question text from answer choices and instructions.
2. Solve each question independently using the provided course materials and conventions. Check calculations, reasoning, code, and edge cases. Use a trusted outside source only to resolve uncertainty, and record that source.
3. Record a tutor-facing answer guide with the expected answer, concise reasoning, marking points, acceptable alternatives, and confidence/ambiguities in `exam-bank/`. Keep it separate from the student HTML and answer export.
4. Use the authentic questions to teach exam style and build practice. Identify copied past-paper questions as past questions; label changed/new questions as variants. Build new variants from the same objective to test transfer rather than memorization.
5. During a quiz, do not reveal a solution before the learner answers unless they explicitly ask for teaching or a worked solution. When grading, compare their answer against the stored reasoning and course source, not only a letter key.

If a question cannot be confidently solved from the sources, say what is uncertain, investigate if useful, and do not invent an authoritative key.

## Match practical work to the subject

The practical section is determined by the actual learning outcome. Make the learner perform the skill when the course expects performance: write or debug code, trace an algorithm, calculate a value, produce a derivation, interpret a graph, label a diagram, apply a command, construct a query, or solve a case. Include the necessary context, constraints, data, language/version, or assumptions.

Capture code and other constructed answers verbatim. Do not claim that an HTML page executed or validated work unless it truly contains the relevant runtime. Evaluate method, correctness, explanation, notation, course conventions, and relevant edge cases.

## Export every response together

Every lesson must end with a prominent **Copy all answers** action. Use the embedded standalone lesson starter below, adapting its content and response controls. Export subject/unit/lesson, attempt timestamp if available, every question ID and full prompt, choices where relevant, selected MCQ choice, written responses, code/calculations verbatim, and unanswered items marked clearly. Provide readable text plus JSON copy/download when practical. Never include the tutor-facing answer key in the learner's export or transmit answers automatically.

Preserve responses locally in the browser. Report whether copying succeeded; if clipboard access is blocked, show the complete packet in a selectable text area for manual copy. The resulting text must be easy to paste into chat.

## Grade, explain, and adapt

When an answer packet arrives:

1. Match each answer to its question; identify blanks, mismatches, or truncation rather than guessing.
2. Grade against the supplied material, stated goals, and tutor-facing solutions. For MCQs, explain the chosen answer. For written responses, identify what is right and what reasoning is missing. For practical work, check the solution and assumptions appropriate to the subject.
3. Summarize per-concept status as **secure**, **developing**, or **review**, supported by specific answer evidence. Keep conceptual recall and practical performance distinct when both are tested.
4. For each gap, explain the concept in English and Arabic, identify the misconception, then give a new retry item with changed details.
5. Update the subject's `progress.md`; carry weak points forward, revisit older material after a delay, and increase difficulty when the evidence supports it. Do not reteach mastered material by default.
6. Advance when the learner explains the key ideas and succeeds on fresh transfer questions. Where a practical outcome is required, ask for a new application of the skill. Treat mastery as evidence-based progress, not a guaranteed exam grade or career result.

Answer clarification questions during a lesson, then resume unfinished practice. Do not call a lesson complete while submitted answers remain unreviewed; state what the learner can paste or retry next.

## Portable single-file mode

This is the complete instruction-only version of Study. It has no separate assets, scripts, or UI metadata file. The YAML front matter supplies the skill name and trigger description; the display name and suggested prompt are included here:

- Display name: Study
- Short description: Learn any subject with source-grounded bilingual lessons and adaptive practice.
- Suggested prompt: Help me study this subject from the sources I provide, quiz me, review my answers, and adapt the next lesson to my progress.

Agent Skills are normally folders anchored by `SKILL.md`, with optional assets loaded only when needed. That folder form is the maintainable choice for Codex and other hosts that support skill bundles. This self-contained form embeds the HTML starter because some hosts accept only one Markdown file; it uses more prompt context in exchange for portability. OpenAI's standard ChatGPT web experience does not install a standalone `SKILL.md` as a native skill. In a regular chat, provide the file and ask the model to follow it if file attachments are supported. For a custom GPT, put behavior in its Instructions and use Knowledge for course references.

Use the embedded HTML starter when the host can create an HTML file or artifact. Replace every `{{...}}` marker, remove optional sections that do not apply, and repeat concept/question blocks as needed. Keep all CSS and JavaScript inline so the page works offline. Do not put answers or correctness markers in the learner page. If the host cannot create or run an HTML artifact, deliver the same lesson in chat and collect responses in a single numbered answer packet; preserve the same feedback loop.

The standalone page uses English for navigation and ordinary interface labels. Put English first and Arabic immediately after it for lesson explanations, with Arabic reserved for concept explanations and genuinely new terminology. It includes a light/dark theme switch, source references, multiple choice and written/application tasks, browser-local answer preservation, progress indication, and one-click export as readable text or JSON. Adapt the practical task to the subject. Remove the terms section if the lesson does not introduce terminology the learner needs to retain. Remove a source link when the source has no accessible URL, but retain its title and page/slide/timestamp reference.

### Complete standalone HTML starter

Copy this starter into the learner's lesson and fill in the content. It is included here so the portable skill needs no accompanying template asset.

```html<!doctype html>
<html lang="en" data-theme="light">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="color-scheme" content="light dark">
  <title>{{LESSON_TITLE}} — Study</title>
  <style>
    :root {
      color-scheme: light;
      --paper: #f4f2eb;
      --surface: #fbfaf6;
      --surface-raised: #fffefa;
      --ink: #252c29;
      --muted: #65706b;
      --rule: #d8d8cc;
      --accent: #315e50;
      --accent-ink: #fffefa;
      --accent-wash: #e7eee8;
      --gold: #a36b21;
      --gold-wash: #f5eddd;
      --input: #fffefa;
      --focus: #bb7625;
      --serif: Georgia, "Times New Roman", serif;
      --sans: "Segoe UI", Tahoma, Arial, sans-serif;
      --mono: Consolas, "Courier New", monospace;
    }
    html[data-theme="dark"] {
      color-scheme: dark;
      --paper: #171e1c;
      --surface: #1d2622;
      --surface-raised: #222d28;
      --ink: #e8e9dd;
      --muted: #a7b1a9;
      --rule: #3b4840;
      --accent: #98c5ad;
      --accent-ink: #15221c;
      --accent-wash: #293d33;
      --gold: #e2b96f;
      --gold-wash: #3b3325;
      --input: #19221e;
      --focus: #efc878;
    }
    * { box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body { margin: 0; background: var(--paper); color: var(--ink); font: 16px/1.7 var(--sans); }
    a { color: var(--accent); text-underline-offset: .2em; }
    button, textarea { font: inherit; }
    button:focus-visible, a:focus-visible, textarea:focus-visible, input:focus-visible { outline: 3px solid var(--focus); outline-offset: 3px; }
    .masthead { background: var(--surface); border-bottom: 1px solid var(--rule); }
    .masthead-inner { width: min(1120px, calc(100% - 48px)); margin: auto; padding: 19px 0 16px; display: flex; justify-content: space-between; align-items: center; gap: 20px; }
    .brand { color: var(--ink); font: 700 22px/1 var(--serif); text-decoration: none; letter-spacing: -.04em; }
    .theme-toggle { border: 1px solid var(--rule); background: var(--surface-raised); color: var(--ink); border-radius: 999px; padding: 8px 13px; cursor: pointer; font-size: 13px; }
    .theme-toggle:hover { border-color: var(--accent); }
    .layout { width: min(1120px, calc(100% - 48px)); margin: 0 auto; display: grid; grid-template-columns: 208px minmax(0, 1fr); gap: clamp(32px, 6vw, 86px); align-items: start; }
    aside { position: sticky; top: 20px; padding: 52px 0; font-size: 13px; }
    .rail-label { margin: 0 0 13px; color: var(--muted); font-size: 11px; letter-spacing: .08em; text-transform: uppercase; }
    .rail-subject { margin: 0 0 5px; font: 700 17px/1.3 var(--serif); }
    .rail-unit { margin: 0; color: var(--muted); }
    .rail-nav { display: grid; gap: 8px; margin: 30px 0; }
    .rail-nav a { color: var(--muted); text-decoration: none; padding: 4px 0 4px 12px; border-left: 2px solid var(--rule); }
    .rail-nav a:hover, .rail-nav a:focus-visible { color: var(--accent); border-color: var(--accent); }
    .progress-label { display: flex; justify-content: space-between; color: var(--muted); font-size: 12px; margin-bottom: 7px; }
    progress { display: block; width: 100%; height: 5px; accent-color: var(--accent); }
    main { min-width: 0; padding: 48px 0 90px; }
    .hero { padding: 2px 0 30px; border-bottom: 1px solid var(--rule); }
    .kicker { margin: 0 0 10px; color: var(--accent); font-size: 13px; font-weight: 650; }
    h1, h2, h3 { text-wrap: balance; }
    h1 { max-width: 760px; margin: 0; font: 500 clamp(35px, 6vw, 59px)/1.08 var(--serif); letter-spacing: -.045em; }
    .hero-meta { display: flex; flex-wrap: wrap; gap: 18px; color: var(--muted); font-size: 13px; margin-top: 18px; }
    .goals { margin: 24px 0 0; padding: 0 0 0 18px; color: var(--muted); font-size: 14px; }
    .section { padding: 40px 0 12px; border-bottom: 1px solid var(--rule); scroll-margin-top: 22px; }
    .section-head { display: flex; align-items: baseline; gap: 13px; margin-bottom: 23px; }
    .section-index { color: var(--gold); font: 18px/1 var(--serif); }
    h2 { margin: 0; font: 500 clamp(24px, 3vw, 32px)/1.2 var(--serif); letter-spacing: -.025em; }
    .concept { padding: 0 0 26px; margin-bottom: 24px; border-bottom: 1px solid var(--rule); }
    .concept:last-child { border: 0; margin-bottom: 0; }
    h3 { margin: 0 0 9px; font: 650 19px/1.35 var(--sans); }
    .explanation { max-width: 70ch; margin: 0; }
    .explanation-ar { max-width: 70ch; margin: 12px 0 0; padding: 12px 16px 12px 0; border-right: 2px solid var(--accent); color: var(--muted); direction: rtl; text-align: right; font-size: 16px; line-height: 1.9; }
    .example { margin: 18px 0 0; padding: 15px 18px; background: var(--accent-wash); border-left: 3px solid var(--accent); white-space: pre-wrap; overflow-wrap: anywhere; font: 14px/1.65 var(--mono); }
    .term-list { display: grid; grid-template-columns: minmax(125px, .32fr) 1fr; border-top: 1px solid var(--rule); }
    .term-list dt, .term-list dd { margin: 0; padding: 12px 0; border-bottom: 1px solid var(--rule); }
    .term-list dt { font-weight: 700; }
    .term-list dd { color: var(--muted); }
    .question { padding: 20px 0 22px; border-bottom: 1px solid var(--rule); }
    .question:last-child { border-bottom: 0; }
    .question-number { display: inline-block; width: 29px; color: var(--gold); font: 18px/1.2 var(--serif); }
    .question-prompt { max-width: 72ch; margin: 0; font-weight: 650; }
    .question-context { margin: 12px 0; padding: 12px 15px; background: var(--gold-wash); color: var(--muted); font-size: 14px; }
    fieldset { min-width: 0; margin: 10px 0 0 29px; padding: 0; border: 0; }
    .choice { display: flex; align-items: flex-start; gap: 11px; margin: 7px 0; padding: 9px 12px; border: 1px solid var(--rule); background: var(--surface); cursor: pointer; }
    .choice:hover { border-color: var(--accent); }
    .choice input { margin-top: 6px; accent-color: var(--accent); }
    .answer { display: block; width: calc(100% - 29px); min-height: 104px; margin: 12px 0 0 29px; padding: 12px 14px; color: var(--ink); background: var(--input); border: 1px solid var(--rule); border-radius: 2px; resize: vertical; }
    .answer.code { min-height: 175px; direction: ltr; text-align: left; tab-size: 2; font: 14px/1.6 var(--mono); }
    .sources { list-style: none; padding: 0; margin: 0; }
    .sources li { padding: 10px 0; border-bottom: 1px solid var(--rule); font-size: 14px; }
    .sources li:last-child { border-bottom: 0; }
    .source-kind { color: var(--muted); font-size: 12px; }
    .export { margin-top: 42px; padding: 25px; background: var(--surface); border-top: 3px solid var(--accent); }
    .export h2 { font-size: 25px; }
    .export-copy { margin: 8px 0 18px; max-width: 65ch; color: var(--muted); font-size: 14px; }
    .actions { display: flex; flex-wrap: wrap; gap: 9px; }
    .action { padding: 10px 15px; border: 1px solid var(--accent); border-radius: 2px; background: var(--accent); color: var(--accent-ink); cursor: pointer; font-weight: 650; font-size: 14px; }
    .action.secondary { background: transparent; color: var(--accent); }
    .action:hover { filter: brightness(.94); }
    #status { min-height: 24px; margin: 12px 0 4px; color: var(--accent); font-size: 13px; }
    .packet-label { display: block; margin-top: 12px; font-size: 13px; font-weight: 650; }
    #packet { width: 100%; min-height: 170px; margin: 6px 0 0; padding: 12px; background: var(--input); color: var(--ink); border: 1px solid var(--rule); font: 12px/1.55 var(--mono); }
    .follow-up { margin: 18px 0 0; color: var(--muted); font-size: 14px; }
    @media (max-width: 760px) {
      .masthead-inner, .layout { width: min(100% - 32px, 640px); }
      .layout { display: block; }
      aside { position: static; padding: 18px 0 0; }
      .rail-nav { display: flex; gap: 18px; overflow-x: auto; margin: 15px 0; }
      .rail-nav a { white-space: nowrap; }
      .rail-progress { max-width: 280px; }
      main { padding-top: 22px; }
    }
    @media (max-width: 420px) {
      .masthead-inner, .layout { width: calc(100% - 24px); }
      .term-list { grid-template-columns: 1fr; }
      .term-list dt { padding-bottom: 0; border-bottom: 0; }
      .term-list dd { padding-top: 3px; }
      .export { padding: 18px 14px; }
      .answer { width: calc(100% - 10px); margin-left: 10px; }
      fieldset { margin-left: 10px; }
    }
    @media (prefers-reduced-motion: reduce) {
      html { scroll-behavior: auto; }
      *, *::before, *::after { transition-duration: .01ms !important; animation-duration: .01ms !important; }
    }
    @media print {
      html, html[data-theme="dark"] { color-scheme: light; --paper: white; --surface: white; --surface-raised: white; --ink: #111; --muted: #444; --rule: #bbb; --accent: #315e50; --accent-ink: white; --accent-wash: #eff4ef; --gold: #79521e; --gold-wash: #f7f2e8; --input: white; }
      .theme-toggle, aside, .actions, #status { display: none !important; }
      .layout { display: block; width: 100%; }
      main { padding: 18px 0; }
      .concept, .question { break-inside: avoid; }
    }
  </style>
</head>
<body data-subject="{{SUBJECT_NAME}}" data-unit="{{UNIT_NAME}}" data-lesson-id="{{LESSON_ID}}">
  <div class="masthead">
    <div class="masthead-inner">
      <a class="brand" href="#top">Study</a>
      <button class="theme-toggle" id="theme-toggle" type="button" aria-label="Switch color theme" title="Switch color theme">◐</button>
    </div>
  </div>

  <div class="layout" id="top">
    <aside aria-label="Lesson navigation">
      <p class="rail-label">Your lesson</p>
      <p class="rail-subject">{{SUBJECT_NAME}}</p>
      <p class="rail-unit">{{UNIT_NAME}}</p>
      <nav class="rail-nav">
        <a href="#learn">Learn</a>
        <a href="#practice">Try it</a>
        <a href="#sources">Sources</a>
      </nav>
      <div class="rail-progress">
        <div class="progress-label"><span>Answered</span><span id="progress-count">0 / 0</span></div>
        <progress id="progress" max="1" value="0">0%</progress>
      </div>
    </aside>

    <main>
      <header class="hero">
        <p class="kicker">{{SUBJECT_NAME}} / {{UNIT_NAME}}</p>
        <h1>{{LESSON_TITLE}}</h1>
        <div class="hero-meta">
          <span>{{ESTIMATED_MINUTES}} min</span>
          <span>{{LESSON_FORMAT}}</span>
        </div>
        <ul class="goals">
          <li>{{LEARNING_GOAL_1}}</li>
          <li>{{LEARNING_GOAL_2}}</li>
        </ul>
      </header>

      <section class="section" id="learn">
        <div class="section-head"><span class="section-index">A</span><h2>Learn</h2></div>
        <!-- Repeat concept blocks as needed. Put the English explanation first and Arabic concept support directly below it. -->
        <article class="concept">
          <h3>{{CONCEPT_TITLE}}</h3>
          <p class="explanation" lang="en">{{ENGLISH_EXPLANATION}}</p>
          <p class="explanation-ar" lang="ar" dir="rtl">{{ARABIC_EXPLANATION}}</p>
          <!-- Keep examples close to the concept. Remove this element when a worked example is not useful. -->
          <pre class="example">{{WORKED_EXAMPLE}}</pre>
        </article>
      </section>

      <!-- Optional: include only when the unit introduces vocabulary the learner needs to retain. -->
      <section class="section" id="terms">
        <div class="section-head"><span class="section-index">B</span><h2>Terms to know</h2></div>
        <dl class="term-list">
          <dt>{{SCIENTIFIC_TERM}}</dt>
          <dd>{{BRIEF_ARABIC_EXPLANATION_OR_CLEAR_DEFINITION}}</dd>
        </dl>
      </section>

      <section class="section" id="practice">
        <div class="section-head"><span class="section-index">C</span><h2>Try it</h2></div>
        <!-- Repeat question blocks. Do not put answer keys or correctness markers in this page. -->
        <article class="question" data-id="q1" data-type="multiple-choice">
          <fieldset>
            <legend class="question-prompt"><span class="question-number">01</span>{{MCQ_PROMPT}}</legend>
            <label class="choice"><input type="radio" name="q1" value="A"><span>{{OPTION_A}}</span></label>
            <label class="choice"><input type="radio" name="q1" value="B"><span>{{OPTION_B}}</span></label>
            <label class="choice"><input type="radio" name="q1" value="C"><span>{{OPTION_C}}</span></label>
            <label class="choice"><input type="radio" name="q1" value="D"><span>{{OPTION_D}}</span></label>
          </fieldset>
        </article>

        <article class="question" data-id="q2" data-type="written-response">
          <p class="question-prompt"><span class="question-number">02</span>{{EXPLAIN_OR_COMPARE_PROMPT}}</p>
          <textarea class="answer" data-answer aria-label="Your answer" placeholder="Write your answer"></textarea>
        </article>

        <!-- Adapt for the subject: scenario, calculation, derivation, diagram, code, query, or other practical work. -->
        <article class="question" data-id="q3" data-type="application">
          <div class="question-context"><strong>Given:</strong> {{PROBLEM_CONTEXT_OR_REMOVE_THIS_LINE}}</div>
          <p class="question-prompt"><span class="question-number">03</span>{{APPLICATION_PROMPT}}</p>
          <textarea class="answer code" data-answer aria-label="Your work" spellcheck="false" placeholder="Write your reasoning or solution"></textarea>
        </article>
      </section>

      <section class="section" id="sources">
        <div class="section-head"><span class="section-index">D</span><h2>Sources</h2></div>
        <ul class="sources">
          <li><span class="source-kind">{{SOURCE_KIND}}</span> <span>{{SOURCE_TITLE_AND_POSITION}}</span><!-- Add a link only if this source has an accessible URL. --></li>
        </ul>
      </section>

      <section class="export" aria-labelledby="export-title">
        <h2 id="export-title">Your answers</h2>
        <p class="export-copy">Copy the full packet and send it to your tutor for feedback. It includes unanswered questions too.</p>
        <div class="actions">
          <button class="action" id="copy-text" type="button">Copy all answers</button>
          <button class="action secondary" id="copy-json" type="button">Copy JSON</button>
          <button class="action secondary" id="download-json" type="button">Download JSON</button>
        </div>
        <p id="status" role="status" aria-live="polite"></p>
        <label class="packet-label" for="packet">Full answer packet</label>
        <textarea id="packet" readonly spellcheck="false" aria-label="Full answer packet"></textarea>
        <p class="follow-up">Need a hint or a concept explained again? Ask before exporting your answers.</p>
      </section>
    </main>
  </div>

  <script>
    (() => {
      const root = document.documentElement;
      const subject = document.body.dataset.subject || 'Course';
      const unit = document.body.dataset.unit || '';
      const lesson = document.body.dataset.lessonId || document.title;
      const responseKey = `study:answers:${subject}:${unit}:${lesson}`;
      const themeKey = 'study:theme';
      const questions = [...document.querySelectorAll('.question[data-id]')];
      const packetBox = document.getElementById('packet');
      const status = document.getElementById('status');

      function setTheme(theme) {
        root.dataset.theme = theme;
        const dark = theme === 'dark';
        const toggle = document.getElementById('theme-toggle');
        toggle.textContent = dark ? '☼' : '◐';
        toggle.setAttribute('aria-label', dark ? 'Switch to light theme' : 'Switch to dark theme');
        toggle.title = dark ? 'Switch to light theme' : 'Switch to dark theme';
        try { localStorage.setItem(themeKey, theme); } catch (_) { /* Theme still works for this page. */ }
      }

      let initialTheme = 'light';
      try {
        initialTheme = localStorage.getItem(themeKey) || (matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light');
      } catch (_) { /* Use the light theme when storage is unavailable. */ }
      setTheme(initialTheme);
      document.getElementById('theme-toggle').addEventListener('click', () => setTheme(root.dataset.theme === 'dark' ? 'light' : 'dark'));

      function readResponse(question) {
        const checked = [...question.querySelectorAll('input[type="radio"]:checked, input[type="checkbox"]:checked')];
        if (checked.length) {
          const values = checked.map((input) => ({
            value: input.value,
            text: input.closest('label')?.innerText.trim() || input.value
          }));
          return { value: values.map((item) => item.value), text: values.map((item) => item.text).join('; ') };
        }
        const select = question.querySelector('select[data-answer]');
        if (select) return { value: select.value, text: select.selectedOptions[0]?.text || '' };
        const answer = question.querySelector('[data-answer]');
        const value = answer?.value.trim() || '';
        return { value, text: value };
      }

      function buildPacket() {
        return {
          subject,
          unit,
          lesson,
          exportedAt: new Date().toISOString(),
          answers: questions.map((question) => ({
            id: question.dataset.id,
            type: question.dataset.type || 'response',
            prompt: (question.querySelector('.question-prompt') || question.querySelector('legend, label, p'))?.innerText.trim() || '',
            choices: [...question.querySelectorAll('input[type="radio"], input[type="checkbox"]')].map((input) => ({
              value: input.value,
              text: input.closest('label')?.innerText.trim() || input.value
            })),
            response: readResponse(question)
          }))
        };
      }

      function renderPacket() {
        const data = buildPacket();
        const lines = [`Subject: ${data.subject}`, `Unit: ${data.unit}`, `Lesson: ${data.lesson}`, `Exported: ${data.exportedAt}`, ''];
        data.answers.forEach((item, index) => {
          lines.push(`${index + 1}. [${item.id} | ${item.type}] ${item.prompt}`);
          item.choices.forEach((choice) => lines.push(`   ${choice.value}. ${choice.text}`));
          lines.push(`Answer: ${item.response.text || '[UNANSWERED]'}`, '');
        });
        packetBox.value = lines.join('\n');
        const answered = data.answers.filter((item) => item.response.text.length > 0).length;
        document.getElementById('progress-count').textContent = `${answered} / ${data.answers.length}`;
        const progress = document.getElementById('progress');
        progress.max = Math.max(data.answers.length, 1);
        progress.value = answered;
        return data;
      }

      function saveResponses() {
        const values = {};
        questions.forEach((question) => {
          values[question.dataset.id] = {};
          question.querySelectorAll('input[type="radio"], input[type="checkbox"]').forEach((input) => {
            values[question.dataset.id][input.value] = input.checked;
          });
          const answer = question.querySelector('[data-answer]');
          if (answer) values[question.dataset.id].text = answer.value;
        });
        try { localStorage.setItem(responseKey, JSON.stringify(values)); } catch (_) { /* Export still works without storage. */ }
        renderPacket();
      }

      try {
        const saved = JSON.parse(localStorage.getItem(responseKey) || '{}');
        questions.forEach((question) => {
          const values = saved[question.dataset.id];
          if (!values) return;
          question.querySelectorAll('input[type="radio"], input[type="checkbox"]').forEach((input) => {
            if (Object.hasOwn(values, input.value)) input.checked = values[input.value];
          });
          const answer = question.querySelector('[data-answer]');
          if (answer && typeof values.text === 'string') answer.value = values.text;
        });
      } catch (_) { /* Start blank if saved data is unavailable. */ }
      document.addEventListener('input', saveResponses);
      document.addEventListener('change', saveResponses);
      renderPacket();

      async function copy(value, label) {
        try {
          await navigator.clipboard.writeText(value);
          status.textContent = `${label} copied. Paste it into your tutor chat.`;
        } catch (_) {
          packetBox.value = value;
          packetBox.focus();
          packetBox.select();
          status.textContent = 'Clipboard access is unavailable. The complete packet is selected below; copy it manually.';
        }
      }
      document.getElementById('copy-text').addEventListener('click', () => copy(renderPacket() && packetBox.value, 'All answers'));
      document.getElementById('copy-json').addEventListener('click', () => copy(JSON.stringify(buildPacket(), null, 2), 'JSON'));
      document.getElementById('download-json').addEventListener('click', () => {
        const blob = new Blob([JSON.stringify(buildPacket(), null, 2)], { type: 'application/json' });
        const url = URL.createObjectURL(blob);
        const link = document.createElement('a');
        link.href = url;
        link.download = `${lesson.replace(/[^a-z0-9_-]+/gi, '-')}-answers.json`;
        link.click();
        setTimeout(() => URL.revokeObjectURL(url), 1000);
        status.textContent = 'JSON answer packet downloaded.';
      });
    })();
  </script>
</body>
</html>
```

