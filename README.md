# Ultimate Guide to Vibe Coding V1.2.2
**Author:** [Nicolas Zullo, https://x.com/NicolasZu](https://x.com/NicolasZu)  
**Creation Date:** March 12, 2025  
**Last Update Date:** March 5, 2026  

---

## Getting Started
To begin vibe coding, you only need:
- **OpenAI GPT-5.4 (high)**, in Codex CLI or the the Codex App (select the Plus subscription for ~ $20 / month)

This guide works for both the CLI version (to use in the terminal), the VSCode extension version, or the Codex App. Right now, the Codex App is gaining a lot of love.

*(Note: While earlier versions of this guide utilized **Grok 3**, we then transitioned to **Gemini 2.5 Pro**. And now we're using **OpenAI GPT-5.4 (high)**)*

*(Note 2: If you want to use Cursor, please check the [version 1.1](https://github.com/EnzeD/vibe-coding/tree/1.1.1) of this guide, but we believe it's less powerful than Codex CLI)*

Setting up everything correctly is key. If you’re serious about creating a fully functional and visually appealing game (or app), take the time to establish a solid foundation.  

**Key Principle:** *Planning is everything.* Do NOT let the AI plan autonomously, or your codebase will become an unmanageable mess.

---

## Setting Up Everything

### 0. Initial Setup
- Download Visual Studio Code (https://code.visualstudio.com/)
- Create a new folder in your machine
- Right click, open with Code
- Start a terminal
  - Install Codex CLI: `npm i -g @openai/codex`
(or download the Codex app)

### 1. Game Design Document (or Product Requirements Document for an app)
- Take your game idea and ask **OpenAI GPT-5.4 (high)** to create a simple **Game Design Document** in Markdown format: `game-design-document.md`.  
- Review and refine the document to ensure it aligns with your vision. It’s fine if it’s basic—the goal is to give your AI context about the game’s structure and intent. Do not over-engineer as we will iterate later.
- If you want, you can also have your AI ask you questions and use that to write the GDD or PRD. 

### 2. Tech Stack and `AGENTS.md`
- Ask **OpenAI GPT-5.4 (high)** to recommend the best tech stack for your game (e.g., Vite + ThreeJS and WebSocket for a multiplayer 3D game). Save this as `tech-stack.md`.
  - Challenge it to propose the *simplest yet most robust stack possible*.  
- In your terminal, open **Codex** and use the `/init` command. It will use the two .md files you created so far. This will create a set of rules so your LLM is guided correctly.
- **Crucially, review the generated rules.** Ensure they emphasize **modularity** (multiple files) and discourage a **monolith** (one giant file). You might need to manually tweak or add rules. Review also when they trigger.
  - **IMPORTANT:** Some rules are critical for maintaining context and should be set as **"Always"** rules. This ensures the AI *always* refers to them before generating code. Consider adding rules like the following and marking them as "Always":
    
    > ```
    > # IMPORTANT:
    > # Always read memory-bank/@architecture.md before writing any code. Include entire database schema.
    > # Always read memory-bank/@game-design-document.md before writing any code.
    > # After adding a major feature or completing a milestone, update memory-bank/@architecture.md.
  - Example: Ensure other (non-"Always") rules guide the AI towards best practices for your stack (like networking, state management, etc.).
  - *This overall rules setup is mandatory if you want a game that is as optimized as possible, and code as clean as possible.*


### 3. Implementation Plan
- Provide **OpenAI GPT-5.4 (high)** with:  
  - The Game Design Document (`game-design-document.md`)
  - The tech stack recommendations (`tech-stack.md`)
- Ask it to create a detailed **Implementation Plan** in Markdown (`.md`) which is a set of step-by-step instructions for your AI developers.  
  - Steps should be small and specific.  
  - Each step must include a test to validate correct implementation.  
  - No code: just clear, concrete instructions.  
  - Focus on the *base game*, not the full feature set (details come later).  

### 4. Memory Bank
- Create a new folder for your project and then open it in VSCode.
- Inside the project folder, create a subfolder named `memory-bank`.  
- Add the following files to `memory-bank`:  
  - `game-design-document.md`  
  - `tech-stack.md`  
  - `implementation-plan.md`  
  - `progress.md` (Create this empty file for tracking completed steps)  
  - `architecture.md` (Create this empty file for documenting file purposes)

---

## Vibe Coding the Base Game
Now the fun begins!

### Making sure everything is clear
- Open **Codex** in VSCode's extension or launch it in the terminal of your project.
- Prompt: Read all the documents in `/memory-bank`, is `implementation-plan.md` clear? What are your questions to make it 100% clear for you?
- He usually asks 9-10 questions. Answer them and prompt him to edit the `implementation-plan.md` accordingly, so it's even better.

### Your first implementation prompt
- Open **Codex** in VSCode's extension or launch it in the terminal of your project.
- Prompt: Read all the documents in `/memory-bank`, and proceed with Step 1 of the implementation plan. I will run the tests. Do not start Step 2 until I validate the tests. Once I validate them, open `progress.md` and document what you did for future developers. Then add any architectural insights to `architecture.md` to explain what each file does.
- **Always** start with a planning pass and once you are satisfied, allow the AI to go through the step.
- **Extreme vibe:** Install [Superwhisper](https://superwhisper.com) to speak casually with **OpenAI GPT-5.4 (high)** instead of typing.

### Workflow
- After completing Step 1:  
- Commit your changes to Git (if unfamiliar, ask your AI for help).  
- Start a new chat (`/new` or `/clear`). Why? LLM produce their best results when there is a lot of room in their context window.
- Prompt: Now go through all files in the memory-bank, read progress.md to understand prior work, and proceed with Step 2. Do not start Step 3 until I validate the test.
- Repeat this process until the entire `implementation-plan.md` is complete.  

---

## Adding Details
Congratulations, you’ve built the base game! It might be rough and lack features, but now you can experiment and refine it.  
- Want fog, post-processing, effects, or sounds?  A better plane/car/castle? A gorgeous sky?
- For each major feature, create a new `feature-implementation.md` file with short steps and tests.  
- Implement and test incrementally.  

---

## Fixing Bugs and Stuckness
- If a prompt fails or breaks the game:  
- Refine your prompt until it works. You can also commit often to git and reset when needed.
- For errors:  
    - **If JavaScript:** Open the console (`F12`), copy the error, and paste it into VSCode to provide a screenshot for visual glitches.  
    - **Lazy Option:** Install [BrowserTools](https://browsertools.agentdesk.ai/installation) to skip manual copying/screenshotting.  
- If stuck:  
    - Revert to your last Git commit (`git reset`) and retry with new prompts.  
- If *really* stuck:  
    - Use [RepoPrompt](https://repoprompt.com/) or [uithub](https://uithub.com/) to get your whole codebase in one file and ask **OpenAI GPT-5.4 (high)** for assistance.

---

## Codex Tips
- **Codex in the terminal:** Run it inside VSCode's terminal to view diffs and feed additional context without leaving your workspace.
- **Custom Codex commands or skills:** Create helpers like `/explain $arguments` that trigger a prompt such as "Do a deep-dive on the code and understand how $arguments works. Once you understand it, let me know, and I will provide the task I have for you." so the model pulls in rich context before editing.
- **Clearing context:** Clear context frequently with `/clear` or `/compact` if you still need previous conversations context. Keep `/context` over 50 or 60% for best performances.
- **Save time (at your own risk):** Use `codex --yolo` to start Codex in a mode where it will never ask you confirmations.

## Other Tips
- **Small Edits:** Use OpenAI GPT-5.4 (high)
- **Great Marketing Copywriting:** Use OpenAI GPT-5.4 (high)
- **Generate Great Sprites (2D images):** Use ChatGPT and Nano Banana Pro
- **Generate 3D assets:** Use Trellis, Tripo or Hunyuan
- **Generate Music:** Use Suno, ElevenLabs
- **Generate Sound Effects:** Use ElevenLabs
- **Generate Video:** Use Sora 2, Veo 3
- **Better prompt outputs:** 
    - Add “think as long as needed to get this right, I am not in a hurry. What matters is that you follow precisely what I ask you and execute it perfectly. Ask me questions if I am not precise enough." 
    - For Codex, ask explicitly for a planning pass, tighter constraints, and deeper reasoning before execution.

---

## Frequently Asked Questions
**Q: What projects have been 100% vibe coded by yourself with this methodology?**  
**A:** Among the most recent:
- https://fly.zullo.fun/ a 3D WW2 Dogfight Arena game. All assets and code are vibe coded with the methodology from this guide. 
- https://vibecraft.game/ a 3D game in which you can prompt anything into existence. All code, UI, and in game assets are vibe coded.
- https://www.dow-de.com/ a web app that ranks the best player of Warhammer 40000 Dawn of War, with stats, replay upload and even a premium tier. 100% vibe coded as well with this methodology.
- https://www.zombiesperminute.com/ a highly complex factory-building roguelite strategy game where you automate zombie-elimination outposts across procedurally generated maps to maximize one metric: zombies killed per minute. 100% vibe coded with this methodology.
  
**Q: I am making an app, not a game, is this the same workflow?**  
**A:** It's mostly the same workflow, yes! Instead of a GDD (Game Design Document), you can do a PRD (Product Requirements Document). You can also use great tools like v0, Lovable, or Bolt.new to prototype first and then move your code to GitHub, and then clone it to continue on VSCode or in the terminal with this guide.

**Q: Your plane in your dogfight game is amazing, but I can’t replicate it in one prompt!**  
**A:** It’s not one prompt—it’s ~30 prompts, guided by a specific `plane-implementation.md` file. Use sharp, specific prompts like “cut out space in the wings for ailerons,” not vague ones like “make a plane.”

**Q: Why is Codex better than Cursor right now?**
**A:** It really is up to your liking. We highlight that Codex is better at using **OpenAI GPT-5.4 (high)** than Cursor is. Having it live in the terminal unlocks many more development workflows: working from any IDE, hopping onto a remote server through SSH, and so on. There are powerful customization options such as custom commands, sub-agents, and hooks that will speed up both the quality and the pace of development over time. Finally, if you’re on the lower-tier ChatGPT plan, that’s enough to get started.

**Q: I don't know how to set up a server for my multiplayer game**  
**A:** Ask your AI.
---
