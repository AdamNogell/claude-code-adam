# Daily paper

Every weekday morning, Claude picks one paper for you to read and sends it to your phone. It runs in the cloud, so your computer can be off. It rotates through four topics you choose, prefers review papers, and only sends papers it actually found and checked that morning.

## What arrives

One short message per weekday:

- the paper's title, authors, journal, date, and a working link or DOI;
- a few sentences on what the paper covers;
- one sentence on why it matters to you, or why people are talking about it;
- whether it is a peer-reviewed review, a peer-reviewed primary study, or a preprint, and whether its findings are preliminary or contested;
- a short confidence and sourcing note, so you can check the details yourself.

## How it works

1. A **scheduled task** starts a fresh cloud session at 7:30 on weekdays.
2. Claude reads a small **rotation log** kept in Claude's memory. The log lists the last 10 to 15 days: date, category, title.
3. It **picks a category** it hasn't used in the last one or two runs. Your core topic comes up most often.
4. It **searches the web** for one real paper (a review if possible) and checks the citation details.
5. It **writes the digest**, **appends today's line to the log**, and the result reaches your phone as a **push notification**.

The whole prompt is in [prompt.md](prompt.md).

## My setup, for reference

Read from the task's own configuration on 2026-10-04.

| Setting | Value |
| :- | :- |
| Created in | Claude desktop app, **Cowork** tab, as a scheduled task |
| Runs | In the cloud (the computer can be off) |
| Schedule | Weekdays, 07:30, Europe/Prague time (cron `30 7 * * 1-5`) |
| Model | Opus 5.5 |
| Permission mode | Auto (nobody is there to approve anything at 7:30) |
| Tools it uses | Web search, web fetch, Claude's memory (for the log) |
| Folders or repositories | None |
| Notifications | Push on, email off |

## Before you start

1. **A paid plan.** Scheduled tasks in Cowork are available on Pro, Max, Team and Enterprise ([support: scheduled tasks](https://support.claude.com/en/articles/13854387-schedule-recurring-tasks-in-claude-cowork)).
2. **Memory turned on.** On claude.ai, open **Settings > Memory** and turn on **Generate memory from chats**. On Team and Enterprise plans an organization Owner decides whether memory is available, and it stays off until you turn it on yourself. Memory is shared between chat and Cowork only when Cowork runs in the cloud, which these scheduled tasks do ([support: memory](https://support.claude.com/en/articles/11817273-use-claude-s-chat-search-and-memory-to-build-on-previous-context)).
   - *My inference, not documented:* the task writes its rotation log with Claude's memory tools, and this setting is what makes them available. The first-run check below confirms it.
3. **The Claude mobile app**, signed in with the same account, if you want the push notification.

## Set it up (the same way as mine)

1. **Fill in [prompt.md](prompt.md):** your name and your four categories.
2. In the **Claude desktop app**, open **Cowork**, click **Scheduled** in the left sidebar, then **New task**, then **Create with Claude** ([support](https://support.claude.com/en/articles/13854387-schedule-recurring-tasks-in-claude-cowork)).
3. **Send this message**, with your filled-in prompt pasted at the end:

   ```text
   Create a scheduled task named "Daily paper" that runs every weekday (Monday to Friday) at 7:30 in the morning, my local time. It should run in the cloud, needs no folders or local files, and should use Opus 5.5. Use the prompt below as the task's instructions exactly as written, without rewording or shortening it. If the task has a notification setting, turn push notifications on.

   [paste the filled-in prompt from prompt.md here: everything from "Your details" to the end of Step 5]
   ```

4. Claude may ask a few questions. **Check the name, schedule and instructions it proposes**, especially that the prompt was not shortened. Then click **Schedule**.

You can also fill in the form yourself: **New task > Set up manually** asks for a name, prompt, approval mode, frequency, model and an optional working folder ([support](https://support.claude.com/en/articles/13854387-schedule-recurring-tasks-in-claude-cowork)). Choose **Weekdays** and leave the folder empty. For approval mode, pick the option that doesn't wait for you; mine runs in Auto. The help article doesn't list the approval-mode options or say whether the manual form takes a time of day, so if you need a specific time, use **Create with Claude**.

## Check the first run

Don't wait until tomorrow. On the **Scheduled** page you can run a task on demand ([support](https://support.claude.com/en/articles/13854387-schedule-recurring-tasks-in-claude-cowork)). Run it once and open the run:

- It should try to read `/areas/morning-review-paper-log.md`. On the first run "doesn't exist yet" is expected. At the end it should write the file.
- The digest's link or DOI should open the paper.
- A push notification should reach your phone.

Run it a second time: it should read the log and pick a different category. If it says the memory tools were unavailable, memory is off (see "Before you start").

## Push notifications

My task has push notifications on, and each run sends the digest summary to my phone. I could not find documentation of where a Cowork scheduled task's push setting lives. If nothing arrives after the first run:

- check that the Claude mobile app is installed and signed in to the same account, and that your phone allows notifications from it;
- look for a notification setting on the task;
- as an untested workaround, add a last line to the prompt: "When you're done, send me a push notification with the paper's title and a one-line summary."

Push or no push, the full digest is always in the run's session in the Claude app.

## Alternative: a Claude Code routine

If you'd rather set it up from Claude Code, the equivalent is a cloud **routine**. Create one with `/schedule` in the CLI, at [claude.ai/code/routines](https://claude.ai/code/routines) with **New routine**, or in the desktop app's **Code** tab under **Routines > New routine > Cloud**. Routines are available on Pro, Max, Team and Enterprise and run on Anthropic's cloud, so they keep working with your laptop closed ([docs: routines](https://code.claude.com/docs/en/routines)). Paste the same filled-in prompt, choose the **Weekdays** schedule (times are in your local zone), and pick the model in the prompt box.

Things that differ from the Cowork setup:

- **Routines are a research preview.** Behavior and limits may change ([docs](https://code.claude.com/docs/en/routines)).
- **Memory is not documented for routines.** I could not confirm that Claude's memory tools exist inside a routine. If they don't, the prompt falls back to a fixed weekday rotation, and you lose the protection against repeats.
- **Connectors:** every connector on your account is included by default, and Claude can use them without asking during a run. Remove the ones this task doesn't need ([docs](https://code.claude.com/docs/en/routines#connectors)).
- **Repository:** the routine form asks for repositories, and this task doesn't need one. The docs don't say whether the step can be skipped.
- **Network:** the Default cloud environment allows only an allowlist of domains, and other requests fail with `403` and `host_not_allowed` ([docs](https://code.claude.com/docs/en/routines#environments-and-network-access)). It's not documented whether web search and fetch go through that path. If runs show `host_not_allowed`, widen the environment's network access.
- **Push:** the Claude Code docs describe push notifications for Remote Control sessions, set with two `/config` toggles ([docs: mobile](https://code.claude.com/docs/en/mobile#get-push-notifications)). They don't describe push for routines.

## Changing it later

- **Topics:** edit "Your details" in the task's prompt.
- **Time or days:** edit the task's schedule on the Scheduled page.
- **Pause:** use the task's pause control on the Scheduled page ([support](https://support.claude.com/en/articles/13854387-schedule-recurring-tasks-in-claude-cowork)).

## Troubleshooting

- **No digest this morning:** check on the Scheduled page that the task is not paused, and open the latest run.
- **The same category every day:** the log is not being written. Open a run and look for errors from the memory tools, then check that memory is on.
- **"Could not read the publisher's page":** some publisher sites block automated access. In my runs, a journal page returned 403 and PubMed Central showed a bot check. The task confirmed the citation through Crossref instead and said so in its sourcing note (run of 2026-10-02).

## Sources

- Cowork scheduled tasks (plans, creation, cloud runs, run on demand, pause): [support.claude.com/en/articles/13854387](https://support.claude.com/en/articles/13854387-schedule-recurring-tasks-in-claude-cowork), retrieved 2026-10-04 (page marked "Updated this week").
- Memory settings and Cowork: [support.claude.com/en/articles/11817273](https://support.claude.com/en/articles/11817273-use-claude-s-chat-search-and-memory-to-build-on-previous-context), retrieved 2026-10-04 (page marked "Updated this week").
- Claude Code routines: [code.claude.com/docs/en/routines](https://code.claude.com/docs/en/routines), retrieved 2026-10-04.
- Push notifications in Claude Code: [code.claude.com/docs/en/mobile](https://code.claude.com/docs/en/mobile), retrieved 2026-10-04.
- My setup and the 2026-10-02 run: the task's configuration and run log, read through the claude.ai routines API on 2026-10-04.
