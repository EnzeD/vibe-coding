# Ultimate Guide to Vibe Coding V1.1
**Author:** [Nicolas Zullo, https://x.com/NicolasZu](https://x.com/NicolasZu)  
**Creation Date:** March 12, 2025  
**Last Update Date:** April 24, 2025  

---

## Getting Started
To begin vibe coding, you only need two tools:  
- **Gemini 2.5 Pro Thinking**  
- **Cursor with Claude Sonnet 3.7 Thinking**  

*(Note: While earlier versions of this guide utilized Grok 3, we have transitioned to **Gemini 2.5 Pro**. The primary reasons for this shift are Gemini's impressive 1M token context window, which allows for a much broader understanding of the project, and its capabilities in handling complex software architecture, making it a more powerful partner for this workflow.)*

Setting up everything correctly is key. If you’re serious about creating a fully functional and visually appealing game, take the time to establish a solid foundation.  

**Key Principle:** *Planning is everything.* Do NOT let the AI plan autonomously, or your codebase will become an unmanageable mess.

---

## Setting Up Everything

### 1. Game Design Document
- Take your game idea and ask **Gemini 2.5 Pro Thinking** to create a simple **Game Design Document** in Markdown format: `game-design-document.md`.  
- Review and refine the document to ensure it aligns with your vision. It’s fine if it’s basic—the goal is to give your AI context about the game’s structure and intent.  

### 2. Tech Stack and `.cursor/rules`
- Ask **Gemini 2.5 Pro Thinking** to recommend the best tech stack for your game (e.g., ThreeJS and WebSocket for a multiplayer 3D game). Save this as `tech-stack.md`.
  - Challenge it to propose the *simplest yet most robust stack possible*.  
- In Cursor, open the chat and use the `/Generate Cursor Rules` command with selected the two .md files you created so far. This will create a set of rules `.mdc` under `.cursos/rules`.
- **Crucially, review the generated rules.** Ensure they emphasize **modularity** (multiple files) and discourage a **monolith** (one giant file). You might need to manually tweak or add rules. Review also when they trigger.
  - **IMPORTANT:** Some rules are critical for maintaining context and should be set as **"Always"** rules in Cursor. This ensures the AI *always* refers to them before generating code. Consider adding rules like the following and marking them as "Always":
    > ```
    > # IMPORTANT:
    > # Always read memory-bank/@architecture.md before writing any code. Include entire database schema.
    > # Always read memory-bank/@game-design-document.md before writing any code.
    > # After adding a major feature or completing a milestone, update memory-bank/@architecture.md.
    > ```
  - Example: Ensure other (non-"Always") rules guide the AI towards best practices for your stack (like networking, state management, etc.).
  - *This overall rules setup is mandatory if you want a game that is as optimized as possible, and code as clean as possible.*


### 3. Implementation Plan
- Provide **Gemini 2.5 Pro Thinking** with:  
  - The Game Design Document (`game-design-document.md`)
  - The tech stack recommendations (`tech-stack.md`)
  - The Cursor rules you just configured (you can copy-paste them from the `.cursor/rules` file)
- Ask it to create a detailed **Implementation Plan** in Markdown (`.md`) which is a step-by-step instructions for your AI developers.  
  - Steps should be small and specific.  
  - Each step must include a test to validate correct implementation.  
  - No code—just clear, concrete instructions.  
  - Focus on the *base game*, not the full feature set (details come later).  

### 4. Memory Bank
- Create a new folder for your project, open it in Cursor.
- Inside the project folder, create a subfolder named `memory-bank`.  
- Add the following files to `memory-bank`:  
  - `game-design-document.md`  
  - `tech-stack.md`  
  - `implementation-plan.md`  
  - `progress.md` (Create this empty file for tracking completed steps)  
  - `architecture.md` (Create this empty file for documenting file purposes)  
- *Note: The `.cursor/rules` file will be automatically created in your project's root directory by Cursor when you save the rules in step 2.*

---

## Vibe Coding the Base Game
Now the fun begins!

### Making sure everything is clear
- Select **Claude Sonnet 3.7 Thinking** in Cursor. 
- Prompt: Read all the documents in `/memory-bank`, is `implementation-plan.md` clear? What are your questions to make it 100% clear for you?
- He usually asks 9-10 questions, answer them and prompt him to edit the `implementation-plan.md` accordingly, so it's even better.

### Your first implementation prompt
- Select **Claude Sonnet 3.7 Thinking** in Cursor.  
- Prompt: Read all the documents in `/memory-bank`, and proceed with Step 1 of the implementation plan. I will run the tests. Do not start Step 2 until I validate the tests. Once I validate them, open `progress.md` and document what you did for future developers. Then add any architectural insights to `architecture.md` to explain what each file does.

- **Extreme vibe:** Install [Superwhisper](https://superwhisper.com) to speak casually with Claude instead of typing.  

### Workflow
- After completing Step 1:  
- Commit your changes to Git (if unfamiliar, ask Gemini 2.5 for help).  
- Start a new composer (`Cmd + N`, `Cmd + I`).  
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
- Click “restore” in Cursor and refine your prompt until it works.  
- For errors:  
- **If JavaScript:** Open the console (`F12`), copy the error, and paste it into Cursor—or provide a screenshot for visual glitches.  
- **Lazy Option:** Install [BrowserTools](https://browsertools.agentdesk.ai/installation) to skip manual copying/screenshotting.  
- If stuck:  
- Revert to your last Git commit (`git reset`) and retry with new prompts.  
- If *really* stuck:  
- Use [RepoPrompt](https://repoprompt.com/) or [uithub](https://uithub.com/) to get your whole codebase in one file and ask **Gemini 2.5 Pro Thinking** for assistance.  

---

## Other Tips
- **Small Edits:** Use Claude Sonnet 3.5. or GPT-4.1 
- **Great Marketing Copywriting:** Use GPT-4.5.  
- **Generate Great Sprites (2D images):** Use ChatGPT-4o
- **Generate Music:** Use Suno
- **Generate Sound Effects:** Use ElevenLabs
- **Generate Video:** Use Sora
- **Better prompt outputs:** Add “think as long as needed to get this right, I am not in a hurry. What matters is that you follow precisely what I ask you and execute it perfectly. Ask me questions if I am not precise enough."

---

## Frequently Asked Questions
**Q: I am making an app, not a game, is this the same workflow?**  
**A:** It's mostly the same workflow, yes! Instead of a GDD (Game Design Document), you can do a PRD (Product Requirements Document). You can also use great tools like v0, Lovable, or Bolt.new to prototype first and then move your code to github, and then clone it to continue on Cursor with this guide.

**Q: Your plane in your dogfight game is amazing, but I can’t replicate it in one prompt!**  
**A:** It’s not one prompt—it’s ~30 prompts, guided by a specific `plane-implementation.md` file. Use sharp, specific prompts like “cut out space in the wings for ailerons,” not vague ones like “make a plane.”

**Q: I don't know how to setup a server for my multiplayer game**  
**A:** Ask Gemini 2.5 Pro or ChatGPT-4o.

---
