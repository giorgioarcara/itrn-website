# Proposed improvements to the ITRN website

The migration keeps the content and URL structure of the old Google Sites website, with a few low-risk upgrades already applied:

- overview pages for Community, Initiatives and Resources, which were empty;
- a News section with RSS feed, which now holds the elections call and the Turin save-the-date that were on the home page;
- tables and tabs for seminars, fees and nodes;
- site search, dark mode, mobile layout and a 404 page;
- small typo fixes, e.g. "Alessandrto", "Istituto Istituto", "Honarable", "Opena Access".

The proposals below need a decision from the Steering Committee and are **not** applied yet. They are ordered by expected benefit relative to effort.

## 1. Content that is out of date or inconsistent (quick fixes)

| Page | Issue | Suggestion |
|---|---|---|
| Join ITRN | "These are the fees for 2024" | Update the year, or say "current fees". |
| ITRN nodes | "Up to August 2023" | Refresh the list and add a "last updated" date. |
| Steering Committee | "Newly elected… 2025–2026 term", with Davide Crepaldi as President-elect | After the February 2027 elections, update the page and move the outgoing committee to a "Past committees" section. |
| Annual meeting | The page still describes Verona 2026 as current | Turn it into the Turin 2027 page as soon as the programme is ready. |
| Online seminars | The last edition is 2024/25, and the 2024/25 playlist link is missing | Add the playlist, and a 2025/26 edition or a note that the series is paused. |
| ReproCoffee | Last session May 2024; the "Next" section is empty; links to Twitter/X | Confirm whether the series is active, and update the social link. |
| Reproducibility Awards | The 2024 call is closed; the 2024 winners and the 2026 awards are not listed; the 2023 description is truncated | Publish winners by year (see §4). |
| Expert List | The page says "explore the list", but no list is shown | Publish the list from the questionnaire export, or reword the page. |
| Awards notification date | It read "14/01/2024", for a call closing 31/12/2024 | Already corrected to 14/01/2025 in the migrated page; please confirm. |

## 2. Move documents off Google Drive

Governance documents, newsletters, flyers and some slides are Google Drive links. These links break when ownership changes, cannot be indexed, and are not citable. Two options:

- Upload them to the **ITRN Zenodo community**, which gives one DOI per version (the Statute and abstract books are already on Zenodo).
- Or commit the PDFs to this repository, e.g. `resources/docs/`, and link them directly.

## 3. A single "Events" hub

Online seminars, onsite seminars, ReproCoffee and the annual meeting are four separate pages with different formats. Proposal:

- Create an `events/` folder with **one small page per event**, with date, speakers, abstract, video and slides, and categories such as `seminar`, `reprocoffee` or `meeting`.
- Generate an "Upcoming" and a "Past" Quarto listing, plus a "Next event" box on the home page.
- Keep the current URLs as overview pages (or as redirects with `aliases:`).

This makes it easier to add events, makes each seminar searchable and shareable, and gives one consistent look.

## 4. One page per annual meeting and per award year

Replace the very long *Past annual meetings* page with `meetings/2026-verona.qmd`, `meetings/2025-milano.qmd` and so on. Each page would have the programme, the book of abstracts DOI, photos, slides and the award winners of that year. A listing then becomes the archive. Do the same for the awards: one page for the current call and an archive of winners by year.

## 5. Data-driven lists

Store repeated, structured information in YAML or CSV files in `data/`, and render it with Quarto listings or a small template. This covers nodes, steering members, seminars, newsletters, governance documents and experts. People who don't write code then only edit a data file, and the format stays consistent.

## 6. Richer Community pages

- **Steering Committee:** add each member's role, affiliation, a 2–3 line bio, and ORCID or website links.
- **Nodes:** add an interactive **map of the nodes** (Leaflet, no server needed), and a link for each institution.
- Add a **Working Groups** page (Educational, Data Sharing, Teaching, AI and Experiments, TIDieR extension, Biomedical data sharing). They are mentioned in the meeting programmes but have no page.
- **Partners/Network:** add links to UKRN, the other national Reproducibility Networks, AIP, AISC and the institutional members.

## 7. Bilingual content

Several pages mix Italian and English. The 2024–2025 meetings and the bank details are in Italian; the rest is in English. Options:

- Pick English as the main language and add Italian summaries where needed.
- Or create a full Italian version (`/it/…`) using Quarto profiles, for the pages most relevant to Italian institutions: Join, Statute and Meetings.

## 8. Membership workflow

Joining currently means an email, then approval, then a bank transfer, then another email. Consider:

- an online application form (e.g. Google Form or Tally) linked from the Join page;
- a clear **FAQ** (who can join, fees per year, receipts and invoices, institutional membership benefits).

## 9. Visibility and privacy

- The site no longer uses Google cookies, so no cookie banner is needed. If visit statistics are wanted, use a cookie-less tool such as **GoatCounter** or **Plausible**.
- Open Graph and Twitter cards are enabled. Add a 1200×630 social sharing image (`image:` in `_quarto.yml`).
- Add the Instagram and YouTube channel links to the navbar and footer.
- Add `alt` text to every new image. Existing images already have it.

## 10. Governance of the website itself

- Add the repository URL to `_quarto.yml` to show "Edit this page" and "Report an issue" links, so members can propose corrections through GitHub.
- Protect `main` and use pull requests for changes made by working groups.
- The GitHub Action can also run a link checker periodically to catch broken external links.
