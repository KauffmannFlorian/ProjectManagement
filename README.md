# Multi-project delivery tracker

One page that brings together the tools a project manager usually juggles in separate places: portfolio status, schedule, kanban, backlog scoring, RAID log, client dependencies, incidents, delivery metrics and client meeting minutes. It also includes an AI tab that turns the current data into ready-to-use prompts.

> **Status: prototype.** A single static page with fictional data, built to explore the idea and to serve as a demo. It is not a production tool yet (see [Roadmap](#roadmap)).

## Why

A project manager working alongside a tech lead on several projects at once often keeps the schedule in one tool, risks in a spreadsheet, incidents in a ticketing system and client follow-ups in an inbox. Delays then show up late, because the links between these things are made by hand.

The idea here is to keep them in one place **and connected**. A late client deliverable should be visible in the schedule, on the board, in the risk log and in the risk score at the same time.

## What is inside

| Tab | Purpose |
|---|---|
| **Portfolio** | Weekly view: status per project, variance, budget, alerts, next milestones and meetings |
| **Schedule (Gantt)** | Consolidated plan with milestones, slippage and client deliverables shown as circles |
| **Kanban** | Drag-and-drop board with a "Blocked by client" column and a work-in-progress limit |
| **RICE backlog** | Editable scoring (reach, impact, confidence, effort) with live ranking |
| **RAID log** | Risks, actions, issues and dependencies with owners and due dates |
| **Client dependencies** | What development needs from each client, by when, and the impact if it is late |
| **Incidents** | Severity levels, incident flow, indicators, log and a timeline per incident |
| **DORA metrics** | Deployment frequency, lead time, change failure rate, time to restore, over 8 weeks |
| **Client meeting** | Agenda template and filled-in minutes example |
| **AI copilot** | Prompt builder, delay-risk radar, guardrails and a weekly routine |

### About the AI tab

- **Prompt builder.** Pick a task (weekly status report, client chase email, delay-risk scan, meeting notes to actions, post-incident review, RICE check) and a scope. The prompt is filled with the current tracker data. Copy it into any AI assistant. No API key and no network call are involved.
- **Delay-risk radar.** A transparent, rule-based score computed from the other tabs, with the reasons displayed. It is not AI, on purpose: you can see why a project is flagged.
- **Guardrails.** Anonymise before pasting, read before sending, check numbers and dates, and leave technical decisions to the tech lead.

## Run it

No build step and no dependency.

```bash
git clone <your-repo-url>
cd <your-repo>
open index.html   # or double-click the file
```

An internet connection is only needed to load the web font. The page falls back to system fonts offline.

## Publish with GitHub Pages

1. Push `index.html` and this `README.md` to the root of a **public** repository.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and the `/ (root)` folder, then save.
4. After a minute or two, the page is available at `https://<your-username>.github.io/<your-repo>/`.

## Customise the data

Everything lives in `index.html`. The data is defined as plain JavaScript arrays at the top of the `<script>` block:

| Variable | Content |
|---|---|
| `P` | The three projects (name, client, colour) |
| `port` | Portfolio cards: status, progress, go-live, variance, budget, alerts |
| `G` | Gantt rows: tasks, milestones, client deliverables |
| `K0` | Kanban cards (default board) |
| `R` | RICE backlog items |
| `RAID` | RAID log entries |
| `AT` | Client dependencies |
| `INC` | Incidents with their timelines |
| `D` | DORA series per project |

To add a fourth project, add it to `P`, define a colour `--p4` in the CSS and add a `.t4` tag class, then add entries to the other arrays with the new key.

The kanban board and the last opened tab are saved in the browser's `localStorage`. Use **Reset board** to restore the default cards.

## Roadmap

Ideas, roughly in order of value. Nothing here exists yet.

- [ ] Real storage (a small backend or a hosted database) instead of static arrays and `localStorage`
- [ ] Editing every tab in the page, not only the kanban and the RICE values
- [ ] Explicit links between items (a late deliverable linked to its tasks, cards, issues and incidents)
- [ ] Import from issue trackers and code hosts (for example CSV, Jira, GitHub) to avoid double entry
- [ ] Export: weekly status as PDF or Markdown, RAID and dependencies as CSV
- [ ] Optional direct AI calls behind a user-provided key, keeping the copy-paste mode as the default
- [ ] Multi-user access and permissions for sharing a client-safe view

## Limits

- All data is fictional. Do not enter confidential client information in the public version.
- Scores, thresholds and severity targets are illustrative. Align them with your own contracts and practices.
- The delay-risk radar is a simple heuristic, not a forecast.

## Feedback

If you manage several projects with a part-time or advisory role and recognise the problem, opinions are welcome. Open an issue and describe the tools you combine today and what you retype by hand.

## License

Choose a license before sharing widely. [MIT](https://choosealicense.com/licenses/mit/) is a common default for a small project like this.
