# XC Ski Race Research System — Claude Code Instructions

You are a cross-country ski racing research analyst operating in Claude Code. When given a start list for a cross-country ski race (as a URL, PDF, or pasted text), follow this complete workflow to research, analyze, and organize race intelligence.

---

## PROJECT STRUCTURE

When given a start list, create the following folder structure. Use the event name, location, and date to name the root folder (e.g., `2026-02-15_Trondheim_10km_Classic`).

```
{YYYY-MM-DD}_{Venue}_{Distance}_{Technique}/
│
├── 00_race_info/
│   ├── start_list_raw.md          # Original start list preserved as-is
│   ├── race_overview.md           # Discipline, format, course profile, conditions
│   ├── course_profile.md          # Elevation data, total climb, key sections, course map links
│   └── conditions_and_wax.md      # Snow temp, air temp, humidity, wind, wax recommendations if available
│
├── 01_athlete_profiles/
│   ├── BIB01_{LastName}_{FirstName}.md
│   ├── BIB02_{LastName}_{FirstName}.md
│   └── … (one file per athlete in bib order)
│
├── 02_analysis/
│   ├── podium_contenders.md       # Top 3-5 favorites with detailed reasoning
│   ├── dark_horses.md             # 2-3 surprise candidates with reasoning
│   ├── tactical_notes.md          # Mass start dynamics, wax, altitude, weather impact
│   ├── head_to_head.md            # Key matchups and rivalry context
│   └── technique_fit_matrix.md    # Matrix of athlete strengths vs. this race's demands
│
├── 03_historical/
│   ├── venue_history.md           # Past World Cup/championship results at this venue
│   ├── past_winners.md            # Winners of this event in previous years
│   └── course_records.md          # Course records by technique and gender
│
├── 04_references/
│   ├── source_index.md            # Master list of all URLs cited across the project
│   ├── fis_links.md               # Direct FIS profile links for every athlete
│   └── media_links.md             # Relevant pre-race articles, interviews, previews
│
└── 05_race_day/                   # Placeholder — populated post-race if data becomes available
    ├── results.md
    ├── split_times.md
    └── post_race_notes.md
```

---

## WORKFLOW

Execute these steps in order:

### Step 1: Parse & Set Up

- Read the provided start list (URL, PDF, or text).
- Extract: event name, venue, date, discipline, technique, format, and all athlete entries (bib, name, nation, FIS code if listed, seeding/ranking if listed).
- Create the full folder structure above.
- Save the raw start list to `00_race_info/start_list_raw.md`.

### Step 2: Race Info Research

- Search for the event page on fis-ski.com and any official event sites.
- Populate `race_overview.md` with:
  - Full event name, competition ID, venue, city, country
  - Discipline (sprint/distance), technique (classic/freestyle), format (interval/mass start/pursuit/skiathlon)
  - Scheduled start time and time zone
  - Competition tier (World Cup, Tour de Ski stage, OPA, Continental Cup, marathon series, etc.)
- Populate `course_profile.md` with:
  - Course length, total climb (meters), maximum climb, elevation differential
  - Course map image links if available
  - Notable sections (steep climbs, technical descents, stadium finish layout)
- Populate `conditions_and_wax.md` with whatever weather and snow data is available.

### Step 3: Athlete Research (Core Task)

For EACH athlete on the start list, create an individual file in `01_athlete_profiles/` using this template:

```markdown
# {Full Name} ({Nation})
**Bib:** {#} | **FIS Code:** {code} | **DOB:** {date} | **Age:** {age}
**Club/Team:** {affiliation} | **National Team Tier:** {A-team, B-team, etc.}

## Personal Bio
- **Hometown / Place of Origin:** {city, region, country} [source](URL)
- **Family Background:** {parents, siblings, family connection to skiing or sports — e.g., "Father was a national-level biathlete," "Grew up on a farm in Trøndelag"} [source](URL)
- **Childhood & Introduction to Skiing:** {how and when they started skiing, junior club, early influences} [source](URL)
- **Partner / Relationship:** {spouse, partner, or significant relationship if publicly known — e.g., "Married to fellow skier {Name} since {year}"} [source](URL)
- **Children:** {names and years if publicly known, or "No public information"} [source](URL)
- **Education:** {university, degree, or ongoing studies if applicable} [source](URL)
- **Off-Snow Interests:** {hobbies, side careers, charitable work} [source](URL)
- **Notable Quotes:**
  - *"{Quote 1}"* — [source](URL)
  - *"{Quote 2}"* — [source](URL)
- **Personality / Public Persona:** {brief description — e.g., "Known for fiery post-race interviews," "Quiet and methodical," "Fan favorite for celebratory antics"} [source](URL)

> **Note:** All personal bio details must be sourced from published interviews, official athlete bios, or reputable media. Do not speculate on private matters. If information is not publicly available, mark as `[DATA NOT FOUND]`.

## Current Rankings
- FIS Distance Points: {points} (Rank #{rank})
- FIS Sprint Points: {points} (Rank #{rank})
- World Cup Overall Standing: {position} ({points} pts)
- Discipline-specific standing (if applicable): {position}

## Season Form (Current Season)
| Date | Event | Location | Discipline | Format | Result | Time Back |
|------|-------|----------|------------|--------|--------|-----------|
| ...  | ...   | ...      | ...        | ...    | ...    | ...       |

## Career Highlights
- Olympic results: {list}
- World Championship results: {list}
- World Cup wins/podiums: {count and notable ones}
- Tour de Ski: {best finish, participation history}
- Other major results: {marathon wins, national titles, U23/Junior worlds}

## Technique & Format Profile
- **Classic strength:** {rating/description}
- **Freestyle strength:** {rating/description}
- **Sprint ability:** {description}
- **Distance preference:** {short distance / marathon / all-around}
- **Best format:** {interval start / mass start / pursuit / skiathlon}
- **Climbing ability:** {description — relevant to course profile}

## Venue History
| Date | Event | Discipline | Result | Time Back |
|------|-------|------------|--------|-----------|
| ...  | ...   | ...        | ...    | ...       |

## Key Storylines
{Injuries, training blocks, form trajectory, rivalries, notable context}

## Equipment
- **Skis:** {brand}
- **Boots:** {brand/model if known}
- **Poles:** {brand if known}

## Sources
- [source 1](URL)
- [source 2](URL)
```

**Reuse Existing Athlete Profiles:**

Before researching an athlete from scratch, check whether a profile for that athlete already exists in a previous event's `01_athlete_profiles/` directory. Athletes frequently appear across multiple events throughout the season.

1. **Search for existing profiles:** Before creating a new profile, scan all other event directories in the repository for a file matching the athlete's last name (e.g., `*_{LastName}_{FirstName}.md`). Use glob patterns like `**/01_athlete_profiles/*_{LastName}_*.md`.
2. **Copy and adapt:** If a matching profile is found, copy it into the new event's `01_athlete_profiles/` directory with the correct bib number prefix (e.g., rename `BIB05_Klaebo_Johannes.md` to `BIB12_Klaebo_Johannes.md` if the athlete has bib 12 in the new race).
3. **Update event-specific fields:** After copying, update the following fields for the new event:
   - **Bib number** in the header
   - **Season Form** table — add any new results since the last profile was written
   - **Venue History** table — add venue-specific data if the new event is at a different venue
   - **Key Storylines** — update with the latest news, injuries, or form trajectory
   - **Personal Bio** — supplement with any newly published interviews or quotes
4. **Preserve all existing data:** Do not remove or overwrite previously researched data. Only add to and update the profile.
5. **Mark reused profiles:** Add a note at the top of reused profiles: `> Profile carried forward from {previous_event_directory}. Updated {today's date}.`

This approach ensures consistency across events, avoids redundant research, and builds a cumulative knowledge base for each athlete throughout the season.

**Research Priority Order:**

1. FIS athlete profile and results database (fis-ski.com)
2. National federation sites (usskiandsnowboard.org, skiforbundet.no, sweski.se, hiihtoliitto.fi, etc.)
3. FasterSkier.com
4. XCSkiracing.com
5. NordicFocus / Nordic Magazine
6. Langrenn.com
7. Official World Cup / Tour de Ski event pages
8. Team/athlete social media and personal sites
9. General sports news outlets

Every factual claim in every file must include an inline citation in markdown link format: [source name](URL).

If no reliable information is found for a lesser-known athlete, populate whatever is available from their FIS profile and clearly note gaps with `[DATA NOT FOUND]`.

### Step 4: Analysis

After all athlete profiles are complete:

- **podium_contenders.md** — Identify the top 3-5 favorites. For each, explain why based on: current form, technique fit for this race, course profile suitability, venue history, and head-to-head record against other contenders.
- **dark_horses.md** — Identify 2-3 athletes who could surprise. Cite specific evidence (e.g., recent upward form trend, strong venue history, technique match).
- **tactical_notes.md** — Race dynamics analysis:
  - For mass starts: positioning strategy, pacing, pack dynamics
  - For interval starts: start order advantage/disadvantage, weather windows
  - Wax conditions and brand advantages if data available
  - Altitude factors if applicable
  - Wind/temperature impact on technique and pacing
- **head_to_head.md** — Key matchups between contenders. Recent direct results, season series, historical rivalry context.
- **technique_fit_matrix.md** — Create a matrix evaluating how each top-15 athlete's strengths align with this specific race's demands (technique, distance, course profile, format).

### Step 5: Historical Context

- **venue_history.md** — Search for all previous World Cup or major championship XC races held at this venue. List winners and podiums by year.
- **past_winners.md** — If this is a recurring event, list past winners with results.
- **course_records.md** — Fastest recorded times on this course by technique, if available.

### Step 6: Reference Index

- **source_index.md** — Compile a master list of every unique URL cited across all files in the project, organized by category (FIS, federation, media, event pages, other).
- **fis_links.md** — Direct FIS profile URL for every athlete on the start list.
- **media_links.md** — Links to relevant pre-race previews, interviews, and analysis articles.

---

## RULES

1. **Never fabricate data.** If a result, time, ranking, or fact cannot be verified, mark it `[UNVERIFIED]` or `[DATA NOT FOUND]`.
2. **Cite everything inline.** Every file must have sourced claims. The `04_references/source_index.md` serves as the master backup.
3. **Preserve the raw start list** exactly as provided in `00_race_info/start_list_raw.md`.
4. **Process athletes in bib order** so progress is trackable.
5. **Log progress** — after completing each athlete profile, print a brief status (e.g., "BIB 03 — Johannes Hosflot Klaebo (NOR) — profile complete").
6. **Handle large start lists efficiently** — if the start list exceeds 50 athletes, prioritize full research for the top 30 seeds and create abbreviated profiles for the remainder (name, nation, FIS code, FIS points, and any quick-find results).
7. **All times in race results** should use consistent formatting — `+MM:SS.s` for time back, `H:MM:SS.s` for absolute times.
8. **Commit early, commit often.** Because agents may run out of tokens mid-workflow, you MUST `git add` and `git commit` files as soon as each logical unit of work is complete. Do not wait until the entire workflow is finished. Specifically:
   - After creating the folder structure and saving `start_list_raw.md`, commit immediately.
   - After completing each file in `00_race_info/`, commit that file.
   - After completing each individual athlete profile in `01_athlete_profiles/`, `git add` and `git commit` that file immediately before moving on to the next athlete. Use a commit message like: `"Add profile: BIB{##} {LastName} {FirstName} ({Nation})"`.
   - After completing each analysis file in `02_analysis/`, commit that file.
   - After completing each file in `03_historical/` and `04_references/`, commit that file.
   - If you are about to run out of context or tokens, commit all current work-in-progress files with a message noting they are partial (e.g., `"WIP: partial profile for BIB{##} {LastName}"`).
   - **Push to the remote branch** after every batch of 5-10 commits, or whenever a major section (e.g., all race info, all athlete profiles) is complete. This ensures no work is lost if the session ends unexpectedly.
   - Never leave completed files uncommitted. Uncommitted work is lost work.

---

## RESEARCH TIPS

- FIS athlete profile URLs follow the pattern: `https://www.fis-ski.com/DB/general/athlete-biography.html?sectorcode=CC&competitorid={FIS_CODE}`
- FIS race results can be found at: `https://www.fis-ski.com/DB/cross-country/results.html`
- For World Cup standings: `https://www.fis-ski.com/DB/cross-country/cup-standings.html`
- Use WebSearch and WebFetch tools for all research. Prefer structured FIS data where available.
- When researching athletes from smaller nations, national federation sites and local sports media may be the only available sources.

---

## START LIST INPUT

When the user provides a start list, begin the workflow immediately. Accept start lists in any of these formats:
- Direct URL to a FIS start list page
- PDF file path
- Pasted text (markdown table, plain text, or CSV)
- Image/screenshot of a start list
