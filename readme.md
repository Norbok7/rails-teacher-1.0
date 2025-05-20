# Rails 8 Interactive Learning Project (with Copilot Agent)

Welcome! This repo teaches you full-stack Rails 8 by running code, encountering real errors, and learning through multiple-choice questions (MCQs) guided by the GitHub Copilot Agent in VS Code.

## 🚦 Step-by-Step: Getting Started with the Copilot Agent in VS Code

1. **Fork this repo** to your own GitHub account.
2. **Clone your fork locally** and open the folder in VS Code.
3. **Make sure the `milestones.md` file stays in the project root.**
   - This file more or less contains `bestpractice.md` and `milestones.md`, which the Copilot Agent uses to guide your learning. Do not move or delete it.
4. **Install the GitHub Copilot and Copilot Chat extensions** from the VS Code Marketplace if you haven't already.
5. **Enable the Copilot Agent:**
   - Open the Command Palette (`Cmd+Shift+P` on Mac, `Ctrl+Shift+P` on Windows/Linux).
   - Type `Copilot: Enable` or `Copilot Chat: Focus` to activate the agent.
   - Make sure you are signed in to GitHub and Copilot is enabled (look for the Copilot icon in the status bar).
6. **Switch Copilot Chat to Agent Mode:**
   - In the Copilot Chat sidebar, find the dropdown at the top (it may say "Ask" by default).
   - Change the dropdown from **"Ask"** to **"Agent"** mode to activate the Rails MCQ agent workflow.
7. **Open a new Copilot Chat window** (from the sidebar or using the Command Palette).
8. **Start the learning loop by typing:**

   > I want to start the Rails MCQ learning loop. What should I do first?

   Or, follow the "Manual Project Bootstrap" steps in `/milestones.md`.

9. **Follow the Copilot Agent's instructions:**
   - Use your browser to trigger errors in your Rails app.
   - Answer the MCQs in the chat window (A/B/C/D + explanation).
   - Let Copilot handle code changes, explanations, and next steps.

10. **Repeat the loop:**
    - After each step, reflect on what you learned.
    - Continue until you complete all milestones in `/milestones.md`.

## 📝 Tips for Using Copilot Agent

- **Always read `/bestpractice.md` before making changes.**
- **Run RuboCop auto-correct** before committing code (Copilot will remind you).
- **Never commit secrets or raw keys.**
- **Ask Copilot for help or clarification at any step.**
- **Keep your README up to date** with any project-specific notes.

## 🤝 Contributing

- Fork, learn, and share improvements via pull requests.
- If you find a better MCQ or explanation, suggest it!
- Keep all docs and code changes clear and beginner-friendly.

## 📚 References

- [/bestpractice.md](./bestpractice.md): Rails 8 best practices for beginners
- [/milestones.md](./milestones.md): Interactive MCQ roadmap and workflow
- [Ruby Style Guide](https://rubystyle.guide/)
- [Rails Guides](https://guides.rubyonrails.org/)

---

Happy learning! If you get stuck, just ask Copilot for help or clarification at any step.
