# 📘 Simple SRS (Software Requirements Specification)
## Project Name: PlacementPilot (My AI Placement Coach)

> **What is this project in one sentence?**  
> An AI coach that reads my resume, finds real company interview questions, creates daily customized quiz and coding games for me, grades my answers, and helps me crack top tech placements.

---

## 🎯 1. Why Am I Building This? (The Goal)

1. **Generic prep is boring:** Everyone does the same random 100 LeetCode problems without knowing if companies actually ask them.
2. **ChatGPT forgets everything:** In a normal chat, ChatGPT forgets what I got wrong last week.
3. **Interviews ask about my resume:** Real interviewers ask hard questions about *my own projects*.
4. **This tool fixes all of that:** It personalizes questions to *my* resume, tests me in 4 areas every day, turns study sessions into games, and remembers all my mistakes so I can fix them.

---

## 🛠️ 2. The Tech Stack (What Tools Am I Using?)

| Tool / Technology | What It Does (Plain English) |
| :--- | :--- |
| **Python** | The main programming language for all AI logic and backend. |
| **LangGraph & LangChain** | The brain manager. It lets multiple AI agents talk to each other, make decisions, and retry if something goes wrong. |
| **Ollama (`llama3.2:3b`)** | The local AI model running on my **NVIDIA RTX 2050 GPU**. It is 100% free, private, and works offline. |
| **ChromaDB** | The vector database. It stores thousands of real interview questions and finds the closest matching ones in milliseconds. |
| **MongoDB & MongoDB Compass** | The memory notebook. It saves my resume details, test scores, and mistake history. I can open MongoDB Compass on my desktop to visually inspect everything. |
| **Next.js & Tailwind CSS** | The website frontend. Gives me an interactive battleground with a code editor, live timers, and skill charts. |
| **UI Design System: Apple-Duolingo Hybrid** | **The exact UI design we are using:** Pairs **Apple's premium minimalism & whitespace** (`#F5F5F7` surfaces, dark obsidian cards, crisp Inter typography) with **Duolingo's tactile gamification** (tactile `#58CC02` 3D-depth buttons, XP badges, and bouncy progress bars). |
| **Docker & Render.com (Phase 7)** | Packages the project and hosts it live on the internet for free so recruiters can click and test it. |

---

## 🤖 3. The 9 AI Agents (Who Does What?)

Think of these agents like a team of 9 assistants working for me:

1. 📄 **Agent 1: Resume Profiler** → Reads my resume PDF and writes down what languages, tools, and projects I know.
2. 🏢 **Agent 2: Company Scout** → Knows what companies like Google, Amazon, and Microsoft ask in their interviews.
3. 🧠 **Agent 3: Strategy Planner** → Checks my mistake history and decides what I need to practice today (e.g., *"He struggled with DBMS yesterday, let's give him 2 DBMS questions today"*).
4. 🔍 **Agent 4: Question Retriever (RAG)** → Searches ChromaDB to fetch real interview questions that match today's plan.
5. ⚖️ **Agent 5: Quality Checker (CRAG)** → Checks the fetched questions: *"Are these questions good and accurate?"* If not, it searches again.
6. ⚡ **Agent 6: Challenge Maker** → Builds my 4 daily test tracks (Quiz, Coding DSA, Resume System Design, OOPs).
7. 🕹️ **Agent 7: Game Master** → Turns chat into a game! Triggers a **60-Second Sudden Death Quiz** when I'm discussing concepts, plus Company Boss Battles.
8. 🛡️ **Agent 8: Anti-Repetition Critic** → Checks my last 14 days in MongoDB: *"Did he already solve this question?"* If yes, it forces Agent 6 to give me a new one.
9. 👨‍🏫 **Agent 9: Evaluator & Mentor** → Grades my code, checks if my code is fast or slow ($O(N)$ vs $O(N^2)$), awards XP points, and saves my mistakes into the `mistake_vault`.

---

## 📋 4. The 4 Daily Tracks I Get Every Day

Every morning, the app gives me 4 customized challenges:

* 🎯 **Track 1: Core CS Quiz** → 5 multiple-choice questions on Operating Systems, DBMS, Computer Networks, and Aptitude with answers explained.
* 💻 **Track 2: Coding DSA** → 1 coding problem matching my skill level, with sample inputs, outputs, and edge test cases.
* 🏗️ **Track 3: System Design** → 1 architecture question based on **my own resume projects** (e.g., *"How would you handle 10,000 users on your website without crashing?"*).
* 🧱 **Track 4: OOPs / Low-Level Design** → 1 design problem (like designing a Parking Lot or Notification System) in Python or my favorite language.

---

## 🗺️ 5. The 7 Phases to Build It (Step-by-Step)

```
[Phase 1] Read my Resume (Agent 1 + MongoDB)
    ↓
[Phase 2] Build the Question Library (ChromaDB + Agents 2, 4, 5)
    ↓
[Phase 3] Generate 4 Daily Tracks (Agents 3, 6, 8)
    ↓
[Phase 4] Add the 60-Second Quiz Game & Boss Battles (Agent 7)
    ↓
[Phase 5] Grade Code & Save Mistakes (Agent 9 + Spaced Repetition)
    ↓
[Phase 6] Build the Next.js Web Interface (Monaco Editor + Timers)
    ↓
[Phase 7] Put it live on the Cloud with Render & Docker (0 MB Laptop RAM!)
```

### Summary of Each Phase:
* **Phase 1:** I upload my resume PDF → Python reads it → Llama 3.2 extracts my skills → saves to MongoDB (viewable in Compass).
* **Phase 2:** Put interview questions into ChromaDB → test semantic search with `nomic-embed-text`.
* **Phase 3:** LangGraph connects the agents to produce the 4 tracks without repeating anything from the last 14 days.
* **Phase 4:** When I chat with the bot, it launches a 60-second quiz game with sound effects and timers!
* **Phase 5:** When I submit code, it checks for bugs and time complexity, awards XP points, and records what I got wrong.
* **Phase 6:** Build the web interface using our **Apple-Duolingo Hybrid Design System** (crisp Apple layouts, floating dock, tactile 3D Duolingo green `#58CC02` buttons, Monaco code editor, and live skill radar charts).
* **Phase 7:** Deploy via Docker to Render.com so I have a public link (`https://placementpilot.onrender.com`) to put on my LinkedIn and resume!

---

## 🔒 6. Hardware Safety Rules (For My Laptop)

* **RAM:** My laptop has 8 GB RAM. During development (Phases 1–6), I run everything directly in Python on Windows to keep RAM usage low (~500 MB).
* **GPU (VRAM):** My RTX 2050 has 4 GB VRAM. The Llama 3.2 3B model uses ~2.0 GB VRAM, leaving ~2.0 GB free. It will run smoothly at 25–35 words per second.
* **Cloud (Phase 7):** When deployed to Render.com, the app runs on the cloud for free, using **0 MB of my laptop's RAM or disk**.

---

## ✅ 7. What Success Looks Like

1. I have an automated, daily placement coach that keeps me consistent.
2. I never have to manually write prompts to study.
3. The app remembers all my weak points and helps me improve them over time.
4. I have an incredible, unique AI engineering project to showcase on my resume and LinkedIn!
