# AIS-OS Intake

This is the source-of-truth file for your AIOS. Fill it in by typing, voice-pasting (Wispr Flow / OS dictation), or running `/onboard` for a guided conversation. Whichever mode, this file is what `/onboard` reads to scaffold your Day-1 setup.

**Hard cap: 7 questions.** Each answerable in under 60 seconds. Don't overthink — you can edit and re-run `/onboard` any time.

---

## Q1 — Who are you, what do you sell, who do you sell it to?

Identity, offer, ICP. One paragraph each is fine.

```
I'm MKM. I build agentic apps that solve problems everyday people face.
```

---

## Q2 — Paste 1-2 things you've written recently. Don't edit them.

An email, a LinkedIn post, a DM, a doc — anything that sounds like you when you're not trying. **Paste verbatim.** Do not type these mid-conversation with Claude — chat-shaped samples are worse than no samples (voice contamination).

```
[Sample 1 — paste raw]
Do some research for me about job search and job application in South Africa. Look for highly effective methods and highly reputable places to look for work. Furthermore I want you to then dive in deep into work for disabled people. Don't just limit it to work. Look for programs, bazaars, internships, articled clerkships, and whatever there is out there geared at helping disabled people to fit in the workplace. Make sure that it is South Africa focused.  
  
After that search how we can best use AI tools to further find better opportunities. Take all of that research and give me a summary that I want to give to my AI developer. Your aim is to guide it into creating a job search engine geared for disabled people and then it will be able to use this summary to better build that engine. It shouldn't be overly complex like Google search engine but it should be really good enough to find reputable job opportunities for disabled people.
```

```
[Sample 2 — paste raw]
If I were to create a mentor agent, the first thing would be the sole.md. I would give it the characteristics and traits of my mentors in real life: people that motivate me, people who are good teachers, people who are leaders in a certain field. I would give it their soul, their characteristics, traits, work ethic, vision, morality, a sense of direction.  
  
Inside the agent.md, I think, is where I would define the workflows of the agent: what it does, its role, its rule pertaining to the task, and how it does it and what rules to follow. This is, for me, where the instruction list of the agent will go. This is what will dictate whether it is a capable agent in terms of output or not.  
  
I also find that the agent.md is where you get to refine the procedures the agent will be able to execute. The heartbeat.md, I believe, is scheduling: how often you wanted to run, how you wanted to run, should it wait for you, or should it just take a goal from you and run with it. The tools.md is basically giving it its legs and its hands so that it can do certain things, if you wanted to go and write emails for you, go and launch campaigns on Twitter and such things for you.
```

---

## Q3 — What are your 2-3 biggest priorities for the next 90 days?

Quarterly priorities. Not yearly aspirations. Things that, if not done by July, would make you say "I wasted Q2."

```
1. Launch Sheahaircare app
2. Finish the Vault — agentic system that runs Sheahaircare as if a real team/company operates it
3. Build an agentic app company running multiple apps, managed by agents + a team of 3-5 people
```

---

## Q4 — Where does revenue actually land, and where is it tracked?

Multiple answers OK. Stripe? Skool? GoHighLevel? QuickBooks? A spreadsheet?

```
Paystack. No tracking setup yet, but Paystack offers tracking and an admin page exists for it.
```

---

## Q5 — Where do you talk to customers, your team, and the outside world day-to-day?

Email (which one — Gmail / Outlook)? Slack? Teams? DMs (Skool / Discord / iMessage)? Phone?

```
Gmail, WhatsApp, phone calls. No team yet.
```

---

## Q6 — Where do meeting recordings, notes, and important docs live?

Granola? Otter? Fireflies? Google Drive? Notion? Dropbox? A folder on your desktop you keep meaning to organize?

```
Google Drive and desktop.
```

---

## Q7 — What's the one task that eats your week, and where do you currently track work?

The single biggest time-suck or recurring drudgery. Plus where tasks/projects live (ClickUp / Asana / Linear / Notion / a notebook).

```
Coding eats my week the most (outside of work). Tasks live in my head. Not much admin yet — just building every day.
```

---

When this file is filled, run `/onboard` (or re-run it) and the wizard will scaffold your Day-1 file set: `context/`, `references/voice.md`, populated `connections.md`, and a filled `CLAUDE.md`.
