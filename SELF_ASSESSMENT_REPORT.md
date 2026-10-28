# IA#2 — Dynamic HTML: Make the Catalogue Work

I assessed my work based on the current source code, Git history, `README.md`, `brief.md`, `AI-LOG.md`, and practical testing in Chrome headless.

## Self-assessment table

| Criterion | Maximum points | Self-assessed points | Main evidence |
| ------------------------------------------------- | ----------: | -----------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Behaviour — B1–B4 | 45 | 43 | Self-check `8/8`; all B1–B4 actions were run in Chrome and produced the correct results. I do not have a screenshot from before Part A for visual comparison. |
| Scope — only `index.html` and `app.js` differ from starter | 10 | 10 | `git diff d41c279..HEAD` shows that the source differs only in `index.html` and `app.js`; `style.css` and `check.js` are unchanged. The rubric excludes `brief.md` and `AI-LOG.md` from scope. |
| Brief — `brief.md` | 15 | 15 | Prompts 001–005 are recorded in the order Part A, B1, B2, B3, B4, with constraints, tools, and practical verification methods. |
| `AI-LOG.md` | 20 | 20 | It contains a summary table and logs for Part A, B1, B2, B3, and B4, including tools, requests, changes, rejected approaches, tests, and corresponding commits. The B2 detail and commit references were checked against the current repository. |
| Commit history | 10 | 10 | There is a starter commit and a separate commit for Part A, B1, B2, B3, and B4; each commit diff matches the change described in its message. |
| **Total** | **100** | **98** | **43 + 10 + 15 + 20 + 10 = 98** |

## Criterion-by-criterion explanation

### 1. Behaviour — 43/45

I give myself 43/45. The 40–45 rubric range applies when the Done means rows are achieved; my B1–B4 functionality has complete test evidence:

- `selfCheck()` returned `8/8`; all eight semantic checks passed.
- B1: one click listener is on `#catalogue`; adding T-shirt twice gives count `2`; Sold out Tote does not increase the count.
- Keyboard B1: focusing Hoodie’s Add button and pressing Enter increases the count from `0` to `1`.
- Load more followed by Add Belt: the catalogue has 12 cards and the cart updates correctly.
- B2: `scarf` and `SCARF` each return one card and `Showing 1 of 12 products`; clearing the search restores all cards and clears the status.
- B2: `<img src=x onerror=alert(1)>` is displayed verbatim in the status, with no image and no alert.
- B3: entering `cap` and pressing Enter leaves the URL without `?q=cap`, preserves the cart count, and updates the status.
- B4: T-shirt ×3 gives `Cart (3) · 540.000 đ`; adding Cap gives `Cart (4) · 635.000 đ`; Load more followed by Belt gives `Cart (5) · 775.000 đ`.
- After reload, the collected Console events contained no `error` events or exceptions.

I do not give myself 45/45 because the repository has no screenshot from before Part A, so I cannot verify the Done means row requiring a visual comparison before and after Part A. This is missing evidence, not an error observed in the code.

### 2. Scope — 10/10

I give myself the full 10/10. The starter is `d41c279`. `git diff --name-status d41c279..HEAD` for the source shows:

- `index.html` was changed for Part A.
- `app.js` was changed for B1–B4.
- `style.css` is unchanged.
- `check.js` is unchanged.

`brief.md` and `AI-LOG.md` were created to record prompts and the log, so they are not counted as changes to starter files under the rubric’s Scope definition.

### 3. Brief — 15/15

I give myself the full 15/15. `brief.md` contains five prompts in chronological order: Part A, B1, B2, B3, and B4. It records key requirements such as preserving IDs/classes, not editing `style.css` and `check.js`, event delegation, `textContent`, preventing form reload, and the cases to test. The prompts also record tools and verification methods instead of only giving general descriptions.

### 4. AI-LOG.md — 20/20

I give myself the full 20/20. `AI-LOG.md` contains a summary table and detailed entries for Part A, B1, B2, B3, and B4. Each entry records the tool, actual request, source files changed, specific changes, rejected approaches, test evidence, and actual errors where applicable. The table records the correct commits `405f46e`, `7295faf`, `b183a40`, `472766d`, and `aff9770`; the B2 detail no longer repeats the prompt. The log matches the source code, `brief.md`, and the current Git history.

### 5. Commit history — 10/10

I give myself the full 10/10. The current history is:

1. `d41c279` — `init starter`
2. `405f46e` — `Complete Part A semantic HTML`
3. `7295faf` — `Implement B1 add to cart`
4. `b183a40` — `Implement B2 product filtering`
5. `472766d` — `Prevent form reload in B3`
6. `aff9770` — `Implement B4 cart total`

I reviewed the diff of each commit: Part A changes `index.html`; B1 changes the listener and cart count; B2 changes filtering; B3 changes submission; and B4 changes the total. Therefore, the history meets the rubric’s 9–10 range.

## Tests run

- `selfCheck()` in Chrome headless: `8/8 passed`.
- B1: T-shirt ×2, Sold out Tote, Load more, and Belt.
- Keyboard B1: focused Add and pressed Enter; the count increased.
- B2: `scarf`, `SCARF`, an empty string, and the malicious HTML string.
- B3: entered `cap`, pressed Enter, and checked the URL and cart count.
- B4: T-shirt ×3, multiple product types, Belt after Load more, and an empty cart.
- Console after reload: no `error`-type Console errors or exceptions were recorded.
- `git diff --check`: no whitespace errors found.
- `git diff d41c279..HEAD --stat`, `git show --stat`, and each commit diff to check scope/history.

## What I did not manage

- I do not have a screenshot from before Part A in the repository, so I could not verify the before/after visual comparison.

## Total self-assessment score

**98/100**
