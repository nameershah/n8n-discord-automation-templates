# MentorAI — Agentic Study OS

> Transform static study materials into dynamic, AI-powered learning sessions.

![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react)
![Tailwind](https://img.shields.io/badge/Tailwind-CSS-38B2AC?style=flat-square&logo=tailwind-css)
![Gemini](https://img.shields.io/badge/Gemini-1.5_Pro-4285F4?style=flat-square&logo=google)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

MentorAI is a NotebookLM-inspired study assistant built for BS AI students. It combines Retrieval Augmented Generation (RAG), adaptive quizzing, and voice-enabled interactions in a clean three-column interface.

---

## Features

**Intelligence Hub** — Context-aware chat powered by Gemini 1.5 Pro with document-grounded responses, real-time thinking indicators, and voice input/output.

**Assessment Agent** — AI-generated adaptive quizzes with instant feedback, detailed explanations, and progress tracking.

**Prep Station** — Upload and pin PDF documents, generate Markdown cheat sheets, export session history as JSON, and manage your context registry.

**Data Management** — All data stays in your browser. Full export and factory reset controls included.

---

## Quick Start

### Prerequisites
- Node.js 16+
- A [Gemini API key](https://makersuite.google.com/app/apikey)

### Installation

```bash
# Create project
npm create vite@latest mentorai -- --template react
cd mentorai

# Install dependencies
npm install lucide-react
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

### Configure Tailwind

`tailwind.config.js`:
```js
export default {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
      },
    },
  },
  plugins: [],
}
```

`src/index.css`:
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Run

```bash
# Replace src/App.jsx with the provided mentorai-app.jsx
npm run dev
```

---

## API Integration

Create a `.env` file in the project root:

```env
VITE_GEMINI_API_KEY=your_api_key_here
```

Then update the `sendMessage` function in the component:

```javascript
const response = await fetch(
  `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-pro:generateContent?key=${import.meta.env.VITE_GEMINI_API_KEY}`,
  {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      contents: [{
        parts: [{
          text: `Context: ${pinnedDocument?.name ?? 'None'}\n\nUser: ${message}`
        }]
      }]
    })
  }
);

const data = await response.json();
const aiMessage = {
  id: Date.now() + 1,
  role: 'assistant',
  content: data.candidates[0].content.parts[0].text,
  timestamp: new Date().toISOString(),
};
```

---

## Feature Status

| Feature | Status |
|---------|--------|
| Three-column layout | ✅ Complete |
| Session management | ✅ Complete |
| Voice TTS & STT | ✅ Complete |
| PDF upload & pinning | ✅ Complete |
| Adaptive quiz generator | ✅ Complete |
| Cheat sheet export | ✅ Complete |
| Session history export | ✅ Complete |
| RAG integration | 🔄 Pending API |
| LaTeX rendering | 🔄 Pending KaTeX |
| Mermaid diagrams | 🔄 Pending |

---

## Deployment

```bash
# Build
npm run build

# Deploy to Vercel
npx vercel

# Deploy to Netlify
netlify deploy --prod --dir=dist
```

---

## Troubleshooting

**Voice features not working** — Ensure you're on `localhost` or HTTPS. Check browser microphone permissions and confirm Web Speech API support.

**PDF not processing** — Confirm the file is `.pdf` format. Check browser storage quota and file API support.

**LocalStorage issues** — Clear browser cache, confirm cookies and storage are enabled in browser settings.

---

## Tech Stack

- **Frontend:** React 18, Tailwind CSS, Lucide Icons
- **AI:** Google Gemini 1.5 Pro
- **Speech:** Web Speech API (native browser)
- **Storage:** Browser localStorage (client-side only)
- **Design:** Obsidian-inspired dark UI, NotebookLM layout

---

## License

MIT — free for educational and personal use.

---

*MentorAI — Built for learners who think in systems.*
