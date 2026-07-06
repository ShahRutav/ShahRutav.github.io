---
name: refine-technical-writing
description: Refine the technical parts of blog posts and notes into Lilian Weng's style (lilianweng.github.io). Use when writing or editing the technical passages of a post, such as explaining a method, model, equation, or paper, especially in posts/*.html. Layers on top of the general `writing` skill.
---

Use this when writing or editing the **technical** portions of a post: explaining a method, an architecture, an equation, a training objective, or the core idea of a paper. It applies Lilian Weng's technical-blog style (lilianweng.github.io). This sits on top of the general `writing` skill; keep those voice and formatting rules (no em dashes, no emojis, short and direct), and add the technical style below.

The framing and opinion parts of a post stay in the user's normal voice. This skill is for the parts that teach a concept.

## The Lilian Weng style

**Intuition before formalism.** Introduce a concept in plain words or with an analogy first, then formalize. Never open with an equation. The reader should know what a thing *is for* before they see its notation.

- Bad: "The policy models \(p(a, s', V(s') \mid s)\)."
- Good: "The model predicts three things at once: the action to take, what the world looks like after, and how good that future is. Written together: \(p(a, s', V(s') \mid s)\)."

**Motivate by problem then solution.** Frame each mechanism as an answer to a concrete difficulty. "A fixed-length context vector cannot remember long sentences. Attention was born to resolve this." Say what breaks, then what fixes it.

**Define notation the moment it appears.** Every symbol gets its meaning and, where it matters, its shape or range. Do not assume the reader carries notation across paragraphs. Bold vectors, name dimensions explicitly (e.g. "an action chunk \(K \times d_{act}\)").

**Equations live inside prose.** No orphaned formulas. Each equation is preceded by what it computes and followed by a plain-language reading of its parts. Inline math for small expressions; a display line only when the expression is the point of the paragraph.

**Prose for reasoning, bullets for enumerable parts.** Use connected prose for a chain of reasoning or a single idea. Use a short parallel list only for genuinely enumerable things: the components of an architecture, the steps of an algorithm, the roles one model plays. Do not bullet a single thought.

**Moderate paragraphs, one idea each.** Aim for 3 to 5 sentences. Break at each conceptual shift. Vary sentence length: a short declarative sentence to state the idea, longer ones to unpack it.

**Concrete examples and numbers.** Ground abstract claims in specifics. Cite the actual ablation number, the actual shape, the actual task. "Removing the future-state target collapses it from 67.1 to 44.4" beats "the auxiliary target helps a lot."

**Calibrated hedging only.** "Broadly speaking," "to some extent," "roughly" are fine when a claim is genuinely approximate. Do not hedge a fact. Mark real uncertainty explicitly, e.g. a `(TODO: verify ...)` note, rather than vague qualifiers.

**Honest about limits.** State what a method does not do or where it is unclear, plainly, in the same voice as the rest. This is a feature of the style, not an aside.

**No repetition.** Say each thing once. Do not restate a point in different words, echo a phrase from an earlier sentence, or add a closing clause that repeats what the sentence already established. If two sentences make the same claim, keep the clearer one and delete the other.

**No punchiness for its own sake.** Do not end a paragraph with a clever one-liner, a rephrase-for-effect, or a slogan that only restates what was just said. If a sentence exists to sound good rather than to add information, cut it. Say the thing once, plainly, and stop. Avoid "turns X into Y" flourishes, rule-of-three cadence, and dramatic short closers when they carry no new content.

**No contribution-listing. Evaluate objectively.** Do not frame the writing around the paper's claimed contributions. Avoid phrasings like "the paper's contribution is," "the key novelty is," "another contribution is," or press-release verbs like "leverage" and "unlock." We are not selling the paper. Describe what the method actually does and how it behaves, in concrete terms, and judge it on the evidence. Prefer "the model predicts X from Y" over "the paper proposes a novel X." When a claim rests on a result, cite the result; when it does not, say what it rests on.

## Workflow when refining a passage

1. Find the claim the passage is making. If you cannot state it in one sentence, the passage needs restructuring, not polishing.
2. Reorder so intuition comes before notation.
3. Check every symbol is defined at first use, with shape or range where it helps.
4. Make sure no equation stands without a plain reading around it.
5. Split any paragraph carrying more than one idea. Convert any run-on list of parts into bullets; convert any bulleted single thought back into prose.
6. Replace vague magnitude words with the actual number or shape when the source has it.
7. Run the general `writing` self-check: no em dashes, no emojis, nothing that reads twice, no unrequested images.

## In this repo

Technical passages live in `posts/*.html`. Wrap paper-specific technical discussion in `<div class="paper-note">...</div>`, which renders slightly smaller than the framing text. Inline LaTeX uses `\( ... \)` (MathJax is loaded in the post template). Keep opinions and framing outside the technical style; this skill is only for the teaching parts.

**Always render TODOs in red.** Any `TODO` note left in a post must be wrapped in `<span class="todo">...</span>`, which renders red (`.todo { color: #c0392b }`). Add that rule to the post's `<style>` block if it is not there yet. This applies to every TODO, in every post, without being asked.
