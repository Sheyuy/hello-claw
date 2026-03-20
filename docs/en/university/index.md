# Skills in Practice: Scenario Index and Selection Principles

This section collects skill combinations and deployment workflows organized by scenario. The goal is to run reusable automation loops with as few skills as possible.

Skills come from two sources: **ClawHub (original)** and **Chinese ClawHub (Tencent SkillHub)**.

[Open ClawHub (original)](https://clawhub.ai/) | [Open Chinese ClawHub (Tencent SkillHub)](https://skillhub.tencent.com/#categories)

Keep your skill count low. Installing too many skills crowds the context window, leading to slower responses, weaker judgment, and higher debugging costs.
One goal only: select by scenario, prioritize stability and maintainability first.

## 1. Top Recommendation: Learn to Use ClawHub First

If you only remember one thing, remember this:

1. Go to [ClawHub (original)](https://clawhub.ai/) or [Chinese ClawHub (Tencent SkillHub)](https://skillhub.tencent.com/#categories) and search for skills by category
2. Install with `clawhub install <skill-slug>`
3. Immediately test with a real task after installing

```bash
clawhub install <skill-slug>
```

ClawHub is the "skill dock" for OpenClaw skills: uploading, versioning, searching, and installing all happen through it. You can use either the original or Chinese entry point as needed.
For a more systematic category index with examples, check the community-curated repository directly:

- [awesome-openclaw-skills (5,000+ categorized skills)](https://github.com/VoltAgent/awesome-openclaw-skills)
- [ClawHub (original)](https://clawhub.ai/)
- [Chinese ClawHub (Tencent SkillHub)](https://skillhub.tencent.com/#categories)

If you prefer not to install the CLI globally, you can also use a one-off command:

```bash
npx clawhub@latest install <skill-slug>
```

You can also search these keywords online to get started quickly:

- `clawhub install`
- `clawhub skills`
- `clawhub openclaw`

## 2. Selection Principles: The Shortest Path to a Stronger Claw

- Beginners should keep **5–10** high-frequency skills active at all times
- Install "chassis skills" first: search, browser, code repository, knowledge base, calendar/email
- For every new skill added, run it through a real task first
- Clear out rarely used skills weekly to avoid context pollution

## 3. The Skills Menu (Order by Category)

Below is a menu-style summary organized by the category structure from `list.md`.
Each category lists a few representative skills that are quick to pick up and highly reusable. For the full list, see the Awesome index or ClawHub.

| Category (list.md) | Recommended skills (examples) | Best for |
|---|---|---|
| Coding Agents & IDEs (1222) | `github`, `code-reviewer`, `git-ops` | Daily development, PR reviews, repo collaboration |
| Browser & Automation (335) | `agent-browser`, `playwright`, `summarize` | Web scraping, form automation, information extraction |
| Productivity & Tasks (206) | `todoist`, `notion`, `obsidian` | Task management, knowledge capture, personal workflows |
| Communication (149) | `slack`, `agentmail`, `gog` | Messaging, email handling, team coordination |
| Search & Research (350) | `tavily-search`, `hackernews`, `summarize` | Web search, news tracking, quick research |
| DevOps & Cloud (409) | `devops`, `aws-infra`, `azure-devops` | Deployment, cloud resource management, pipelines |
| Web & Frontend Development (938) | `agent-browser`, `playwright`, `github` | Frontend integration, UI testing, automated regression |
| Calendar & Scheduling (65) | `caldav-calendar`, `gog`, `todoist` | Scheduling, conflict detection, reminders |
| Notes & PKM (71) | `obsidian`, `notion`, `summarize` | Note archiving, knowledge linking, long-term memory |
| Security & Passwords (53) | `skill-vetter`, `1password`, `amai-id` | Skill security checks, risk alerts |
| PDF & Documents (111) | `summarize`, `add-watermark-to-pdf`, `agentmail` | Document summaries, report processing, attachment workflows |
| Smart Home & IoT (43) | `home-assistant`, `weather`, `gog` | Home automation, life assistant integrations |

## 4. Suggested Curriculum (Copy Directly)

### 4.1 Starter Kit of 5

```bash
clawhub install skill-vetter
clawhub install tavily-search
clawhub install agent-browser
clawhub install github
clawhub install gog
```

### 4.2 Advanced Add-ons (Pick One or Two as Needed)

- Content creation: `x-api`, `linkedin`, `blogburst`
- DevOps engineering: `devops`, `aws-infra`, `azure-devops`
- Personal assistant: `weather`, `caldav-calendar`, `agentmail`

## 5. Further Learning

- Full category index and large skill library:
  [awesome-openclaw-skills](https://github.com/VoltAgent/awesome-openclaw-skills)
- Skill publishing, versioning, and installation:
  [ClawHub (original)](https://clawhub.ai/) | [Chinese ClawHub (Tencent SkillHub)](https://skillhub.tencent.com/#categories)
- Tools chapter in this tutorial (toolsets, scheduled tasks, web search):
  [Chapter 7: Tools and Scheduled Tasks](/en/adopt/chapter7/)
- Skill development and publishing workflow:
  [Appendix D: Skill Development and Publishing Guide](/en/appendix/appendix-d)
- Skill development in practice (local health management):
  [Skill Development in Practice: Local Health Management Assistant](/en/university/local-health-assistant/)

**One-sentence graduation requirement**: The key to making the claw "useful" is not installing the most skills, but installing the right ones.
Pick 5 from this menu first, get your own first automation loop running, then keep adding.
