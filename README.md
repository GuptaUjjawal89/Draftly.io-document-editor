# Draftly.io — Lightweight Collaborative Document Editor

A fast, minimal document workspace for individuals and small teams. Built with Next.js 15, TipTap rich-text editor, and Tailwind CSS. No backend required — runs entirely in the browser with localStorage persistence.

---

## Features

- **Rich text editing** — Bold, italic, underline, headings, lists via TipTap
- **Auto-save & persistence** — Documents survive refresh via localStorage
- **Multi-user simulation** — Switch between Alice, Bob, and Carol to test sharing flows
- **Document sharing** — Share docs with other simulated users; owned vs shared views
- **File import** — Upload `.txt` or `.md` files to create or append to documents
- **Attachments** — Attach files to documents (stored as base64 in localStorage)
- **AI Writing Assistant** — Summarize, improve writing, shorten, or make text more professional — all local, no API key needed
- **Export** — Download any document as Markdown or PDF via the export dropdown

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 16 (App Router) |
| UI | React 19 + Tailwind CSS v4 |
| Rich Text Editor | TipTap v3 (with StarterKit + Underline) |
| Components | Radix UI + shadcn/ui |
| State Management | React Context (`DocumentContext`) |
| Persistence | Browser `localStorage` |
| PDF Export | jsPDF |
| Package Manager | pnpm |
| Language | TypeScript 5.7 |

---

## Prerequisites

Make sure you have the following installed:

- **Node.js** `v18.17` or higher ([download](https://nodejs.org))
- **pnpm** `v8` or higher

Install pnpm if you don't have it:

```bash
npm install -g pnpm
```

---

## Local Setup

**1. Clone the repository**

```bash
git clone https://github.com/GuptaUjjawal89/Draft.io-document-editor.git
cd Draft.io-document-editor
```

**2. Install dependencies**

```bash
pnpm install
```

> No `.env` file is needed — the app has no external API dependencies in its current MVP state.

---

## Running the App

**Development server** (with hot reload)

```bash
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

**Production build**

```bash
pnpm build
pnpm start
```

**Lint**

```bash
pnpm lint
```

---

## Project Structure

```
Draft.io-document-editor/
├── app/
│   ├── layout.tsx          # Root layout, fonts, metadata
│   ├── page.tsx            # App entry point
│   └── globals.css         # Global styles
├── components/
│   ├── editor/
│   │   ├── document-editor.tsx     # Main editor shell
│   │   ├── rich-text-editor.tsx    # TipTap integration
│   │   ├── editor-toolbar.tsx      # Formatting toolbar
│   │   ├── share-dialog.tsx        # Share with user dialog
│   │   ├── attachments-panel.tsx   # File attachment panel
│   │   ├── ai-assistant-panel.tsx  # AI writing assistant dialog (NEW)
│   │   └── export-dropdown.tsx     # Markdown / PDF export menu (NEW)
│   ├── sidebar/
│   │   ├── app-sidebar.tsx         # Main sidebar wrapper
│   │   ├── document-list.tsx       # Owned + shared doc lists
│   │   └── file-upload.tsx         # Import .txt / .md files
│   └── ui/                         # shadcn/ui component library
├── lib/
│   ├── document-context.tsx        # Global state (React Context)
│   ├── storage.ts                  # localStorage read/write layer
│   ├── export-utils.ts             # Markdown / PDF export helpers
│   ├── ai-assistant.ts             # Local AI text transformation engine (NEW)
│   ├── date-utils.ts               # Date formatting
│   └── utils.ts                    # Tailwind class helpers
├── hooks/                          # Shared React hooks
├── public/                         # Static assets
├── next.config.mjs
├── package.json
└── tsconfig.json
```

---

## How It Works

### Users

The app simulates three users — no login required:

| User | ID |
|---|---|
| Alice Johnson | `user1` |
| Bob Smith | `user2` |
| Carol Lee | `user3` |

Switch users via the sidebar to see ownership and sharing in action.

### AI Writing Assistant

The AI assistant runs entirely locally — no API key or network request needed. It supports four actions:

| Action | What it does |
|---|---|
| **Summarize** | Extracts the first sentence from each paragraph into a summary |
| **Improve Writing** | Fixes grammar, capitalisation, and informal language |
| **Make Shorter** | Strips filler words and verbose phrases |
| **Make Professional** | Replaces casual language with formal alternatives |

Open it via the **AI Assistant** button in the editor toolbar. Results can be copied to clipboard or inserted directly into the document.

> **Production note:** `lib/ai-assistant.ts` is structured to make swapping in a real LLM (OpenAI, Anthropic, etc.) straightforward — just replace `generateLocalAISuggestion` with an API call.

### Export

Use the **Export** dropdown in the editor toolbar to download the active document:

- **Markdown** — plain `.md` file, downloaded directly in the browser
- **PDF** — generated client-side via [jsPDF](https://github.com/parallax/jsPDF), no server required

---

All data is stored in `localStorage` under these keys:

| Key | Contents |
|---|---|
| `collab-docs-documents` | All documents (JSON array) |
| `collab-docs-attachments` | File attachments (base64) |
| `collab-docs-current-user` | Active user ID |
| `collab-docs-active-doc:<userId>` | Last active document per user |

> **Note:** Clearing browser storage will reset all documents. This is expected behavior for the localStorage-based MVP.

---

## Common Issues

**Port already in use**

```bash
# Kill whatever is on port 3000
npx kill-port 3000
pnpm dev
```

**pnpm not found**

```bash
npm install -g pnpm
```

**TipTap SSR hydration warning in dev**

This is a known Next.js + TipTap edge case in development mode. It does not affect functionality and does not appear in production builds.

**Styles not loading**

Ensure you're on Node.js 18+. Tailwind v4 requires a modern Node environment.

---

## Roadmap

- [x] AI Writing Assistant (local, no API key)
- [x] Export to Markdown and PDF
- [ ] Real-time collaboration (WebSockets / CRDTs)
- [ ] Backend persistence (Supabase / PostgreSQL)
- [ ] Connect AI Assistant to a real LLM API (OpenAI / Anthropic)
- [ ] Document version history
- [ ] Role-based permissions (viewer / editor)
- [ ] Secure sharing links

---

## Built With

- [Next.js](https://nextjs.org)
- [TipTap](https://tiptap.dev)
- [Radix UI](https://radix-ui.com)
- [shadcn/ui](https://ui.shadcn.com)
- [Tailwind CSS](https://tailwindcss.com)
- [jsPDF](https://github.com/parallax/jsPDF) — client-side PDF generation
- [Vercel v0](https://v0.dev) — initial scaffolding

---

## License

Private repository. All rights reserved © Ujjawal Gupta.
