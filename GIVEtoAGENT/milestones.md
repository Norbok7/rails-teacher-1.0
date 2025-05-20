# Interactive Rails Full-Stack Roadmap (No-Scaffold Edition — **MCQ Mode**)

> **Note:** All setup commands assume you are already in the project root directory. Use `rails` (not `bin/rails`) for all commands. Gems are installed automatically before starting the MCQ loop.

**Purpose** → Teach Rails 8 full-stack by _running the code_, letting the first runtime error surface the next learning objective, and quizzing the learner with a **multiple-choice prompt** that ties back to community best-practice principles (see `bestpractice.md`).

> _Learning = Red → Question → Green → Why._

---

## 0. Manual Project Bootstrap (Run These Steps First)

Before starting the MCQ-driven milestones, you must manually set up your Rails project. Run the following commands in your terminal, step by step:

```bash
# 1. Create a new Rails project (if not already created)
rails new library_tracker \
  --database=postgresql \
  --skip-test --skip-system-test --skip-javascript --skip-hotwire
cd library_tracker

# 2. Install required learning gems
# (If you see errors, run 'gem install bundler' first)
bundle add rspec-rails factory_bot_rails faker devise pundit \
           hotwire-rails sidekiq pry-byebug bullet \
           rubocop rubocop-rails rubocop-performance brakeman \
           --group="development,test"

# 3. Set up database and tools
gem install rails # Ensure latest rails is available
rails db:create
rails g rspec:install
rails g stimulus:install     # later for Hotwire
```

_Once you have completed these steps, your app is ready for the interactive MCQ learning loop. No application code exists yet._

---

## Devise Authentication Setup (Step-by-Step)

1. **Install Devise**

   - `rails generate devise:install`
   - _What it does:_ Sets up Devise's configuration files, adds initializers, and provides setup instructions. This prepares your app for authentication features.

2. **Generate the User model**

   - `rails generate devise User`
   - _What it does:_ Creates a `User` model with Devise modules, migration for user authentication fields, and updates routes for user registration and sessions.

3. **Run the migration**

   - `rails db:migrate`
   - _What it does:_ Applies the generated migration, creating the `users` table with all necessary authentication fields in your database.

4. **Update navigation and views**
   - _What it does:_ Add links for login, signup, and logout to your navbar, and update views to use Devise helpers for user authentication state.

---

## Devise Authentication Access

To access the Devise login and registration forms:

- Visit `/users/sign_in` in your browser to see the login form.
- Visit `/users/sign_up` to see the registration form.

These routes are provided automatically by Devise when you have `devise_for :users` in your `routes.rb`.

After confirming that `/users/sign_in` works in your browser, answer the following multiple-choice question:

**MCQ: What is the best way to help users easily navigate to the login page?**

A) Add a direct link to `/users/sign_in` in your application layout or navbar
B) Tell users to type the URL manually every time
C) Only allow login via API requests
D) Other (custom): **********\_\_**********

_Choose A, B, C, or D and briefly explain why!_

---

## 1. The **Error-Driven MCQ Loop** (repeats for each feature)

| Phase                   | Agent responsibility                                                                                                                                                                                                                                                                   | Your role                                                                                                      |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Run & Capture**       | Visit or interact with `localhost:3000` in the browser, capture the **first runtime error** that appears in the web UI.                                                                                                                                                                | Trigger the error by using the app in your browser (not the terminal).                                         |
| **Quiz Prompt**         | Generate a **multiple-choice question** (MCQ) with 2–4 **relevant next steps** (order and correct answer will vary), plus an **“Other (custom)”** option. **Each MCQ and explanation must reference both `milestones.md` and `bestpractice.md` to justify the choices and reasoning.** | Reply with **A / B / C / D** (or your own choice) **and briefly explain _why_ this is the correct next step.** |
| **Implement & Explain** | ◾ Write/patch code following the selected option. ◾ Run RuboCop, Bullet, Brakeman, & RSpec. ◾ If green: commit & open PR. ◾ Post a **“Why we built this”** blurb (≤ 4 lines) explaining the principle at play, referencing `bestpractice.md` and the current milestone.            | Review the PR & blurb; merge when satisfied.                                                                   |
| **Feedback**            | After each user answer, the Agent will say if the answer is correct, partially correct, or incorrect, and explain why, referencing both files. If incorrect, the user can select again.                                                                                                |                                                                                                                |

> **Speed rule:** Each loop should complete in < 5 minutes so the feedback feels immediate.

---

## 2. Milestone Sequence (12 Issues)

Below are the _expected_ first errors and the MCQ the Agent will ask. Each row is an Issue with the loop above until it’s merged. **The order of MCQ answers will be varied, and the correct answer will not always be the first option.**

| #   | First Runtime Error (on localhost:3000)         | Proposed Choices (Agent may tweak and reorder)                                        | Principle Highlight                                |
| --- | ----------------------------------------------- | ------------------------------------------------------------------------------------- | -------------------------------------------------- |
| 1   | `ActionController::RoutingError` “/”            | 1) Add HomeController#index & set `root` (✓) 2) Generate Book model 3) Install Devise | Keep navigation working before touching DB / auth. |
| 2   | No Book model/table (NameError in browser)      | 2) Generate Book model & migrate (✓) 1) Add Devise 3) Add navbar                      | Model before UI/auth.                              |
| 3   | No BooksController or views (MissingController) | 3) Generate BooksController with CRUD (✓) 1) Add seed data 2) Add Devise              | RESTful CRUD, MVC separation.                      |
| 4   | Home page does not show books                   | 2) Query Book in HomeController#index & render in view (✓) 1) Add books to seeds.rb   | MVC: controller fetches, view renders.             |
| 5   | Manual book routes in routes.rb                 | 1) Use only `resources :books` (✓) 2) Keep manual routes 3) Add custom route          | RESTful, DRY routes.                               |
| 6   | ...                                             | ...                                                                                   | ...                                                |

---

## 2a. How to Trigger the Next Error

To move to the next milestone, visit `http://localhost:3000/books` in your browser. This will attempt to access the books resource, which does not exist yet, and should trigger the next error needed for the learning loop. Once you see the error, continue with the MCQ prompt.

---

## MCQ Guidelines and Quick Reference (Read by Copilot Agent)

As your Copilot Agent, I will guide you through each milestone using the following approach:

- **You will create the next bug:** For each milestone, you will attempt to visit a relevant page or perform an action in your Rails app (e.g., open the home page, try to create a book, etc.) in your browser. Do not look at the error in the console or logs yet—just trigger the error naturally by using the app as a user would.
- **I will surface the error:** I will capture the first error that appears in your browser and present it to you as a learning opportunity. I will not tell you the exact error message up front.
- **MCQ Prompt:** I will then present a multiple-choice question (MCQ) with 2–4 possible next steps (plus an “Other (custom)” option). Each MCQ and its explanation will reference both best practices and milestones.
- **Your Response:** Reply with the letter (A/B/C/D) and a brief explanation of why you think it’s the correct next step. If you want to propose a different action, choose “Other” and explain.
- **Feedback:** I will tell you if your answer is correct, partially correct, or incorrect, and explain why, referencing both files. If incorrect, you can try again.
- **Implementation:** I will implement the correct next step, and always explain what was changed and why, referencing both files. I will also post a short “Why we built this” blurb referencing both files.
- **Reflection:** After each step, you are encouraged to write a 1–2 sentence reflection: “What did you learn? What was confusing?”

| **Explicit MCQ Labels** | All MCQs use A/B/C/D labels. Respond with the letter and a brief reason. |
| **Reference Principles** | MCQ explanations cite specific best practice numbers/sections. |
| **Clarify Content Changes** | The Agent must always clarify when adding or editing HTML, ERB, or other content files, specifying what was added or changed and why. |
| **Feedback Template** | Feedback: "Correct/Incorrect/Partially correct. Here’s why (see milestone X, best practice Y)..." |
| **Why We Built This** | After each step, I will include a short "Why we built this" blurb referencing both files. |
| **Encourage Questions** | Ask why at any step; I will always explain. |
| **MCQ Randomization** | MCQ answer order is randomized; correct answer is not always first. |
| **Reflection** | After each milestone, write a short reflection on what you learned. |
| **No Error Spoilers** | The Agent must not tell the user what error will happen next; instead, prompt the user to visit the browser and recreate the error themselves before proceeding. |
| **Always Explain** | The Agent must always explain what is being done, why it is being done, and how it relates to best practices and milestones, at every step of the application walkthrough. |

> For a quick reference, see the end of this file for a glossary of common Rails terms and best practices.
> For a more detailed reference, see the [Rails Guides](https://guides.rubyonrails.org/) and the [Ruby Style Guide](https://rubystyle.guide/).

---

## Devise Authentication Testing Milestone

After setting up Devise and adding navigation links, test the following authentication features in your browser:

- **Sign Up:** Go to `/users/sign_up` and create a new user account.
- **Sign In:** Go to `/users/sign_in` and log in with your new account.
- **Log Out:** Use the Logout link in the navbar to log out.

If you encounter any errors during these steps, note the error message and respond with the details. If all steps work, confirm that authentication is functioning as expected.

---
