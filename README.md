# EX1 — Scatterplot with D3

Build an interactive scatterplot of Netflix movies using D3 v7.

---

## Dataset

`data/netflix_votes1000.txt` — 1,606 Netflix movies with at least 1,000 TMDB votes.

The base data comes from the **Netflix Prize dataset**, one of the most studied datasets in recommendation systems research. It has been enriched with metadata (genres, cast, director, posters, ratings) via a crawl of the [TMDB](https://www.themoviedb.org/) API. The movies are older, but the dataset is interesting enough for meaningful visual exploration.

All columns in the dataset:

| Column | Type | Description |
|---|---|---|
| `movie_id` | number | Netflix internal ID |
| `year` | number | Release year |
| `title` | string | Netflix title |
| `tmdb_id`, `tmdb_title` | number / string | Matched TMDB entry |
| `original_language` | string | ISO 639-1 code, e.g. `en`, `fr` |
| `overview` | string | Plot summary |
| `tagline` | string | Marketing tagline |
| `genres` | string | Comma-separated list, e.g. `"Drama, Comedy"` |
| `cast` | string | Top-billed cast members |
| `director` | string | Director name(s) |
| `keywords` | string | TMDB keyword tags |
| `runtime_min` | number | Runtime in minutes |
| `tmdb_vote_average` | number | Mean user rating (0–10) |
| `tmdb_vote_count` | number | Number of ratings |
| `popularity` | number | TMDB popularity score |
| `tmdb_release_date` | string | TMDB release date (YYYY-MM-DD) |
| `poster_path` | string | Full URL to the movie poster image |

> **Note:** `primary_genre` is not a data column — it is derived in `netflix.js` by taking the first value from `genres`. It is available on every data object inside `update()`.

---

## Collaboration and resource policy

Discussing the assignment with the instructor or peers, reading D3/web documentation, and looking at past tutorials or online examples are all encouraged.

AI programming assistants (e.g. GitHub Copilot, ChatGPT, Claude) should **not** be used for this assignment. The goal is to build a genuine understanding of data visualization principles and the D3 library — that understanding only develops through working through the problems yourself.

---

## What you need to implement

All your work goes in `js/netflix.js`. Search for `// TODO` — there are four sections:

1. **Declare scales** at the top of the file (`xScale`, `yScale`, `sizeScale`, `colorScale`)
2. **Create / update scales** inside `update()` — set domains from the data and ranges to fit the chart
3. **Update axes and axis labels** — call the D3 axis helpers on the existing axis groups
4. **Draw circles** — bind `data` to `circle` elements; map x, y, radius, and fill through your scales; attach the provided `showMovie` click handler
5. **Draw a color legend** — use `colorScale.domain()` to label each color category

The sidebar (`showMovie`) and all HTML structure are already provided.

### Recommended scale types

```js
xScale     = d3.scaleLinear()  // continuous → pixel position
yScale     = d3.scaleLinear()
sizeScale  = d3.scaleSqrt()    // area perception
colorScale = d3.scaleOrdinal(d3.schemeTableau10)
```

> **Note on genres:** There are 19 unique genres but `schemeTableau10` only has 10 colors. Consider mapping only the top genres and grouping the rest as `"Other".`

---

## Running locally

Browsers block file-based data loading (`d3.csv(...)`) for security reasons. You need a local server.

**Option A — VS Code (easiest)**
Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension, then click **Go Live** in the status bar. Your browser will open automatically.

**Option B — Node.js**
```bash
npx serve .
```
Then open `http://localhost:3000` (or whichever port is shown).

**Option C — Python**
```bash
python3 -m http.server 8000
```
Then open `http://localhost:8000`.

---

## Suggested order of implementation

Work through the encodings one at a time — verify each before moving on.

1. **Position** — get circles on screen at the right x/y coordinates with a fixed radius and color
2. **Size** — replace the fixed radius with `sizeScale`
3. **Color** — replace the fixed fill with `colorScale`; add the legend
4. **Interaction** — attach the click handler to show the sidebar; add hover styles

This order makes bugs easier to isolate. A blank chart usually means a scale domain or range is wrong — check the browser console for errors.

---

## File overview

```
EX1/
├── index.html          # Layout, dropdowns, sidebar — Shouldn't need to modify
├── js/
│   └── netflix.js      # Your implementation goes here
├── data/
│   ├── netflix_votes1000.txt   # Dataset used by the assignment
│   ├── netflix_clean.txt       # All rows with complete fields (You can find on Moodle)
│   └── filter_netflix.py       # Script used to generate filtered datasets

```
