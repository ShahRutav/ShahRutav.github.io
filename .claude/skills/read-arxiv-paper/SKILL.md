---
name: read-arxiv-paper
description: Use this skill when asked to read an arxiv paper given an arxiv URL
---

You will be given a URL of an arxiv paper, for example:

https://www.arxiv.org/abs/2601.07372

### Part 1: Normalize the URL

The goal is to fetch the TeX Source of the paper (not the PDF!), the URL always looks like this:

https://www.arxiv.org/src/2601.07372

Notice the /src/ in the url. Once you have the URL:

### Part 2: Download the paper source

Download the paper source yourself (e.g. with `curl` or `wget`) to a local .tar.gz file inside the repo's `papers/arxiv/` directory: `papers/arxiv/{arxiv_id}.tar.gz`. Create the `papers/arxiv/` directory if it does not exist. Note that `papers/arxiv/` is gitignored, so downloaded sources stay local and are never committed.

(If the file already exists, there is no need to re-download it).

### Part 3: Unpack the file in that folder

Unpack the contents into the `papers/arxiv/{arxiv_id}` directory.

### Part 4: Locate the entrypoint

Every latex source usually has an entrypoint, such as `main.tex` or something like that.

### Part 5: Read the paper

Once you've found the entrypoint, Read the contents and then recurse through all other relevant source files to read the paper.

### Part 6: Report

Once you've read the paper, produce a summary of the paper into an HTML file at `papers/ai_summary_{tag}.html`. Generate some reasonable `tag` like e.g. `conditional_memory` or whatever seems appropriate given the paper. Probably make sure that the tag doesn't exist yet so you're not overwriting files.

The HTML file should be a standalone page that renders nicely in the browser and matches the site style. Follow the existing `posts/` pages: link `../stylesheet.css`, use the same narrow centered table layout, and include a link back to `../index.html` and `../blog.html`. Note that the summary lives in `papers/`, so use `../` for site-root paths.

Write a clear, faithful summary of the paper itself: what it does, the core idea, method, key results, and any practical tricks worth remembering. Do NOT add a section on why the paper is relevant to the user's own work. Keep it about the paper.

Follow the local `writing` skill for style (no em dashes, no emojis, short and clear, bullets for lists).

### Part 7: Add a blog note

The summary is AI generated and lives alongside the user's own writing. The user keeps a blog where each paper gets a note post.

- Create a blog post under `posts/` for this paper (for example `posts/wams-cosmos-policy.html`, following the existing post template).
- The post title and slug are given by the user (e.g. "WAMs: Cosmos Policy note"). If not given, ask or pick a sensible title.
- The post body is left for the user's own writing. Add a clear link inside the post to the AI generated summary HTML file (`papers/ai_summary_{tag}.html`).
- Add the new post to the list in `blog.html` (newest first).
