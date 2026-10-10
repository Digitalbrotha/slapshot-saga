# Newcomer City 🏢🕹️

A playful, top-down retro onboarding game. Load a markdown file that describes your
company's teams and people, and it becomes a living open-plan office where people
work at their computers, hold meetings, grab coffee and visit colleagues.

Open `index.html` in a browser (no build step, no server needed), or visit
`/newcomer-city/` on the deployed site.

## What you can do

| | |
|---|---|
| **Roam** | `WASD`/arrows to walk (hold `Shift` to run), click the floor to walk there, drag to pan, scroll / `+` `−` to zoom, click the minimap to jump. |
| **Meet people** | Click a person (or stand next to them and press `E`). **Time freezes** and their personnel file opens: avatar, title, what they're doing right now, teams, knowledge, all extra details, bio, and full intel on each of their teams. `Esc` resumes. |
| **Search** | Press `/`. Anything in the file matches: names, titles, teams, knowledge keywords, team responsibilities/areas, extra fields, bios. Pick a hit and the camera flies to that person. |
| **Teams** | Click a team's floor sign or any team chip to see responsibilities, areas, connected teams (also drawn on the minimap) and members. |
| **Missions** | "Find someone who knows X" — follow the yellow arrow. Meeting new people earns respect. |
| **Save game** | Downloads one standalone `.html` file with the game *and* your markdown embedded. Send it to a colleague; it opens straight into the office. |

## File format (schema)

One markdown file, two sections: `# Teams` and `# People`. Each `## heading` inside is one
team or one person. Details are bullet lines `- key: value`; lists are comma separated
(or nested bullets under `- key:`). See [`example-company.md`](example-company.md) for a full example.

```markdown
---
company: Pixel Pines Inc.          # optional
welcome: Welcome aboard!           # optional, shown on the pager
---

# Teams

## Growth
- color: #e4572e                   # optional hex color
- responsibilities: User acquisition, Referral program
- areas: Landing pages, Signup funnel
- connects: Retention, Data Platform

Free text becomes the team description.

# People

## Ada Lindqvist
- title: Head of Growth
- teams: Growth, Data Platform     # required, must match team headings
- knowledge: growth, retention     # required keywords
- email: ada@example.com           # any other key is shown as a detail

Free text becomes the bio.

```avatar
k=#111 s=#f1c9a5 h=#7a3b12 c=#e4572e
..hhhh..
.hsssshh
.sksksss
.ssssss.
..cccc..
.cccccc.
```
```

### Rules

- At least one team and one person. Every person needs `teams` and `knowledge`.
- Team names in `teams` and `connects` must match a `## Team` heading (case-insensitive).
  Connections are two-way. A person's **first** team decides where their desk is.
- **Avatar** (optional): an ` ```avatar ` block. The first line(s) define the palette as
  `char=#hex` (`.` is transparent; a few defaults like `k` black, `w` white, `s` skin exist).
  All rows must be equally wide, max 64×64 (12×12 or 16×16 looks best). Alternatively
  `- avatar: https://…` or a `data:image/…` URI. Without one, a pixel face is generated.
- Aliases: `role`→title, `skills`/`keywords`/`expertise`→knowledge, `team`→teams,
  `connections`/`works with`→connects, `about`→description.
- Problems are reported with line numbers (with "did you mean…?" for misspelled team names).
  Errors block loading; warnings (e.g. a team without members) don't.

## Notes

- The example in `example-company.md` is also embedded in `index.html` (in the
  `<script id="example-md">` tag) for the "Play example company" and "Download template"
  buttons — update both if you change it.
- Progress (people met, respect) is remembered per company in the browser's local storage.
- Fonts load from Google Fonts; offline it falls back to a monospace font.
