# Baroda Film Festival Shorts 2.0

A static website for Baroda Film Festival Shorts 2.0, built with [Hugo](https://gohugo.io/). This edition is two days of short films, 21–22 November 2026, at Alkapuri Hall in Vadodara. Films, dates, and prices in the sample program can be replaced.

The Hugo project lives in [`film-festival/`](film-festival/).

## Pages

| Page | What it shows |
| --- | --- |
| Home | Opening-day ticket, featured films, the two-day schedule, and pass prices |
| Films | Coming soon |
| Tickets | Coming soon |
| Venue | Alkapuri Hall: address, rooms, and arrival notes |
| About | Festival background, jury, and staff |

## Requirements

- [Hugo](https://gohugo.io/installation/) extended, **0.156** or newer (this site was built with 0.167)

## Run locally

```bash
cd film-festival
hugo server
```

Open http://localhost:1313/. The server rebuilds when you save a content or layout file.

## Build

```bash
cd film-festival
hugo --minify
```

Hugo writes the finished site to `film-festival/public/`. That directory is gitignored.

## GitHub Pages

The live site is [https://faguncb.github.io/baroda-film-festival/](https://faguncb.github.io/baroda-film-festival/).

Pushes to `cursor/afterglow-film-festival` run `.github/workflows/hugo-pages.yml`. That workflow builds the site and deploys it to GitHub Pages. `baseURL` in `film-festival/hugo.toml` matches that address. `hugo server` still serves a local preview and does not use the public address.

## Project layout

```text
film-festival/
  hugo.toml                 Festival name, dates, venue, email, navigation
  content/                  Pages and film write-ups
  content/films/            One Markdown file per film
  data/screenings.yaml      Day-by-day showtimes
  data/passes.yaml          Ticket names, prices, and what each pass includes
  layouts/                  Page templates
  assets/css/main.css       Styles
  assets/js/site.js         Mobile menu, film filters, and the ticket form
  static/                   Files copied as-is, such as the favicon
  archetypes/films.md       Front matter for a new film
```

## Edit the festival

**Name, dates, city, and contact.** Change `[params]` and `[params.venue]` in `film-festival/hugo.toml`. The box office email is `params.email`. Navigation labels and order are the `menus.main` entries in that same file.

**A film.** Each file in `content/films/` is one title. The filename is the screening id (`salt-on-the-lens.md` is referenced as `salt-on-the-lens`). Front matter used by the templates:

| Field | Role |
| --- | --- |
| `title`, `director`, `runtime`, `year`, `country`, `language` | Credits on the film page and posters |
| `genre` | Filter on the films list |
| `category` | Strand, such as Opening night or Closing night |
| `featured` | Include the film in the home-page row |
| `poster` | CSS gradient used as the poster background |
| `tagline`, `summary`, `weight` | Short description and sort order |
| body | Full synopsis |

Add a film with:

```bash
cd film-festival
hugo new content films/new-film.md
```

Then fill in the front matter and add at least one screening.

**The schedule.** `data/screenings.yaml` lists each day and its screenings. A screening’s `film` value must match a film filename without `.md`. Optional `note` is the line under the title, such as a reception or an encore.

**Passes.** `data/passes.yaml` lists each pass. `featured: true` highlights that card. Prices are whole dollars.

**Prose pages.** `content/about.md`, `content/venue.md`, `content/program.md`, and `content/tickets.md` hold the page introductions. About and venue use a sidebar; set `sidebar` to `facts` or `venue`.
