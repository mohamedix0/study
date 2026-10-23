# Study

[![Agent Skills format](https://img.shields.io/badge/format-Agent%20Skills-2563eb)](https://agentskills.io/specification)
[![Skill editions](https://img.shields.io/badge/editions-2-7c3aed)](#choose-an-edition)
[![Portable edition](https://img.shields.io/badge/portable-single%20file-059669)](portable/study/SKILL.md)
[![skills.sh installs](https://skills.sh/b/mohamedix0/study)](https://skills.sh/mohamedix0/study)

**Study** is a bilingual, source-grounded learning skill. It helps an AI tutor teach a subject, test understanding, review submitted answers, and adapt the next practice to the learner’s demonstrated gaps.

It is designed for many subjects: theory courses, mathematics, algorithms and data structures, programming, and other practical topics. It is not tied to one course or one AI provider.

Explanations put English first and follow with a clear Arabic explanation. Keep course terminology, symbols, and notation intact; translate or explain genuinely new subject terms where that helps. Ordinary interface labels and familiar instructions stay in English.

## Choose an edition

| Edition | Files | Use it when |
| --- | --- | --- |
| **Agent edition** | [`study/`](study/) | Your local agent natively loads Agent Skills folders and can access the bundled HTML lesson template. This is the recommended edition for compatible coding agents. |
| **Portable edition** | [`portable/study/SKILL.md`](portable/study/SKILL.md) | The AI interface accepts one Markdown file, or lets you attach it as context. This file embeds the instructions and HTML starter so it has no companion assets. |

The portable edition is a self-contained instruction file; it does **not** turn a web chat into a native skills runtime. Native discovery, persistent workspace access, HTML artifact creation, and file handling depend on the host product, account, and enabled tools. In a regular web chat, attach `SKILL.md` (or paste its contents if attachments are unavailable) and explicitly ask the model to follow it. If the host cannot create an HTML file or artifact, Study provides the same lesson and answer workflow directly in chat.

## Use Study

### Install into a local agent from the terminal

With Node.js and `npx` available, run the command for the edition you want:

```bash
# Full local-agent edition: includes the reusable lesson-page template
npx skills add https://github.com/mohamedix0/study/tree/main/study

# Single-file edition: choose this instead when you want the portable SKILL.md
npx skills add https://github.com/mohamedix0/study/tree/main/portable/study
```

The `skills` CLI downloads the selected skill and interactively asks which supported local agent(s) and install scope to use. Add `-g` for a user-wide installation, or `-a <agent-id>` to target a particular supported agent. Choose one edition per agent: both deliberately use the skill name `study`. To update a CLI-managed installation later, run `npx skills update study`.

The CLI installs into **local agent applications** that it supports; it does not add a skill to a ChatGPT, Gemini, or Claude web account. Use the host’s own skill-import feature for a web product.

### In a web AI chat

The portable edition is meant to be reusable as a **skill**, not only attached to an individual chat. If the web interface lets you import or create reusable skills, add [`portable/study/SKILL.md`](portable/study/SKILL.md) there under the name **Study**, then invoke it in later sessions using that product’s normal skill workflow. Some products expose reusable behavior through a feature called Skills; others use Gems, Projects, custom assistants, or instruction/knowledge fields. Put the Study workflow in the reusable instructions and your course files in that feature’s knowledge or source area when supported.

If the web product does not provide a reusable skill feature, use the same portable file as conversation context: attach it if `.md` is accepted, paste its contents, or save a `.txt` copy and upload it. Then provide the course material and ask to study the desired subject. This is a fallback for chat-only interfaces, not a requirement for interfaces that can save and invoke skills.

Product labels, import flows, plans, and available capabilities differ. The portable file supplies the workflow; it does not add browser access, file persistence, HTML generation, or other tools the host itself lacks. If the interface cannot create an HTML lesson artifact, Study can still deliver the lesson and collect answers directly in chat. Complete the lesson, then use **Copy all answers** (or the single answer packet in chat) and send the packet back to the tutor for grading.

For example, ChatGPT supports file uploads in conversations and offers Projects/custom assistants where available; Gemini Apps supports file uploads and Gems; Claude supports uploaded files and Project instructions/knowledge. Where the product has separate instruction and knowledge areas, put Study's workflow in instructions and course material in knowledge. If a web interface does not accept a `.md` file, paste its contents or use a `.txt` copy. Product features, plans, limits, and native skill support vary; see each provider's current documentation below.

## What the study loop does

1. **Inspect the sources.** Use learner-provided files and links as the primary authority for course scope, terms, and conventions. Sources may include slides, documents, textbooks, notes, diagrams, problem sets, websites, audio, video, transcripts, NotebookLM/Gemini exports, and past exams. State clearly when something could not be accessed or extracted.
2. **Teach in focused lessons.** Explain key ideas in English and Arabic, show course-grounded examples, and define unfamiliar or easily confused terms.
3. **Practise retrieval and application.** Mix suitable multiple-choice, explanation, comparison, calculation, trace, proof, diagram, command, query, or code tasks. Use practical work only when it fits the learning outcome.
4. **Export the complete response.** The lesson page preserves responses locally and exports the questions and submitted answers together as readable text or JSON when supported. The learner sends this packet to the tutor; answers are not sent automatically.
5. **Grade with evidence and adapt.** Identify secure, developing, and review areas from the actual responses, correct misconceptions, give fresh retry questions, and carry weak points into later practice.

Past exam questions retain their provenance and wording where possible. Their solutions are kept separate from learner-facing quizzes; uncertain answers are flagged instead of guessed.

## Sources, state, and privacy

Study can only use material the current AI host can actually read. Video links, private notebooks, protected websites, and externally hosted files may need an upload, transcript, captions, screenshots, or an accessible export. Do not assume a shared link is readable.

For persistent local study, keep generated notes and progress in a separate `study-workspace/` rather than editing the installed skill. Study’s workflow uses source records, mission plans, per-attempt learning records, and a concise progress summary. Browser lesson responses are stored locally by the generated page; the tutor receives them only when the learner copies and sends the answer packet.

Course materials and answer packets may contain private or copyrighted content. Share only what you are allowed to provide, and avoid committing personal course files or learner answer packets to this repository.

## Repository layout

```text
study/
├── SKILL.md                 # Agent Skills instructions
├── agents/openai.yaml       # Codex-facing metadata
└── assets/
    └── lesson-template.html # Reusable interactive lesson page
portable/
└── study/
    └── SKILL.md             # Standalone version with the HTML starter embedded
```

The two `SKILL.md` files are separate deliverables for different loading environments. When changing shared behavior, keep them aligned. The portable edition must continue to work without references to separate files.

## Compatibility notes

The Agent Skills format describes a skill as a directory with a required `SKILL.md` and optional supporting files. Compatible agents can load the full folder; a single-file-only interface can use the portable edition as provided context. Neither edition supplies capabilities the host does not have: for example, source extraction, video analysis, web browsing, persistent file writes, clipboard access, or HTML artifact creation depend on the host and its permissions.

The repository does not claim that every AI website installs skills natively. Use the portable file through that product’s documented instruction or file-upload features, and verify that the model actually follows it.

## Official references

- [Agent Skills format specification](https://agentskills.io/specification)
- [Skills CLI commands and install options](https://github.com/vercel-labs/skills/blob/main/docs/commands.md)
- [Skills CLI documentation](https://www.skills.sh/docs/cli)
- [ChatGPT file uploads](https://help.openai.com/en/articles/8555545-uploading-files-and-audio-to-chatgpt)
- [ChatGPT capabilities and custom assistants](https://help.openai.com/en/articles/9260256-chatgpt-capabilities-overview)
- [Gemini Gems](https://support.google.com/gemini/answer/15236321)
- [Upload and analyze files in Gemini Apps](https://support.google.com/gemini/answer/14903178)
- [Claude Projects and project knowledge](https://support.anthropic.com/en/articles/9517075-what-are-projects)
- [Claude supported document uploads](https://support.anthropic.com/en/articles/8241126-what-kinds-of-documents-can-i-upload-to-claude-ai)

These product-specific features and availability can change. Check each provider’s current documentation for plan, region, file, and workspace limits.

## Validation

The Agent edition follows the Agent Skills folder convention and can be checked with a compatible skill validator. The portable edition is intentionally a single `SKILL.md`; its embedded HTML is generated per lesson and should be opened and checked in the target AI host before relying on it for an assessment.
