---
title: "Using AI Efficiently"
date: 2026-06-23
draft: false
tags: ["AI", "Claude", "developer tools", "productivity"]
---

# Using AI Efficiently

The idea behind this blog is simple: to show the tools and skills that make working with AI a lot smoother. We will look at what each one does, how it helps everyday work, and how it quietly saves tokens along the way. We will not go deep into installation here. Each tool has an official GitHub page that walks us through setup far better than we ever could, and the link is right under each heading so one can jump straight to it.

First, a quick word on tokens, since they come up a lot below. Tokens are the unit AI runs on. Everything we send it and everything it sends back is measured in tokens, and that is what we pay for. So when a tool "saves tokens," it really means lower cost, longer working sessions before the AI gets tired or forgetful, and an AI that stays sharp because it is not buried in noise. With that in mind, let us look at the tools.

There are plenty of tools available on the internet right now, but here we will focus on the ones I have been using for a while.

---

## 1. Caveman

**What it is:** Caveman is a skill that makes the AI talk in short, blunt sentences, like a caveman. It drops all the polite filler, long intros, and over-explaining, but keeps every bit of the actual technical answer. Brain stays big, mouth gets small.

**How it helps your work:** You get the answer without wading through three paragraphs to find it. The fix, the reason, the next step, that is all you see. Whether you are deep in code or just asking a quick question, replies come back tight and fast, which honestly makes the AI nicer to read, not just cheaper.

**How it saves tokens:** Caveman cuts tokens by simply making the AI use fewer words to say the same thing. Here is the example straight from their page:

> 🗣️ **Normal Claude (69 tokens):** "The reason your React component is re-rendering is likely because you're creating a new object reference on each render cycle. When you pass an inline object as a prop, React's shallow comparison sees it as a different object every time, which triggers a re-render. I'd recommend using useMemo to memoize the object."
>
> 🪨 **Caveman Claude (19 tokens):** "New object ref each render. Inline object prop = new ref = re-render. Wrap in `useMemo`."

Same fix, same accuracy, about 70% fewer words. Now picture that across a whole day. If almost every reply shrinks like that, a chat that would have burned through your limit by lunch can keep going till evening. The savings are small on one reply but huge over a full session.

**A quick scenario:** You are debugging an auth bug. Normal AI starts with "Sure! I'd be happy to help you with that..." and then explains. Caveman just says: "Bug in auth middleware. Token expiry check use `<` not `<=`. Fix:" and gives it. You read it in two seconds and move on.

**GitHub:** https://github.com/JuliusBrussee/caveman

---

## 2. RTK (Rust Token Killer)

**What it is:** RTK is a small tool that sits quietly between your terminal and the AI. When the AI runs a command, RTK cleans up the messy output before the AI ever reads it, keeping only the part that actually matters.

**How it helps your work:** Commands like `git status`, `cargo test`, or `kubectl get pods` often spit out hundreds of lines, most of it noise. RTK strips that down so the AI sees only the signal. It works through a hook, so you do nothing different. You type your normal commands and RTK handles the rest in the background.

**How it saves tokens:** This is one of the biggest single wins, around 60 to 90 percent on common commands. The clever part is that nothing important is thrown away. Errors, diffs, and stack traces are kept in full. RTK only removes the boring, repetitive stuff that nobody, not even the AI, needed to read.

**How it helps the context window:** Noisy command output is the number one thing that clogs up an AI's memory during a session. By cutting that clutter, your sessions last far longer before the AI starts losing track of what you were doing earlier.

**A quick scenario:** The AI runs your test suite. Normally that is 200 lines of passing tests scrolling by. With RTK, the AI just gets "262 passed, 3 failed" along with the details of those 3 failures. It instantly knows what is wrong without reading the 262 that were fine.

**GitHub:** https://github.com/rtk-ai/rtk

---

## 3. OpenSpec

**What it is:** OpenSpec is a way of working where you and the AI agree on *what* to build before any code is written. Instead of a vague request and a hope for the best, you get a clear written plan first, then the AI builds exactly that.

**How it helps your work:** This is where OpenSpec really shines. When you run its propose command with your idea, it does not start coding. Instead it creates a small set of files in your project that lay out the whole plan: a **proposal** explaining why and what is changing, a **specs** file with the detailed requirements, a **design** file for the technical approach, and a **tasks** checklist of the actual steps. In short, it asks "is *this* what you want to build?" and shows you the full picture before lifting a finger.

You then read it over. If something is off, you ask for changes and it updates the plan. Once you are happy, you run the apply command, and the AI builds exactly what was agreed, ticking off the task list one by one. It does the asked work and nothing extra, no surprise detours.

**How it saves tokens:** Most wasted tokens in AI coding come from the AI guessing wrong, you correcting it, and that back-and-forth piling up. OpenSpec removes the guessing. Because the plan is agreed up front, the AI gets it right the first time far more often, which means fewer expensive correction loops.

**How it helps the context window:** Fewer correction loops means less messy back-and-forth filling up the AI's memory. The session stays focused on building the thing, instead of getting tangled in undoing and redoing.

**A quick scenario:** You want to add a dark mode to your app. You run propose, and OpenSpec writes out the plan: which files change, how the toggle works, where the setting is saved. You glance through, notice it forgot to remember the user's choice, ask it to add that, and it updates the plan. You hit apply, and dark mode gets built correctly in one clean pass.

**GitHub:** https://github.com/Fission-AI/openspec

---

## 4. CLAUDE.md (project memory)

**What it is:** CLAUDE.md is a plain file the AI reads automatically every time it starts working on your project. Think of it as a sticky note for the AI: it holds the few things the AI should just *know* about your project without you repeating them.

**How it helps your work:** Without it, you end up explaining the same things over and over, every new session. With it, the AI already knows your setup, your house rules, and the little traps to avoid. It is like the difference between a new hire you have to brief every morning, and one who already knows how your team works.

**How it saves tokens:** A good CLAUDE.md saves you from re-typing the same context again and again across sessions. The trick is to keep it short. Only put in things that would genuinely surprise someone new to your project. A bloated file actually backfires, because the AI reads it on every single message, and that costs tokens each time.

**How it helps the context window:** You can place a CLAUDE.md inside a specific folder, and it only loads when the AI is working in that folder. So while you are editing the website, the AI is not carrying around rules about your payment system. Less unrelated stuff in memory means more room for the work at hand.

**A quick scenario:** Imagine your team always writes dates as day-month-year, never month-day-year, because a mix-up once caused a real headache. Instead of catching the AI every time, you write one line in CLAUDE.md: "Always use day-month-year for dates." From then on, it just gets it right, and you never think about it again.

**Reference:** https://docs.claude.com/en/docs/claude-code/memory

---

## 5. Custom slash commands

**What it is:** A slash command is a saved instruction you trigger by typing a short `/name`. You write the full instruction once, and from then on you call it with a couple of keystrokes instead of typing the whole thing out every time.

**How it helps your work:** Everyone has a handful of things they ask for again and again. A slash command turns each of those into a one-word shortcut, and it runs the same way every single time, so the results stay consistent. This is not just for coding. On the technical side, you might make a `/review` command that checks your latest code changes for bugs, or a `/test` command that runs your tests and fixes what breaks. On the non-technical side, you could make a `/summary` command that turns long notes into three clean bullet points, or a `/reply` command that drafts a polite response to a customer email in your usual tone. Anything you repeat, you can save.

**How it saves tokens:** You can point a command at a cheaper, faster model for the routine stuff, which keeps the bigger, pricier model free for the hard problems. You also stop rebuilding the same request from scratch each time, which would otherwise burn the same tokens again for the same result.

**A quick scenario:** Every Friday you write a short update on what changed during the week. Instead of explaining the format each time, you make a `/weekly` command that already knows your style: pull the week's changes, group them, and write a friendly three-line summary. Now your Friday update is one word away.

A small heads-up: in newer versions, slash commands and skills are merging into one feature. For a fixed instruction you trigger by hand, a simple command works great. For something you want the AI to reach for on its own, a skill is the better fit.

**Reference:** https://docs.claude.com/en/docs/claude-code/slash-commands

---

## How they work together

The nice thing is that these tools do not overlap. Each one cleans up a different corner of your workflow, so they stack neatly. RTK cleans the messy command output before it reaches the AI. CLAUDE.md makes sure the AI already knows your project. Caveman trims the AI's replies down to the essentials. OpenSpec stops wasted rework by agreeing on the plan first. And slash commands save you from repeating yourself.

If you are just starting, RTK is the easiest first win, especially if you work in the terminal a lot, because it runs invisibly once set up. After that, keep a lean CLAUDE.md, try Caveman for a few sessions, and add slash commands as you notice yourself typing the same thing twice. The more you lean on AI, the more all of this adds up.