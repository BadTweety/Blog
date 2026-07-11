# Field Notes — a zero-install markdown blog

One HTML file. Markdown posts. No build step, no dependencies to install.

```
blog/
├── index.html        ← the entire blog engine (edit SITE title/tagline at the top of the <script>)
├── posts/
│   ├── posts.json    ← list of posts (the only thing you edit besides the .md file)
│   ├── hello-world.md
│   └── shell-tricks.md
└── images/
    └── sample.svg
```

## About page

Edit `about.md` (next to `index.html`) — plain markdown, same as posts. It's linked in the header automatically.

## Changing the logo / site name

Open `index.html` and edit two spots:

1. **Header logo** — near the top of `<body>`, find:
   ```html
   <a class="site" href="#/">Field<b>Notes</b></a>
   ```
   Change the text (the part inside `<b>` gets the accent color), or replace it with an image — there's a ready-made commented example right above that line:
   ```html
   <a class="site" href="#/"><img src="images/logo.svg" alt="My Blog" style="height:1.5rem; display:block"></a>
   ```
   Just drop your `logo.svg`/`logo.png` into `images/`.
2. **Homepage title & tagline + browser tab** — in the `<script>`, edit the `SITE` object (`title`, `tagline`), and update the `<title>` tag in `<head>`.

Bonus: to change the accent color (the teal), edit `--accent` in the `:root` and `html[data-theme="dark"]` blocks at the top of the CSS.

## Adding a post

1. Write `posts/my-new-post.md` in plain markdown.
2. Add an entry to `posts/posts.json`:

```json
{
  "slug": "my-new-post",
  "title": "My new post",
  "date": "2026-07-11",
  "summary": "One line shown on the homepage and in search.",
  "tags": ["life"]
}
```

The `slug` must match the filename (without `.md`). Newest date sorts first automatically.

## Grouping posts into a series (optional)

Add a `"series"` field to any post's entry in `posts.json`:

```json
{
  "slug": "licensing-03-distribution",
  "title": "What counts as distribution?",
  "date": "2026-07-12",
  "summary": "...",
  "tags": ["licensing"],
  "series": "Licensing"
}
```

Only posts with a `series` field are grouped — everything else stays a normal standalone post. Posts with the **same series name** are grouped together, and you can have as many different series as you like. You get automatically:

- A **Series** section on the homepage with a card per series (name + post count)
- A **series page** (`#/series/licensing`) listing its posts in reading order (oldest first = part 1)
- A **"Part N of M"** box at the top of each post in the series, with previous/next links
- Series names are searchable too

No separate config — the part numbers come from the post dates, so to reorder a series, adjust the dates.


## Images

Put files in `images/` and reference them: `![alt text](images/photo.jpg)`

## Features

- **Search** — press `/` anywhere, or click Search. Searches titles, tags, summaries, and full post text.
- **Code blocks** — syntax highlighting + a copy button, ~190 languages via highlight.js.
- **Dark mode** — ◐ button, remembers your choice, follows system preference by default.
- Tables, blockquotes, task lists — anything GitHub-flavored markdown supports.

## Hosting on Azure Static Web Apps (no installs)

Everything happens in the browser — no git, no CLI, no npm.

**One-time setup:**

1. **Put the files on GitHub**: create a new repository at github.com, click *Add file → Upload files*, and drag this folder's contents in (`index.html`, `posts/`, `images/`). Commit.
2. **Azure Portal** → *Create a resource* → **Static Web App**:
   - Plan: **Free**
   - Deployment source: **GitHub** → sign in and pick your repo + `main` branch
   - Build presets: **Custom**
   - App location: `/`
   - Api location: *(leave empty)*
   - Output location: *(leave empty — there is no build)*
3. Click *Create*. Azure adds a GitHub Actions workflow to your repo and deploys automatically. In a minute or two your blog is live at `https://<something>.azurestaticapps.net`.

**Publishing a post from then on:** open your repo on github.com, use *Add file → Create new file* to write `posts/my-post.md` in the browser, edit `posts/posts.json` to add its entry, commit. Azure redeploys automatically within a couple of minutes. You never touch a terminal.

No `staticwebapp.config.json` is needed — the blog uses hash routing (`#/post/...`), so every URL is served by `index.html` natively.

**Previewing locally before publishing** is optional; if you ever want it, any static file server works (e.g. `python3 -m http.server` in the folder). Opening `index.html` by double-click won't work because browsers block `fetch()` on local files.

## What it deliberately doesn't have

No RSS, no comments, no analytics, no themes to configure. Add them later if you ever need them — it's just one HTML file to edit.
