# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A free, Bengali-language Operating Systems course published as a static site at `os.najmulislam.dev` (GitHub Pages, see `CNAME`; repo `github.com/najmulislamnajim/os`). All content is prose, diagrams, and C examples written in Bengali (`<html lang="bn">`) — English is used only for technical terms (`syscall`, `page fault`, `inode`).

There is no build system, no package manager, no tests, no dependencies to install. Every page is a single hand-written, self-contained HTML file. To preview, open the file in a browser or serve the directory (`python -m http.server`). Deployment is `git push` to `main`.

## Page inventory

| File | Role |
|---|---|
| `index.html` | Landing page — hero, module cards, footer. The only page with a top bar instead of a sidebar. |
| `plan.html` | Roadmap / study plan. Sidebar layout, but its own section markup (`section.blk`, `.blk-head`, `.bn`/`.bs`). |
| `module1.html` … `module6.html` | The six course modules. Identical layout and CSS skeleton. |

Module order and identity (each module owns one accent color, used consistently on its own page **and** on its card in `index.html`):

1. Foundations — kernel/user, syscall, interrupt, boot — `#7a4a1e` — project: strace analysis
2. Process & Scheduling — fork/exec, context switch, threads, IPC — `#1a6b5a` — project: build a shell
3. Memory & Virtual Memory — paging, TLB, page fault — `#25608f` — project: build malloc
4. Concurrency — race, lock, semaphore, deadlock — `#6a3d7a` — project: producer-consumer
5. Storage & File System — inode, journaling, buffer cache — `#3d6b2f` — project: toy file system
6. Build Your Own OS — xv6, kernel hacking, MIT 6.1810 — `#b8501f` — project: xv6 hacking

## Anatomy of a module page

Every module file follows the same structure, and new content must match it:

- **Duplicated `<style>` block** in `<head>`. There is deliberately no shared stylesheet — each page carries its own copy. A visual change that should apply site-wide has to be repeated in every file. The shared parts are the `:root` palette (`--ink`, `--paper`, `--line`, `--muted`, `--code-bg`, plus the named hues) and the layout rules; `--accent` is what differs per module.
- **Layout**: `.wrap` flex → sticky `aside` (296px, brand + `.modtag` + `nav#toc` + `.toc-hint`) and `main` (max 880px). Below 900px the sidebar is hidden by media query.
- **`.hero`** with eyebrow / `h1` / lead paragraph.
- **`section.chapter` with `id="chN"`**, each opening with `.ch-head` containing `.ch-num` (Bengali numeral, e.g. `০৩`), an `h2` title, and a `.ch-sub` English slug. Chapter `id`s must match the `href`s in `nav#toc`, in order.
- **Closing `<script>`** — a ~5-line scrollspy that highlights the current `#toc a` with `.active`. It is byte-identical across `plan.html` and all six modules; copy it as-is.

Chapters run `০০ শুরুর কথা` (orientation) through a final `প্রজেক্ট` chapter, which closes with a centered `.box analogy` "module complete" summary that names the next module.

### Callout boxes

Content is carried almost entirely by `div.box` variants, each with a leading `<span class="tag">` that starts with an emoji. Use the right one — colors are semantic and readers rely on them (the `.toc-hint` in the sidebar tells them so):

- `.analogy` (amber) — 🚗 real-world analogy for a concept
- `.note` (teal) — 💡 clarification, definition, key takeaway
- `.deep` (blue) — 🔬 optional deeper technical detail
- `.warn` (rust) — ⚠️ pitfall, prerequisite, common misconception
- `.lab` (green) — 🛠 hands-on step the reader types and runs
- `.quiz` (dashed) — 🧠 self-check; wraps `<details><summary>question</summary><p>answer</p></details>`

`plan.html` uses a different set (`.why`, `.note`, `.res`, `.warn`, `.lab`) — don't mix the two taxonomies.

### Code and diagrams

- `<pre>` blocks are hand-highlighted with span classes: `.c` comment, `.k` keyword, `.s` string, `.f` function. No highlighter library runs — apply the spans yourself when writing code samples.
- Diagrams are **inline hand-authored SVG** inside `<figure><div class="diagram">…</div><figcaption>…</figcaption></figure>`. No raster images anywhere. Reuse the palette hex values in SVG fills/strokes so diagrams match the page. SVG text uses `font-family="Hind Siliguri, sans-serif"`.
- Fonts come from Google Fonts: Hind Siliguri (Bengali body) and JetBrains Mono (code, numerals, eyebrows).

## Conventions worth preserving

- The **favicon** is an inline `data:image/svg+xml` chip mark (same geometry as the topbar logo in `index.html`), duplicated verbatim in the `<head>` of all 8 pages — like the `<style>` block, a change must be repeated everywhere. It carries a `prefers-color-scheme` rule so the frame lightens on dark tab bars. If it ever renders as the browser's default globe, check the namespace first: it must be `xmlns='http://www.w3.org/2000/svg'`, and `#` in colors must be written `%23`.
- Section numbers, module numbers, and counts in prose are written in **Bengali numerals** (০১, ৯০০০). Code, filenames, and command output stay in ASCII.
- **Cross-page navigation** exists in three places on `plan.html` and every module, and all three must be updated together when the course structure changes:
  - `a.home` + `.modnav` in the sidebar — back-to-home link and the full course switcher, with `class="cur"` on the current page. `.modnav` sits *outside* `nav#toc` on purpose; the scrollspy would otherwise try to highlight it.
  - `.crumbs` at the top of `main` — `কোর্স হোম / রোডম্যাপ / <current>`.
  - `nav.pager` before `</main>` — prev/next through the linear order `plan → module1 … module6 → index`.

  The sidebar is hidden below 900px, so `.crumbs` and `.pager` are the only navigation on mobile — keep them working.
- Adding a module means touching: the new page, a card in `index.html`, a block in `plan.html`, and the `.modnav`/`.pager` links on all sibling pages.
- The pedagogy is "theory + hands-on": every concept is paired with something the reader builds in C, and every module ends in a working project. Keep new content in that shape rather than adding pure reference material.
- Commit style is short and imperative: `add module 6`, `update home`.
