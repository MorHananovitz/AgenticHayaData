# Hayadata Conference Copilot (Claude skill)

An unofficial Claude skill for attendees of [hayaData 2026](https://haya-data.com/), the not-for-profit data community conference held on 20 October 2026 at the David InterContinental Hotel, Tel Aviv. It helps attendees find relevant talks, build a conflict-free personal agenda, and look up facts about sessions and speakers.

For the official program, tickets, and updates, always check the conference website: **https://haya-data.com/**

> This project is community-built and is not affiliated with or endorsed by the hayaData organizers.

## What it does

- Runs a short interview (one question at a time) and recommends 3 to 5 sessions ranked by fit.
- Builds a chronological agenda around the fixed breaks (10:35-11:00, 12:55-13:45, 15:15-15:30) and flags conflicts.
- Answers factual questions about sessions, speakers, tracks, companies, and times, using only the bundled data.
- Replies in the language the attendee uses.

All times are local conference time in Israel (Asia/Jerusalem).

## Example prompts

- "I'm a data engineer interested in streaming and AI agents. Which Hayadata talks should I see?"
- "I'll be at Hayadata from 13:45 to 16:00. Build me an agenda."
- "Who is speaking at the Track B session after lunch?"
- "Swap the 14:00 talk in my agenda for something on analytics."

## Repository layout

```
hayadata-conference-copilot-skill/
├── README.md
├── LICENSE
├── .gitignore
├── .gitattributes
└── hayadata-conference-copilot/        <- the skill folder
    ├── SKILL.md                        <- required: frontmatter + instructions
    ├── Hayadata_Sessions.csv           <- 50 sessions
    └── Hayadata_Speakers.csv           <- 57 speakers
```

The skill is the `hayadata-conference-copilot/` folder. `SKILL.md` must stay at its root, and the folder name must match the `name` field in the frontmatter.

## Install

**Claude.ai:** zip the `hayadata-conference-copilot/` folder (or download the `.skill` file from Releases), then upload it under Settings > Capabilities > Skills.

**Claude Code:** copy the folder into `~/.claude/skills/` (personal) or `.claude/skills/` in a project.

## Package a `.skill` file

A `.skill` file is a zip of the skill folder:

```bash
zip -r hayadata-conference-copilot.skill hayadata-conference-copilot -x "*.DS_Store"
```

## Keeping the data current

The schedule can change before the event. If the program on [haya-data.com](https://haya-data.com/) differs from the bundled CSVs, update the files and re-package. Keep these columns:

- Sessions: `session_id, title, description, speakers, domain, talk_format, duration_minutes, track, start_time, end_time_calculated, schedule_note`
- Speakers: `speaker_name, tagline, bio, speaker_title, company`

If counts, hours, or break times change, update `SKILL.md` to match (it mentions 50 sessions, 09:45 to 16:55, the fixed breaks, and the HD-019 lunch overlap).

## Notes

- The CSVs use a UTF-8 BOM and CRLF line endings. `.gitattributes` stops git from rewriting them.
- Session titles, descriptions, and speaker bios come from the hayaData program and belong to the conference and its speakers. The skill answers only from this data and does not invent sessions, speakers, or times.

## License

The skill instructions (`SKILL.md`) and this README are released under the [MIT License](LICENSE).

The MIT License does not cover `Hayadata_Sessions.csv` and `Hayadata_Speakers.csv`. Their content (session titles and descriptions, speaker names and bios) comes from the hayaData program and remains the property of the conference and its speakers.
