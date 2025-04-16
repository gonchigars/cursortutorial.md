# Practical Guide: Full Stack Development with Cursor & AI

## Getting Started

### Setting Up Your Environment
1. **Install Cursor**
   - Go to [cursor.com](https://cursor.com)
   - Download the appropriate version for your OS
   - Run the installer and follow the prompts
   - Start Cursor and activate the free Pro trial

2. **Configure Your Workspace**
   - Open a new or existing project folder
   - Navigate the interface: file explorer (left), editor (center), terminal (bottom)
   - Open the AI Chat panel with `Ctrl/Cmd + L` if not visible
   - Configure settings at File > Preferences > Cursor Settings

3. **Set Up AI Models**
   - Choose your preferred model in the AI chat panel dropdown
   - Recommended: Claude 3.5 Sonnet for most coding tasks
   - Consider Claude 3.7 Sonnet for complex design tasks
   - Ensure your API keys are correctly configured if required

## Basic Workflow

1 . **Version Control Setup**
   - Initialize Git repository if needed
   - Create .gitignore and README.md files
   - Prompt: "Create a comprehensive .gitignore file for a [your stack] project and a basic README"

# Essential Web Development Concepts: A Reading Guide
*Understanding the 20% that gives you 80% of code reading ability*

## Learning with AI-Assisted Experimentation
This guide embraces a new approach to learning web development:
- **You focus on understanding concepts**, not memorizing syntax
- **Let AI write the code** while you design experiments to test your understanding
- **Read, modify, observe, and learn** from the results

### The Experiment-Based Learning Approach:
```
┌────────────────────┐     ┌────────────────────┐     ┌────────────────────┐
│                    │     │                    │     │                    │
│  Understand        │────▶│  Form a            │────▶│  Design an         │
│  the concept       │     │  hypothesis        │     │  experiment        │
│                    │     │                    │     │                    │
└────────────────────┘     └────────────────────┘     └────────────────────┘
                                                                │
                                                                │
                                                                ▼
┌────────────────────┐     ┌────────────────────┐     ┌────────────────────┐
│                    │     │                    │     │                    │
│  Refine your       │◀────│  Observe the       │◀────│  Ask AI to         │
│  mental model      │     │  results           │     │  implement code    │
│                    │     │                    │     │                    │
└────────────────────┘     └────────────────────┘     └────────────────────┘
```

## How to Use This Guide
This guide focuses on helping you **read and understand** web development code, not necessarily write it. Each section includes:
- Core concepts explanation
- Text diagrams for visual understanding
- Common patterns to recognize
- Example snippets showing what they look like in real code
- Experiment prompts for AI-assisted learning

---

## HTML Fundamentals

### 1. Document Structure
```
<!DOCTYPE html>
<html>
    <head>
        <!-- Metadata, title, CSS links -->
    </head>
    <body>
        <!-- Visible content -->
    </body>
</html>
```

**Visual Structure:**
```
┌─────────────────────────────────────────┐
│ <!DOCTYPE html>                         │
│ <html>                                  │
│ ┌─────────────────────────────────────┐ │
│ │ <head>                              │ │
│ │   <title>Page Title</title>         │ │
│ │   <link rel="stylesheet" href="..."> │ │
│ │   <meta ...>                        │ │
│ │ </head>                             │ │
│ └─────────────────────────────────────┘ │
│ ┌─────────────────────────────────────┐ │
│ │ <body>                              │ │
│ │   <header>...</header>              │ │
│ │   <main>...</main>                  │ │
│ │   <footer>...</footer>              │ │
│ │ </body>                             │ │
│ └─────────────────────────────────────┘ │
│ </html>                                 │
└─────────────────────────────────────────┘
```

**What to look for when reading:**
- `<!DOCTYPE html>` - Tells the browser this is HTML5
- `<head>` contains invisible setup information 
- `<body>` contains everything you actually see

### 2. Semantic HTML
**Common semantic elements:**
```
<header>  - Top section with logo, nav, etc.
<nav>     - Navigation links
<main>    - Primary content area
<section> - Standalone section of content
<article> - Self-contained content
<aside>   - Related but separate content
<footer>  - Bottom section with extra links/info
```

**Reading comparison:**
```
NON-SEMANTIC HTML                   SEMANTIC HTML
┌─────────────────────────┐       ┌─────────────────────────┐
│ <div class="nav">       │       │ <nav>                   │       ← Clearly indicates this is navigation
│                         │       │                         │
│   <div>Home</div>       │       │   <a href="/">Home</a>  │       ← Proper link element with destination
│                         │       │                         │
│   <div>About</div>      │       │   <a href="/about">     │       ← Links are clickable and accessible
│                         │       │      About              │
│ </div>                  │       │   </a>                  │
│                         │       │                         │
│                         │       │ </nav>                  │
└─────────────────────────┘       └─────────────────────────┘

• Non-semantic version tells us nothing about purpose
• Browser treats all <div> elements the same way
• Screen readers can't identify navigation purpose
• CSS styling must be used to make it look like navigation

• Semantic version communicates meaning to browsers
• Screen readers announce this as navigation
• Browsers may render differently (e.g., on mobile)
• Search engines understand the page structure better
```

**Key tip:** When reading code, semantic elements tell you what the content's purpose is, while divs and spans tell you nothing until you see their CSS.

---

## CSS Core Concepts

### 1. Selectors and Specificity

**Selector types from least to most specific:**
```
Element < Class < ID < Inline styles < !important
```

**Specificity visualization:**
```
┌────────────────────────────────────────────────────┐
│ Specificity power:                                 │
│                                                    │
│ p              → [0,0,0,1] (Element)               │
│ .card          → [0,0,1,0] (Class)                 │
│ #header        → [0,1,0,0] (ID)                    │
│ style="color:" → [1,0,0,0] (Inline)                │
│                                                    │
│ .card p        → [0,0,1,1] (Class + Element)       │
│ #header .nav   → [0,1,1,0] (ID + Class)            │
└────────────────────────────────────────────────────┘
```

**When reading CSS, ask:**
- Which selector will win when styles conflict?
- Is the selector targeting the right elements?
- Is `!important` being used (which overrides everything)?


---


