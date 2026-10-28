# AI-LOG.md

## AI Usage Summary

| No. | Date | Part | Tool | Request / Task | Changes made | Rejected / Not used | Verification | Commit |
| --: | ---------- | ----------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| 001 | 2026-10-28 | Part A / testing | Codex (GPT-5), PowerShell, Chrome headless | Completed Part A — Semantic HTML; reached self-check 8/8; updated brief and AI-LOG; did not start B1 | Updated semantic structure in `index.html`: landmarks, headings, form, list/card, label, button, and disabled Add. Created `brief.md` and `AI-LOG.md` as required | Did not edit `app.js`, `style.css`, or `check.js`; did not implement B1–B4; did not commit/push | Chrome headless loaded `index.html`; `check.js` Console reported `Session 4 self-check: 8/8 passed`; all 8 checks passed. `git diff --check` reported no errors | `405f46e` — Complete Part A semantic HTML |
| 002 | 2026-10-28 | B1 / testing | Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol | Completed B1 — Add to Cart using event delegation on `#catalogue` | Updated `app.js`: added one click listener on `#catalogue`, checked `.add`, found `.card`, blocked disabled/Sold out, and updated `cart` and `cart-count` with `textContent` | Did not edit `index.html`, `style.css`, or `check.js`; did not attach listeners to individual buttons; did not implement B2–B4 | First inline run failed due to PowerShell quoting before the test executed. Rerun succeeded: T-shirt twice → `2`; Tote Sold out → still `2`; Load more created 12 cards; Belt → `3`. `git diff --check` reported no errors | `7295faf` — Implement B1 add to cart |
| 003 | 2026-10-28 | B2 / testing | Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol | Completed B2 — Filter as you type | Updated `app.js`: added input filtering, trim/lowercase handling, card visibility, status via `textContent`, and the `input` listener | Did not edit `index.html`, `style.css`, or `check.js`; did not use `innerHTML`; did not change B1 or implement B3/B4 | Chrome DevTools Protocol: `scarf` and `SCARF` both returned 1/8; empty input restored 8 cards and blank status; after Load more there were 12 cards; HTML string returned no result, preserved the status, 0 images, 0 alerts | `b183a40` — Implement B2 product filtering |
| 004 | 2026-10-28 | B3 / testing | Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol | Completed B3 — Prevent form reload | Updated `app.js`: obtained the form through `searchInput.form`, prevented `submit` with `event.preventDefault()`, and called `applyFilter()` | Did not edit `index.html`, `style.css`, or `check.js`; did not change B1, B2, or B4 | Chrome DevTools Protocol: added T-shirt twice, entered `cap`, pressed Enter; URL had no `?q=cap`, cart remained `2`, status was `Showing 1 of 8 products` | `472766d` — Prevent form reload in B3 |

| 005 | 2026-10-28 | B4 / testing | Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol | Completed B4 in `renderCart()`; calculated item count and total price | Updated `app.js`: summed `Object.values(cart)`, found cards by ID, converted `dataset.price` with `Number()`, multiplied quantity by price, and wrote `cart-count`/`cart-total` with `textContent` | Did not edit `index.html`, `style.css`, or `check.js`; did not change B1–B3 | T-shirt ×3 → `Cart (3) · 540.000 đ`; added Cap → `Cart (4) · 635.000 đ`; Load more + Belt → `Cart (5) · 775.000 đ`; empty cart → count `0`, total ` · 0 đ` | `aff9770` — Implement B4 cart total |

## Detailed Log

### Interaction 001 — Part A — Semantic HTML

Date: 2026-10-28

Part: Part A

Tool: Codex (GPT-5)

Request: Complete Part A — Semantic HTML according to the full actual prompt stored in `brief.md`; edit only `index.html` for Part A, update the two documents, run the self-check to reach 8/8, and stop before B1.

Files changed: `index.html`

Changes made:

- Changed the top bar to `header`, the menu to `nav`, the content to `main`, and the footer to `footer`.
- Changed the Catalogue title to the only `h1`; product names became `h2` headings.
- Changed `#catalogue` to `ul`; all current cards and the card in `#card-template` became `li` elements.
- Changed the search area to a `form` and added `label for="q"` linked to input `#q`.
- Changed Search, Add, and Load more into real `button` elements.
- Added the `disabled` attribute to the Sold out Tote bag Add button.
- Preserved IDs, classes, selectors, and product data; did not change `app.js`.

Rejected / not used: Did not edit `style.css`, `check.js`, or `app.js`; did not use `div` elements as buttons; did not implement B1–B4; did not commit or push, in accordance with the request scope.

Verification: Ran `git diff --check` — no whitespace errors. Ran Chrome headless with `index.html`; the Console reported `Session 4 self-check: 8/8 passed`. Results: 1 PASS landmarks; 2 PASS exactly one h1; 3 PASS heading levels; 4 PASS product names are headings; 5 PASS catalogue list and cards; 6 PASS connected label; 7 PASS search inside form; 8 PASS real buttons and no onclick.

Errors found: No errors found in Part A.

### Interaction 002 — B1 — Add to Cart

Date: 2026-10-28

Part: B1 / testing

Tool: Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol

Request: Read README.md and app.js, complete only B1 — Add to Cart with one click listener on `#catalogue`, event delegation, `closest('.card')`, updating `cart-count`, ignoring disabled/Sold out, and not editing files outside the scope; then test T-shirt, Tote bag, Load more, and Belt.

Files changed: `app.js`

Changes made: Added exactly one `catalogue.addEventListener('click', ...)`; found `.add` and `.card` with `closest`; ignored buttons with the `disabled` class, the `disabled` attribute, or `Sold out` status; updated `cart[id]` and used `cartCount.textContent` in `renderCart()`. B4 was not implemented, so `cart-total` was still not handled.

Rejected / not used: Did not edit `index.html`, `style.css`, or `check.js`; did not attach listeners to individual buttons; did not implement B2, B3, or B4.

Verification: The first attempt did not run because of PowerShell command quoting before the test executed. The rerun with Chrome DevTools Protocol completed these actions: clicked T-shirt twice, dispatched a test click on Sold out Tote, clicked Load more, and clicked Belt. Results: `before: "2"`, `afterTote: "2"`, `afterBelt: "3"`, `cards: 12`, `belt: true`. Ran `git diff --check`; no whitespace errors were found.

Errors found: A quoting error occurred in the first test run and was fixed with an encoded CDP script; no B1 error was found in the successful test.

### Interaction 003 — B2 — Filter as you type

Date: 2026-10-28

Part: B2 / testing

Tool: Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol

Request: Complete only B2 — Filter as you type; filter `#q` on the `input` event, ignore case, use `card.hidden`, display the status in the required format with `textContent`, prevent user HTML from executing, and edit only `app.js`.

Files changed: `app.js`

Changes made: `applyFilter()` reads the original value and the `trim().toLowerCase()` value, iterates over cards in `#catalogue`, updates `hidden`, counts results among all current cards, uses `statusBox.textContent`, and registers `searchInput.addEventListener('input', applyFilter)`.

Rejected / not used: Did not edit `index.html`, `style.css`, or `check.js`; did not use `innerHTML`; did not change B1 or implement B3/B4.

Verification: Chrome DevTools Protocol entered `scarf` → `Scarf`, status `Showing 1 of 8 products`; entered `SCARF` → the same result; cleared the input → 8 cards returned and status became blank; Load more → 12 cards; entered `<img src=x onerror=alert(1)>` → no card, status `No products match "<img src=x onerror=alert(1)>"`, `images: 0`, `alerts: 0`.

Errors found: No B2 errors were found in the successful test. The final string did not run JavaScript because it was assigned to the status through `textContent` and was not parsed as HTML.

### Interaction 004 — B3 — Prevent form reload

Date: 2026-10-28

Part: B3 / testing

Tool: Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol

Request: Complete only B3 using `searchInput.form`, prevent submission with `event.preventDefault()`, call `applyFilter()`, preserve the cart state, and test entering `cap` followed by Enter.

Files changed: `app.js`

Changes made: Registered a `submit` listener on `searchInput.form`; called `event.preventDefault()` to stop the default submission and called `applyFilter()` to update the results.

Rejected / not used: Did not edit `index.html`, `style.css`, or `check.js`; did not change B1, B2, or B4.

Verification: Chrome DevTools Protocol added T-shirt twice, entered `cap`, and dispatched the Enter key. Results: the URL had no `?q=cap`; the cart was `2`; the status was `Showing 1 of 8 products`; the form existed.

Errors found: No B3 errors were found in the successful test. Enter submits the form by default because the input is inside a form and the browser submits it when Enter is pressed; `preventDefault()` cancels the default reload and URL change.

### Interaction 005 — B4 — Cart total

Date: 2026-10-28

Part: B4 / testing

Tool: Codex (GPT-5), PowerShell, Chrome headless, Chrome DevTools Protocol

Request: Complete B4 in `renderCart()`, calculate the item count with `Object.values(cart)`, calculate money as `quantity × Number(data-price)`, update both elements with `textContent`, use `vi-VN` formatting, and test T-shirt ×3, multiple product types, Load more, and an empty cart.

Files changed: `app.js`

Changes made: `renderCart()` calculates `itemCount`; iterates over entries in `cart`, finds the corresponding card in `#catalogue`, converts `dataset.price` to a number with `Number()`, adds to `total`, and writes `cartCount.textContent` and `cartTotal.textContent`.

Rejected / not used: Did not edit `index.html`, `style.css`, or `check.js`; did not change B1–B3 logic.

Verification: Chrome DevTools Protocol returned T-shirt ×3: `{count: "3", total: " · 540.000 đ"}`; after adding Cap: `{count: "4", total: " · 635.000 đ"}`; after Load more and adding Belt: `{count: "5", total: " · 775.000 đ", cards: 12}`; calling `renderCart()` with an empty cart returned `{count: "0", total: " · 0 đ"}`.

Errors found: No B4 errors were found in the successful test. When the quantity is zero, the sum of the values in `cart` is 0 and the total is displayed as ` · 0 đ`.
