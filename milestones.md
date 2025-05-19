# Interactive Rails Full-Stack Roadmap (No-Scaffold Edition — **MCQ Mode**)

> **Note:** When using any external gem, always check that it is present in your Gemfile and installed (`bundle install`) before continuing with setup or usage. This prevents missing dependency errors and ensures a smooth workflow.

**Purpose** → Teach Rails 8 full-stack by _running the code_, letting the first runtime error surface the next learning objective, and quizzing the learner with a **multiple-choice prompt** that ties back to community best-practice principles (see `bestpractice.md`).

> _Learning = Red → Question → Green → Why._

---

## Devise Authentication Setup (Step-by-Step)

1. **Install Devise**
   - `bin/rails generate devise:install`
   - _What it does:_ Sets up Devise's configuration files, adds initializers, and provides setup instructions. This prepares your app for authentication features.

2. **Generate the User model**
   - `bin/rails generate devise User`
   - _What it does:_ Creates a `User` model with Devise modules, migration for user authentication fields, and updates routes for user registration and sessions.

3. **Run the migration**
   - `bin/rails db:migrate`
   - _What it does:_ Applies the generated migration, creating the `users` table with all necessary authentication fields in your database.

4. **Update navigation and views**
   - _What it does:_ Add links for login, signup, and logout to your navbar, and update views to use Devise helpers for user authentication state.

---

## 0. One-Time Auto-Bootstrap _(handled by Copilot Agent)_

```bash
rails new library_tracker \
  --database=postgresql \
  --skip-test --skip-system-test --skip-javascript --skip-hotwire
cd library_tracker

# Learning gems (already locked in Gemfile)
bundle add rspec-rails factory_bot_rails faker devise pundit \
           hotwire-rails sidekiq pry-byebug bullet \
           rubocop rubocop-rails rubocop-performance brakeman \
           --group="development,test"

rails db:create
rails g rspec:install
rails g stimulus:install     # later for Hotwire
```

The Agent commits this (`chore: bootstrap app with learning gems`) and sets up GitHub Actions (`rubocop`, `brakeman`, `rspec`). _No application code exists yet._

---

## 1. The **Error-Driven MCQ Loop** (repeats for each feature)

| Phase                   | Agent responsibility                                                                                                                                                                                                                                                                   | Your role                                                                                                      |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Run & Capture**       | Execute `rspec` or `rails server`, capture the **first runtime error**.                                                                                                                                                                                                                | Watch the terminal for the error snippet (it will also be echoed in chat).                                     |
| **Quiz Prompt**         | Generate a **multiple-choice question** (MCQ) with 2–4 **relevant next steps** (order and correct answer will vary), plus an **“Other (custom)”** option. **Each MCQ and explanation must reference both `milestones.md` and `bestpractice.md` to justify the choices and reasoning.** | Reply with **A / B / C / D** (or your own choice) **and briefly explain _why_ this is the correct next step.** |
| **Implement & Explain** | ◾ Write/patch code following the selected option. ◾ Run RuboCop, Bullet, Brakeman, & RSpec. ◾ If green: commit & open PR. ◾ Post a **“Why we built this”** blurb (≤ 4 lines) explaining the principle at play, referencing `bestpractice.md` and the current milestone.            | Review the PR & blurb; merge when satisfied.                                                                   |
| **Feedback**            | After each user answer, the Agent will say if the answer is correct, partially correct, or incorrect, and explain why, referencing both files. If incorrect, the user can select again.                                                                                                |                                                                                                                |

> **Speed rule:** Each loop should complete in < 5 minutes so the feedback feels immediate.

---

## 2. Milestone Sequence (12 Issues)

Below are the _expected_ first errors and the MCQ the Agent will ask. Each row is an Issue with the loop above until it’s merged. **The order of MCQ answers will be varied, and the correct answer will not always be the first option.**

| #   | First Runtime Error                  | Proposed Choices (Agent may tweak and reorder)                                        | Principle Highlight                                |
| --- | ------------------------------------ | ------------------------------------------------------------------------------------- | -------------------------------------------------- |
| 1   | `ActionController::RoutingError` “/” | 1) Add HomeController#index & set `root` (✓) 2) Generate Book model 3) Install Devise | Keep navigation working before touching DB / auth. |
| 2   | No Book model/table                  | 2) Generate Book model & migrate (✓) 1) Add Devise 3) Add navbar                      | Model before UI/auth.                              |
| 3   | No BooksController or views          | 3) Generate BooksController with CRUD (✓) 1) Add seed data 2) Add Devise              | RESTful CRUD, MVC separation.                      |
| 4   | Home page does not show books        | 2) Query Book in HomeController#index & render in view (✓) 1) Add books to seeds.rb   | MVC: controller fetches, view renders.             |
| 5   | Manual book routes in routes.rb      | 1) Use only `resources :books` (✓) 2) Keep manual routes 3) Add custom route          | RESTful, DRY routes.                               |
| 6   | ...                                  | ...                                                                                   | ...                                                |

---

## 3. MCQ Guidelines and Quick Reference

| **Explicit MCQ Labels** | All MCQs use A/B/C/D labels. Respond with the letter and a brief reason. |
| **Reference Principles** | MCQ explanations cite specific best practice numbers/sections. |
| **Feedback Template** | Feedback: "Correct/Incorrect/Partially correct. Here’s why (see milestone X, best practice Y)..." |
| **Why We Built This** | After each step, include a short "Why we built this" blurb referencing both files. |
| **Encourage Questions** | Ask why at any step; the Agent will always explain. |
| **MCQ Randomization** | MCQ answer order is randomized; correct answer is not always first. |

> For a quick reference, see the end of this file for a glossary of common Rails terms and best practices.
