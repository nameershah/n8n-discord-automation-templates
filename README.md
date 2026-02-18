# MentorAI - Agentic Study OS

A sophisticated, NotebookLM-inspired study assistant designed for BS AI students, featuring RAG-enhanced intelligence, adaptive quizzes, and voice-enabled learning.

## 🎯 Overview

MentorAI transforms static study materials into dynamic, interactive intelligence sessions through Retrieval Augmented Generation (RAG) and Agentic Reasoning. Built with a professional three-column layout inspired by Jan.ai and NotebookLM's clean design philosophy.

## ✨ Key Features

### 1. **Intelligence Hub (Chat)**
- Context-aware AI powered by Gemini 1.5 Pro
- Document-grounded responses via RAG
- Linear message feed with identity blocks
- Real-time AI thinking indicators
- Voice-enabled interactions (TTS & STT)

### 2. **Assessment Agent (Quiz)**
- AI-generated adaptive quizzes
- Instant visual feedback (green/red highlighting)
- Detailed explanations for reinforced learning
- Progress tracking and scoring
- Question-by-question review

### 3. **Prep Station (Docs)**
- Cheat sheet generator (Markdown export)
- Session history export (JSON)
- PDF document upload & pinning
- Context registry management
- Data sovereignty controls

### 4. **AI Tools**
- RAG Intelligence with document grounding
- Quiz generator from conversations
- Voice engine (read aloud & voice input)
- LaTeX equation rendering support
- Mermaid.js diagram capabilities

### 5. **Settings & Data Management**
- Export all session data
- Factory reset capability
- System information display
- Privacy-focused local storage

## 🎨 Design Philosophy

### Visual Language
- **Obsidian Aesthetic**: Surface-on-surface design with grayscale palette
- **Primary Color**: `#0b0c0e` (deep charcoal)
- **Secondary**: `#111214` (slightly lighter)
- **Accent**: Electric blue (`#3b82f6`) for AI activity telemetry

### Layout Architecture
1. **Column 1 (68px)**: Icon navigation for subsystem switching
2. **Column 2 (280px)**: Activity sidebar with session history
3. **Column 3 (flex)**: Main workspace with header and content

### Interaction Model
- Intent-driven design
- Proactive "Agentic Sub-Actions"
- High information density
- Minimal friction workflow

## 🚀 Setup Instructions

### Prerequisites
- Node.js 16+ and npm/yarn
- Modern browser with Web Speech API support
- Gemini API key (for production deployment)

### Quick Start

1. **Create a new React project:**
```bash
npm create vite@latest mentorai -- --template react
cd mentorai
```

2. **Install dependencies:**
```bash
npm install lucide-react
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

3. **Configure Tailwind CSS:**

Update `tailwind.config.js`:
```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
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

Update `src/index.css`:
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

body {
  margin: 0;
  font-family: 'Inter', system-ui, -apple-system, sans-serif;
}
```

4. **Replace the component:**

Replace `src/App.jsx` with the provided `mentorai-app.jsx` content.

5. **Run the development server:**
```bash
npm run dev
```

## 🔧 API Integration

To connect with the Gemini API:

1. **Get your API key** from [Google AI Studio](https://makersuite.google.com/app/apikey)

2. **Create a `.env` file:**
```
VITE_GEMINI_API_KEY=your_api_key_here
```

3. **Update the sendMessage function** in the component:

```javascript
const sendMessage = async () => {
  // ... existing code ...
  
  try {
    const response = await fetch(
      `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-pro:generateContent?key=${import.meta.env.VITE_GEMINI_API_KEY}`,
      {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          contents: [{
            parts: [{
              text: `Context: ${pinnedDocument ? 'Document: ' + pinnedDocument.name : 'No document'}\n\nUser: ${message}`
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
    
    // Update session with AI response
    const finalSession = {
      ...updatedSession,
      messages: [...updatedSession.messages, aiMessage],
    };
    
    setCurrentSession(finalSession);
    setSessions(sessions.map(s => s.id === finalSession.id ? finalSession : s));
  } catch (error) {
    console.error('API Error:', error);
    // Handle error appropriately
  }
  
  setIsLoading(false);
};
```

## 📋 Feature Implementation Status

| Feature | Status | Notes |
|---------|--------|-------|
| Three-column layout | ✅ Complete | Responsive & polished |
| Session management | ✅ Complete | LocalStorage persistence |
| Message interface | ✅ Complete | Linear feed with identity blocks |
| Voice TTS | ✅ Complete | Web Speech API |
| Voice STT | ✅ Complete | Web Speech API |
| PDF upload | ✅ Complete | File handling ready |
| Quiz generator | ✅ Complete | Adaptive assessment |
| Cheat sheet export | ✅ Complete | Markdown download |
| History export | ✅ Complete | JSON export |
| Data management | ✅ Complete | Clear all data |
| RAG integration | 🔄 Pending | Needs API connection |
| LaTeX rendering | 🔄 Pending | Needs KaTeX library |
| Mermaid diagrams | 🔄 Pending | Needs Mermaid.js |

## 🎓 Use Cases

### 1. **Compiler Design Study**
- Upload lecture notes PDF
- Ask questions about lexical analysis, parsing, code generation
- Generate practice quizzes on grammar rules
- Export concept summaries

### 2. **Data Structures Mastery**
- Pin algorithm documentation
- Voice-query complexity questions
- Quiz on tree traversals, graph algorithms
- Build comprehensive cheat sheets

### 3. **Exam Preparation**
- Aggregate multiple PDFs
- Generate adaptive quizzes
- Review with voice narration
- Export study guides

## 🔐 Privacy & Data

- **100% Local Storage**: All data stored in browser localStorage
- **No Server**: Client-side only (until API integration)
- **Data Export**: Full JSON export capability
- **Factory Reset**: Complete data clearing option

## 🎨 Customization

### Colors
Modify the color scheme in the component by updating Tailwind classes:
- Background: `bg-[#0b0c0e]`, `bg-[#111214]`
- Accent: `bg-blue-500`, `text-blue-400`
- Borders: `border-gray-800`, `border-gray-700`

### Typography
Add custom fonts in `index.html`:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
```

### Layout Dimensions
Adjust column widths in the component:
- Icon nav: `w-16` (change to `w-20` for larger)
- Sidebar: `w-72` (change to `w-80` for wider)

## 🐛 Troubleshooting

### Voice features not working
- Ensure HTTPS or localhost
- Check browser permissions
- Verify Web Speech API support

### PDF upload not processing
- Confirm file type is `.pdf`
- Check file size limits
- Verify browser file API support

### LocalStorage issues
- Check browser storage quota
- Clear browser cache if needed
- Ensure cookies/storage enabled

## 🚀 Deployment

### Vercel
```bash
npm run build
npx vercel
```

### Netlify
```bash
npm run build
netlify deploy --prod --dir=dist
```

### GitHub Pages
```bash
npm run build
# Configure base path in vite.config.js
# Deploy dist folder
```

## 📝 License

This project is provided as-is for educational and personal use.

## 🙏 Acknowledgments

- Design inspiration from NotebookLM and Jan.ai
- Built with React, Tailwind CSS, and Lucide Icons
- Powered by Gemini 1.5 Pro API

## 📧 Support

For issues, feature requests, or questions, please refer to the project documentation or contact the development team.

---

**MentorAI** - Transforming study materials into interactive intelligence sessions 🚀
