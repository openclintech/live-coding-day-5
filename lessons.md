# Vibe Coding Best Practices — Class Lessons

A hands-on class on how to "vibe code" responsibly: letting an AI assistant (Claude)
write code for you, while keeping the habits that real engineers rely on to stay safe.

Audience: largely non-technical. Everything below is explained in plain language.

> **How to use this file (instructor):** Each lesson has two parts — a short
> **teaching script** to say out loud, and a **live demo** with prompts you can
> paste to Claude in front of the class. The 👉 lines are the exact things to
> say/paste.

---

## The big idea

When you "vibe code," you describe what you want and the AI writes the code. That's
powerful — but if you just let changes pile up directly into your live project, one
bad change can break everything and you won't know which one did it.

The habits in this class are how professionals get the *speed* of AI without the *chaos*.
Three habits, three lessons:

1. **Branches & Pull Requests** — make changes in a safe side-copy and review before they go live.
2. **Small, reviewable diffs** — change one small thing at a time so it's easy to check.
3. **Verify & test** — actually run it and confirm it works before you ship.

---

## Lesson 1 — Branches & Pull Requests (PRs)

### Teaching script

👉 "Imagine a Google Doc that everyone shares — the *real* version your audience sees.
You don't want to type directly into it while experimenting, because a mistake is live
immediately. Instead, you make a **copy**, play in the copy, and only merge your changes
back in after someone looks them over."

- **`main`** = the official, live version of the project. Treat it as sacred.
- **Branch** = a safe side-copy where you make changes. Mistakes here can't hurt `main`.
- **Commit** = a saved snapshot of your change, with a short note describing it.
- **Pull Request (PR)** = a formal request that says *"please review my branch and, if it
  looks good, merge it into `main`."* It shows a side-by-side of exactly what changed.
- **Review & merge** = a human looks at the PR, asks questions, and approves. Then the
  change becomes part of `main`.

👉 "Why bother? Three reasons: (1) **safety** — `main` never breaks from half-finished work,
(2) **review** — a second set of eyes catches mistakes before they're live, and
(3) **history** — every change is documented, so if something breaks later we know exactly
what changed and can undo just that piece."

### Live demo — make a tiny change and open a PR

The whole demo is one prompt. Just say:

👉 **"Start lesson 1."**

Claude will make a simple wording change to `app/page.tsx`, then ask whether to
commit and/or open a PR. Say **"do both."** Claude opens the PR and gives you the link.

Then, on screen, review the PR yourself in GitHub:
1. Open the PR link.
2. Click the **"Files changed"** tab — point out the red (removed) / green (added) lines.
   "This is the *diff* — exactly one line changed, and we can see it."
3. (Optional) Approve and **Merge** to show the change going live.

That's it — Lesson 1 is intentionally simple.

---

## Lesson 2 — Small, Reviewable Diffs

### Teaching script

👉 "A **diff** is just *what changed* — the before and after. A *small* diff changes one
thing. A *big* diff changes fifty things at once."

👉 "Ask yourself: if I changed 50 things and the app broke, which change broke it? You'd
have no idea. If I changed *one* thing and it broke, I know exactly what to fix or undo.
Small changes are easier to review, safer to merge, and trivial to reverse."

- One change = one branch = one PR. Keep them focused.
- A good PR can be reviewed in a couple of minutes. If it can't, it's probably too big.
- Smaller changes get reviewed faster and merged sooner — you actually go *faster* overall.

👉 The anti-pattern: "While you're in there, also redesign the whole page" — resist it.
Do the one thing, ship it, then start a fresh change for the next thing.

### Live demo — contrast a small change vs. a big one

👉 First, a clean small change (paste to Claude):
```
On a new branch, change the "Documentation" button label on the homepage to
"Read the Docs". Just that one change. Show me the diff before committing.
```
Point out how tiny and obvious the diff is — anyone could review it in seconds.

👉 Then show the contrast (you don't have to commit this — it's to make the point):
```
For teaching purposes only, describe (don't apply) what the diff would look like
if we instead rewrote the entire homepage layout, changed the colors, and added
three new sections all at once. Roughly how many lines would change?
```
"See how much harder that is to review? That's why we keep changes small."

---

## Lesson 3 — Verify & Test Your Changes

### Teaching script

👉 "The AI is confident even when it's wrong. *Confidence is not correctness.* Before any
change goes live, we **verify**: we actually run the app and look with our own eyes."

- **Don't blindly trust the output.** Code that looks right can still be broken.
- **Run it.** Start the app and check the change actually appears and works.
- **Check it didn't break anything else** — glance at the rest of the page, not just your change.
- Only *after* it's verified do we merge the PR.

👉 "This is the difference between 'the AI said it's done' and 'I confirmed it's done.'
Only one of those is true engineering."

### Live demo — verify a change in the running app

👉 Paste to Claude:
```
Start the dev server so we can see the app in the browser, and tell me the URL.
```
Open the URL on screen and show the heading you changed in Lesson 1 actually appears.

👉 Then have Claude make a deliberately verifiable change and check it:
```
On a new branch, change the homepage heading to "Verified by the class".
Then verify the change is actually showing in the running app, and tell me
exactly how you confirmed it before we open a PR.
```
Talk through: "Notice Claude didn't just say 'done' — it *checked*. That's the habit."

👉 Stop the server when finished:
```
Stop the dev server.
```

---

## Quick reference — the vibe coding loop

1. **Branch** — make a safe side-copy (`git checkout -b my-change`).
2. **Change one small thing** — keep the diff tiny and focused.
3. **Verify** — run the app, confirm it works, check nothing else broke.
4. **Open a PR** — let a human review the exact diff.
5. **Review & merge** — approve, merge into `main`, delete the branch.
6. Repeat.

> The whole point: move fast *and* stay safe. The AI gives you speed; these habits keep you safe.
