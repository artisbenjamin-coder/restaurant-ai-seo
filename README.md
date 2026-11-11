# Restaurant AI SEO — a working example

Structured data, `llms.txt` and a single source of truth, as actually deployed on a
Paris brasserie's website: **[lechoupinet.com](https://lechoupinet.com)** — Le Choupinet,
58 boulevard Saint-Michel, Paris 6e, facing the Luxembourg Gardens.

Most "AI SEO" advice is abstract. This repository is the opposite: the real files from a
real restaurant site, so you can see what the markup looks like once it is complete rather
than minimal.

## Why this exists

Assistants like ChatGPT, Claude, Gemini and Perplexity increasingly answer "where should I
eat near the Luxembourg Gardens?" directly, without sending anyone to a website. What they
say about a restaurant depends on what they can read about it — and on whether the sources
agree with each other.

Our experience: **the enemy is not missing data, it is contradictory data.** The site said
one thing in French and another in English about the same lunch menu. The WhatsApp assistant
knew a fact the website had never published. Every inconsistency is an opportunity for a
model to get it wrong, or to skip the place entirely because it cannot be confident.

So the work was done in this order:

1. **Build a single source of truth** — every fact about the restaurant, with its source, its
   date, and a status: public, internal, or unverified. Including an explicit
   "never write this" list.
2. **Audit what the site already exposed**, instead of assuming it exposed nothing.
3. **Fill the gaps only**, with facts that trace back to the source of truth.

## What is here

| File | What it is |
|---|---|
| [`llms-full.txt`](llms-full.txt) | The long-form file for AI crawlers: address, hours, service, menus, accessibility, groups. Stable facts only; volatile ones point to the live pages. |
| [`schema/restaurant-amenityfeature.json`](schema/restaurant-amenityfeature.json) | `amenityFeature` block merged into the existing `Restaurant` type — accessibility, families, pets, payment, terrace, takeaway. |
| [`schema/menu-sections.json`](schema/menu-sections.json) | `MenuSection` entries added to the existing `Menu` on the menu page — lunch set menu, children's menu, drinks. |
| [`schema/faqpage-homepage.json`](schema/faqpage-homepage.json) | `FAQPage` markup for eight questions that were already **displayed** on the homepage but not marked up. |

## Four things worth stealing

**Mark up what you already show.** The homepage had eight questions and answers on screen in
plain HTML. No markup. That is free structured data left on the table — and the text must
match word for word, otherwise you are describing a page that does not exist.

**State the negatives.** We declare that the restaurant does takeaway and that it does
**not** deliver. An absent fact is an invented fact: say what you do not do, and a model has
no reason to guess.

**No self-declared ratings.** We deliberately omit `aggregateRating`. Google ignores
self-reported review scores for local businesses, and a rating you award yourself is a
credibility cost, not a gain.

**Audit before you write.** The site already had `Restaurant` on three pages, a full `Menu`,
an 18-question `FAQPage` and a valid `llms.txt`. Rewriting all of it would have broken
working markup. We only added what was genuinely missing.

## Honest limits

This is one restaurant, not a benchmark. We have no controlled measurement of what the
markup changed — the site went live in its current form in November 2026, and the only
honest answer in a month will come from the Search Console and Business Profile figures.

`llms.txt` is a proposed convention, not a standard. Crawlers may ignore it. It costs
almost nothing to publish, which is the whole argument for it.

These files describe one specific restaurant. Copy the structure, not the facts.

## Licence

Code and structure: MIT. The facts about Le Choupinet — hours, prices, menus — describe a
real business and should not be reused as if they were yours.

---

🇫🇷 **En français** — Ce dépôt rassemble les données structurées et le fichier `llms.txt`
réellement déployés sur [lechoupinet.com](https://lechoupinet.com), brasserie parisienne
face au jardin du Luxembourg. L'idée directrice : construire d'abord un socle de faits
unique et daté, puis n'ajouter au site que ce qui manque vraiment — parce que ce qui
désoriente les IA, ce n'est pas l'information absente, c'est l'information contradictoire.
