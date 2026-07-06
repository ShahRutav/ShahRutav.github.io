---
name: add-citation
description: Add a verified citation to a blog post as a numbered footnote, matching the existing footnote pattern. Use when the user points at a specific term, method, or claim in posts/*.html and asks for a citation. Only cite where the user tells you to; never add citations on your own initiative.
---

Add a citation for a specific spot the user points to, as a numbered footnote. Do not scan the post for things to cite. Cite only where the user says.

## Citation format

Footnote text is:

> First Author et al., "Title", venue, year.

- **First Author et al.**: first author's family name, then "et al." if there is more than one author. Two authors: "Smith and Jones". One author: just the name.
- **Title**: the paper's exact title, in quotes.
- **venue**: the conference or journal (e.g. NeurIPS 2023, ICRA 2024, TMLR). If it was never published anywhere but arXiv, use the arXiv id: "arXiv:2203.12601". Prefer the real venue when one exists; still link to the arXiv abstract page.
- **year**: publication year of that venue. For arXiv-only, the arXiv year.

The title links to the arXiv abstract page: `https://arxiv.org/abs/<id>`.

## Verification (do this thoroughly, before writing anything)

Getting a citation wrong is worse than not having one. Verify every field against at least two independent sources. Do not rely on memory for any field.

1. Find the paper. Search the web for the exact term or method name the user pointed at (e.g. "LAPA latent action pretraining", "Decision Transformer"). Confirm you have the right paper, not a similarly named one.
2. Cross-check these fields across sources:
   - **arXiv id and title**: from the arXiv abstract page itself (`arxiv.org/abs/...`).
   - **Author order**: confirm the first author from arXiv and one more source (Semantic Scholar, DBLP, Google Scholar, or the paper PDF). Author lists on blogs are often wrong.
   - **Venue and year**: many papers are on arXiv first and published later at a conference. Check DBLP or the venue proceedings, or the "Comments" field on the arXiv page, to find where it was actually published. Do not assume arXiv-only.
3. If sources disagree on any field, keep digging until you can resolve it. If you genuinely cannot confirm the venue, use the arXiv id as the venue and say so to the user.
4. Prefer these sources, in order: the arXiv abstract page, DBLP, Semantic Scholar, the publisher/proceedings page, the authors' project page. Treat random blog posts as weak evidence.

Use ReadInternalWebsites only for amazon-internal URLs; use WebFetch/WebSearch for public sources like arXiv, DBLP, and Semantic Scholar.

After writing, tell the user which sources you used to confirm the venue and author order, so they can spot-check.

## Inserting the footnote in the post

The posts use a numbered footnote pattern. Match it exactly.

At the citation site, wrap the term with a ref:

```html
LAPA<a class="fn-ref" id="fnrefN" href="#fnN"><sup>N</sup></a>
```

In the `.footnotes` block at the bottom of the post, add:

```html
<p id="fnN">
  <a href="#fnrefN">N.</a> First Author et al.,
  "<a href="https://arxiv.org/abs/XXXX.XXXXX">Title</a>", venue, year.
</p>
```

- `N` is the next footnote number in that post. Renumber only if the user asks; otherwise append.
- Keep footnotes ordered by number in the `.footnotes` block.
- If a `.footnotes` block does not exist yet in the post, create one just before the `<!-- ===== END YOUR WRITING ===== -->` comment, using the same markup as other posts.

## Scope

- One citation per user request unless they list several.
- Do not reword the surrounding prose. Only attach the ref and add the footnote.
- Do not cite the paper the post is already about (it has its own AI-summary link and heading).
