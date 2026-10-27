# Making lesson decks with Claude: a brief

*For science teachers at Diocesan, and for the AI working with them. Maintained by Victor Canela. This is a living document: it gets better every time someone adds what they learned (section 9).*

**Teachers:** start a conversation with Claude and say:

> Read the full text of this brief (not a summary) and follow it: https://raw.githubusercontent.com/diocesanschoolforgirls/unit-decks-brief/main/README.md. Then I'll share my unit materials.

If Claude says it can't open the link, download this page and attach the file instead. To read the brief yourself: https://interactives.diocesan.school.nz/unit-decks-brief/

**Claude:** everything below is written to you. Read all of it before you reply. If your tool for opening links gives you only a summary, fetch the raw text another way (for example with `curl`): you need every section.

---

## 1. What these decks are for

You are helping a teacher build a set of slide decks for one unit, usually one deck per lesson. The decks have three jobs:

1. **Support the teacher in class.** Most teachers here teach from the whiteboard. A deck gives them striking images to display while they talk, plus definitions and activities to refer to. It is not a script.
2. **Let students who miss a lesson catch up** on their own, at home, often on a phone.
3. **Remind the teacher** what each lesson covers and in what order.

The reference example is the Year 9 unit *Are we related?*:

- Live: https://interactives.diocesan.school.nz/are-we-related/
- Source: https://github.com/diocesanschoolforgirls/are-we-related

Look at it before you start. Match its look and slide engine (section 5). Everything else, including how lessons are structured, is open to the teacher's judgement.

## 2. How to work with the teacher

This is a conversation, not a production line. The back-and-forth is what keeps the decks good and stops them becoming formulaic.

**Step 1: gather.** Ask for whatever the teacher has. Typical materials:

- the unit plan
- content notes, or the teacher's own summary of what students should know
- the lab manual or workbook (note its page numbers)
- the assessment and mark scheme, even last year's (tell the teacher it is only used to check the decks never copy it; it never goes into them)
- how many lessons are available before the assessment
- what has worked well in past years

**Step 2: read everything, then give your thoughts before building anything.** Include:

- how well the content, activities and assessment line up, such as content that is taught but never assessed, or assessed but thin in the notes
- factual errors or out-of-date claims in the materials (say what is wrong and what is right; don't silently copy them)
- whether the activities fit the lessons available
- a proposed lesson sequence: one line per lesson
- any questions you need answered

Then **stop and wait for the teacher's approval.** Don't build until they agree the sequence.

**Step 3: build one lesson at a time.** After each deck, give a short summary of what's on each slide and anything the teacher should check, then wait. Teachers often reply with numbered points: respond to each one specifically. Expect the plan to change as you go; that's normal.

**Step 4: publish** (section 7), when the teacher is ready.

## 3. Firm rules

These hold whatever else changes.

1. **Never reuse the assessment's content in the decks.** The decks are public. Don't use the test's scenarios, organisms, data sets or wording in practice questions, examples or exit questions. Practise the same *skill* in a different context, with made-up data labelled "Example data". Core facts students must learn (from the unit's learning outcomes) are fine. If you notice an overlap, flag it rather than quietly keeping it. If there is no assessment yet, ask what students will be assessed on, and do this check once it exists.
2. **Only use images you are allowed to use.** Creative Commons (CC BY, CC BY-SA, CC0) or public domain only. Credit every image on the slide where it appears: author, licence, and a link to its source page. Keep a `credits.json` list as well.
3. **Be accurate.** If the teacher's notes contain an error, point it out and use the correct version. Round numbers sensibly and say when figures are estimates.
4. **Every deck ends with an exit question and a "Missed this lesson?" slide.** The catch-up slide tells an absent student exactly what to read, do and write, using lab manual pages where they exist.
5. **Write for the reader.** Pitch the language at the year level. Use NZ English and correct te reo Māori with macrons. Prefer Aotearoa examples where they fit. For te ao Māori content, keep it brief and respectful, and suggest the teacher checks the framing.

## 4. What a typical deck looks like

A shape, not a template. Change it whenever the lesson calls for something else.

1. **Title slide** with a full-screen photo.
2. **Starter:** a question, image or puzzle that gets students thinking.
3. **Key ideas** with definitions, revealed step by step so the teacher can ask first and reveal second.
4. **The activity or practical:** method, safety and the lab manual pages.
5. **Check or practise:** questions with answers revealed one at a time, a worked example, or data to interpret.
6. **Exit question.**
7. **Missed this lesson? Catch up here.**

About 10 to 13 slides. Hero photos are what students remember: choose them carefully and look at every one before using it.

## 5. The look and the engine

Copy these two files from the reference repo into the unit's `assets/` folder, unchanged:

- `assets/deck.css`
- `assets/deck.js`

Raw links: https://raw.githubusercontent.com/diocesanschoolforgirls/are-we-related/main/assets/deck.css and `.../assets/deck.js`.

If a unit genuinely needs a new slide style, add it to `deck.css` and tell the teacher, so it can be shared back to the reference.

**File layout for a unit:**

```
unit-folder/
  index.html        unit page linking every lesson
  L01.html ...      one file per lesson
  assets/deck.css   shared engine (copied)
  assets/deck.js
  img/              photos, plus credits.json
```

**Skeleton of a lesson file:**

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>L1 Short title | Unit name</title>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@500&family=IBM+Plex+Sans:wght@400;600;700&display=swap">
<link rel="stylesheet" href="assets/deck.css">
</head>
<body>
<main class="deck">
  <section class="slide photo"> ... </section>
  <section class="slide"> ... </section>
</main>
<script src="assets/deck.js"></script>
</body>
</html>
```

**Slide building blocks** (see the reference decks for real examples):

| Class | Use |
|---|---|
| `slide photo` | Full-screen photo with `<img class="bg">`, an `.overlay` for the text and a `.credit`. Add `bright` for snowy or pale photos so the text stays readable. |
| `slide` | Ordinary content slide. Start with `<p class="kicker">` and an `<h2>`. |
| `def` | A highlighted definition or key statement. |
| `cols`, `cols wide-left` | Two columns. |
| `cards three` / `four` / `five`, with `card` or `tile` | Grids of cards; `tile` holds a photo and caption. Add `compact` for shorter photos. |
| `figure.sketch` | A portrait image or diagram shown whole, beside text. |
| `table.taxa` | A clean table; `tr.shared` shades a row. |
| `svg.chart` | Hand-drawn bar charts, histograms and pie charts. Use class `col` for bars (not `bar`, which the engine already uses). |
| `quote`, `big-number`, `small` | Model answers, a striking figure, small print. |
| `step` | On any element: hidden until the next click. |

**How the decks behave:** arrow keys, a clicker or a mouse click step forward. **R** switches between presenting and reading mode; phones open in reading mode automatically. **F** is full screen.

## 6. Practical tips

- **Images.** commons.wikimedia.org is blocked on the school network, but en.wikipedia.org is not. Use the Wikipedia API (`https://en.wikipedia.org/w/api.php`, `action=query&prop=imageinfo&iiprop=url|extmetadata&iiurlwidth=1600`) to get each Commons file's licence, author and a thumbnail on upload.wikimedia.org. Send a descriptive User-Agent and pause between requests, or you'll be rate-limited.
- **Image size.** Resize to at most 1600 px on the long side, and **never enlarge** a small image; it gets blurry and the file gets bigger. Keep a whole unit's images to around 10 to 15 MB.
- **Check every slide before showing the teacher.** Open the deck at 1280×720, reveal every step, and make sure nothing runs past the bottom of the slide (slides are 1600×900 inside). Check that every image loads. Look at the photo slides yourself: busy or bright backgrounds swallow text.
- **Charts.** Draw them as inline SVG so they stay sharp on a projector. Label invented data clearly.
- **Video links.** If you can't confirm a clip's exact URL, link to a YouTube search for its title and say so.
- **Diagrams.** A simple diagram you draw yourself is often clearer than a detailed one you find. Avoid images students might find confronting when a diagram would do.

## 7. Publishing (optional)

Decks can be published to the school's GitHub organisation, **diocesanschoolforgirls**. They appear at `https://interactives.diocesan.school.nz/<repo-name>/` and can be embedded in Schoolbox.

This needs the **Claude desktop app (Code tab)**, because Claude has to run commands on the teacher's computer. Teachers using Claude on the website can build and review decks there, then ask a colleague who has publishing set up.

**One-time setup for the teacher** (Claude: walk them through it, step by step, in plain language):

1. A GitHub account, and an invitation to the diocesanschoolforgirls organisation from one of its owners.
2. The GitHub command-line tool (`gh`), installed and signed in with `gh auth login` in the browser.

**Claude, when the teacher says "publish":** do every step yourself and explain what is happening in plain words, without git jargon.

1. Make the unit folder a git repository with a `.gitignore` containing `.DS_Store`, and commit.
2. Create a **public** repo in the organisation with a short kebab-case name such as `y10-chemical-reactions`, and push it.
3. Turn on GitHub Pages from the `main` branch: `gh api -X POST repos/diocesanschoolforgirls/<repo>/pages -f 'source[branch]=main' -f 'source[path]=/'`.
4. Wait until the build finishes, then open the live site and check that it works.
5. Give the teacher the link and a Schoolbox embed code:

```html
<iframe src="https://interactives.diocesan.school.nz/<repo-name>/" width="100%" height="700" style="border:0"></iframe>
```

**Updating later:** when the teacher says "update my decks", commit the changes and push. The site rebuilds in about a minute. If a browser still shows the old version, a hard refresh (Cmd+Shift+R) fixes it.

## 8. What we've learned

Add to this list. Date each entry and keep it short.

- *Oct 2026, Are we related? (Y9).* The richest inputs (content notes, lab manual, last year's test) produced the best decks. Thin notes produce generic decks.
- *Oct 2026.* Checking the decks against the test caught several practice questions that copied the test's own scenarios. Do that check before building each lesson, not at the end.
- *Oct 2026.* A whole lesson of documentary (Planet Earth III, episode 2) before any content was a powerful hook for a biology unit.
- *Oct 2026.* Building one lesson at a time, with the teacher's feedback in between, caught things a full batch would have missed: an unreadable photo slide, a wrong photo, a misleading diagram.

## 9. Improving this brief

The brief gets better when the people using it add to it: a tip, a new slide style, a rule that should change, or an entry for "What we've learned".

**Teachers**, three ways, easiest first:

1. **In the Claude desktop app (Code tab):** tell Claude what you learned and say *"suggest this as an addition to the decks brief"*. Claude does the rest and gives you a link.
2. **On GitHub:** open `README.md` in https://github.com/diocesanschoolforgirls/unit-decks-brief, click the pencil icon, make your change, then click **Propose changes**. You only need a free GitHub account.
3. **Or just tell Victor.**

**Claude, when a teacher asks to suggest a change:**

- Keep the brief's style: short, plain, written to Claude. Date entries in "What we've learned" with the month, year, unit and year level.
- Propose it as a pull request, so the maintainer can review it: `gh repo fork diocesanschoolforgirls/unit-decks-brief --clone`, edit `README.md` on a new branch, commit, then `gh pr create` with a short description of what changed and why. Don't push straight to `main` unless the teacher is the maintainer.
- Give the teacher the pull request link, and explain in plain words that Victor will review it.

**Maintainer:** review pull requests on GitHub and merge the good ones. Both links above update within a minute.
