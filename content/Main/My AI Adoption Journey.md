---
share: true
---

2026-03-22  15:58
Tags:[[Technical Literacy|Technical Literacy]]

https://mitchellh.com/writing/my-ai-adoption-journey
I really like this article.

## Step 1: Drop the Chatbot

## Step 2: Reproduce Your Own Work
The next phase on my journey I tried [Claude Code](https://github.com/anthropics/claude-code). I'll cut to the chase: I initially wasn't impressed. I just wasn't getting good results out of my sessions. I felt I had to touch up everything it produced and this process was taking more time than if I had just done it myself. I read blog posts, watched videos, but just wasn't that impressed.

Instead of giving up, I **forced myself to reproduce all my manual commits with agentic ones.** I literally did the work twice. I'd do the work manually, and then I'd fight an agent to produce identical results in terms of quality and function (without it being able to see my manual solution, of course).

But, expertise formed. I quickly discovered for myself from first principles what others were already saying, but discovering it myself resulted in a stronger fundamental understanding.

1. Break down sessions into separate clear, actionable tasks. Don't try to "draw the owl" in one mega session.
2. For vague requests, split the work into separate planning vs. execution sessions.
3. If you give an agent a way to verify its work, it more often than not fixes its own mistakes and prevents regressions.

## Step 3: End-of-Day Agents

To try to find some efficiency, I next started up a new pattern: **block out the last 30 minutes of every day to kick off one or more agents.** My hypothesis was that _perhaps_ I could gain some efficiency if the agent can make some _positive progress_ in the times I can't work anyways. Basically: instead of trying to do more in the time I have, try to do more in the time I don't have.

Similar to the previous task, I at first found this both unsuccessful and annoying. But, I once again quickly found different categories of work that were really helpful:

- **Deep research sessions** where I'd ask agents to survey some field, such as finding all libraries in a specific language with a specific license type and producing multi-page summaries for each on their pros, cons, development activity, social sentiment, etc.
- **Parallel agents attempting different vague ideas I had but didn't have time to get started on.** I didn't expect them to produce something I'd ever ship here, but perhaps could illuminate some unknown unknowns when I got to the task the next day.
- **Issue and PR triage/review.** Agents are good at using `gh` (GitHub CLI), so I manually scripted a quick way to spin up a bunch in parallel to triage issues. I would NOT allow agents to respond, I just wanted reports the next day to try to guide me towards high value or low effort tasks.

To be clear, I did not go as far as others went to have agents running in loops all night. In most cases, agents completed their tasks in less than half an hour. But, the latter part of the working day, I'm usually tired and coming out of flow and find myself too personally inefficient, so shifting my effort to spinning up these agents I found gave me a "warm start" the next morning that got me working more quickly than I would've otherwise.

## Step 4: Outsource the Slam Dunks

By this point, I was getting very confident about what tasks my AI was and wasn't great at. I had really high confidence with certain tasks that the AI would achieve a mostly-correct solution. So the next step on my journey was: **let agents do all of that work while I worked on other tasks.**

More specifically, I would start each day by taking the results of my prior night's triage agents, filter them manually to find the issues that an agent will almost certainly solve well, and then keep them going in the background (one at a time, not in parallel).

Meanwhile, **I'd work on something else.** I wasn't going to social media (any more than usual without AI), I wasn't watching videos, etc. I was in my own, normal, pre-AI deep thinking mode working on something I wanted to work on or had to work on.

**Very important at this stage: turn off agent desktop notifications.** Context switching is very expensive. In order to remain efficient, I found that it was my job as a human to be in control of when I interrupt the agent, not the other way around. Don't let the agent notify you. During natural breaks in your work, tab over and check on it, then carry on.

## Step 5: Engineer the Harness

At risk of stating the obvious: agents are much more efficient when they produce the right result the first time, or at worst produce a result that requires minimal touch-ups. The most sure-fire way to achieve this is to give the agent fast, high quality tools to automatically tell it when it is wrong.

I don't know if there is a broad industry-accepted term for this yet, but I've grown to calling this "harness engineering." It is the idea that anytime you find an agent makes a mistake, you take the time to engineer a solution such that the agent never makes that mistake again. I don't need to invent any new terms here; if another one exists, I'll jump on the bandwagon.

This comes in two forms:

1. **Better implicit prompting (AGENTS.md).** For simple things, like the agent repeatedly running the wrong commands or finding the wrong APIs, update the `AGENTS.md` (or equivalent). Here is [an example from Ghostty](https://github.com/ghostty-org/ghostty/blob/ca07f8c3f775fe437d46722db80a755c2b6e6399/src/inspector/AGENTS.md). Each line in that file is based on a bad agent behavior, and it almost completely resolved them all.
    
2. **Actual, programmed tools.** For example, scripts to take screenshots, run filtered tests, etc etc. This is usually paired with an AGENTS.md change to let it know about this existing.
    

**This is where I'm at today.** I'm making an earnest effort whenever I see an agent do a Bad Thing to prevent it from ever doing that bad thing again. Or, conversely, I'm making an earnest effort for agents to be able to verify they're doing a Good Thing.

## Step 6: Always Have an Agent Running

Simultaneous to step 5, I'm also operating under the goal of **having an agent running at all times.** If an agent isn't running, I ask myself "is there something an agent could be doing for me right now?"

I particularly like to combine this with slower, more thoughtful models like Amp's [deep mode](https://ampcode.com/news/deep-mode) (which is basically just GPT-5.2-Codex) which can take upwards of 30+ minutes to make small changes. The flip side of that is that it does tend to produce very good results.

**I'm not [yet?] running multiple agents, and currently don't really want to.** I find having the one agent running is a good balance for me right now between being able to do deep, manual work I find enjoyable, and babysitting my kind of stupid and yet mysteriously productive robot friend.

The "have an agent running at all times" goal is still just a goal. I'd say right now I'm maybe effective at having a background agent running 10 to 20% of a normal working day. But, I'm actively working to improve that.

**I don't want to run agents for the sake of running agents.** I only want to run them when there is a task I think would be truly helpful to me. Part of the challenge of this goal is improving my own workflows and tools so that I can have a constant stream of high quality work to do that I can delegate. Which, even without AI, is important!

---
