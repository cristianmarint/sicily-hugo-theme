# Sicily

A minimal editorial Hugo theme in black and white. Landing page, blog, pricing, FAQ and contact — no JavaScript framework, no build step beyond Hugo itself.

[**Live demo**](https://sicily-hugo-theme.netlify.app/)

![Sicily screenshot](https://raw.githubusercontent.com/cristianmarint/sicily-hugo-theme/master/images/screenshot.png)

## Requirements

Hugo **extended** v0.128.0 or newer — the theme compiles SCSS with `css.Sass`, which the standard build does not include.

```
hugo version   # must contain "+extended"
```

## Run the demo site

```
git clone https://github.com/cristianmarint/sicily-hugo-theme.git
cd sicily-hugo-theme/exampleSite
hugo server --themesDir ../..
```

Open http://localhost:1313.

## Use it in your own site

```
cd your-site
git submodule add https://github.com/cristianmarint/sicily-hugo-theme.git themes/sicily
```

Then set `theme = "sicily"` in your config and copy `exampleSite/config.toml`, `exampleSite/content/` and `exampleSite/data/` as your starting point.

## Configuration

Everything lives in `config.toml`. The parameters the theme actually reads:

| Key | What it does |
| --- | --- |
| `title` | Site name — also rendered as the black brand block in the header and footer |
| `summaryLength` | Words shown in blog post summaries |
| `[pagination] pagerSize` | Posts per page on the blog list |
| `[services.disqus] shortname` | Enables comments on posts; remove the block to disable |
| `params.logo` | Favicon path, relative to `static/` |
| `params.author`, `params.description` | Default meta tags |
| `params.contact_form_action` | POST target of the contact form (Netlify Forms, Formspree, etc.) |
| `params.navigation_button` | `enable`, `label` and `link` for the header call-to-action |
| `params.preloader` | `enable` and image path for the loading screen |
| `params.company` | Address block in the footer |
| `[[params.footer]]` | Repeatable — one contact card per person (`rol_name`, `rol_representative`, `rol_email`) |
| `[[params.social]]` | Repeatable — social links on the homepage (`title`, `link`, `icon`) |
| `[[params.plugins.css]]`, `[[params.plugins.js]]` | Vendored assets loaded on every page |

Menus are standard Hugo menus. Three are used: `main` (header), `company` and `product` (footer columns).

## Content

Each top-level section maps to a layout:

| Path | Renders as |
| --- | --- |
| `content/blog/` | Post list with pagination, plus single post pages |
| `content/pricing/_index.md` | Three-column pricing table, driven by the `intro`, `enterprise` and `base` front matter keys |
| `content/faq/_index.md` | Two-column FAQ grid, built with the `faq` shortcode |
| `content/contact/_index.md` | Contact form |
| Any other `_index.md` | Plain page — title, optional `subtitle`, and the markdown body |

Blog posts accept `image`, `description` and `type`. Setting `type: "featured"` promotes a post to the wide layout at the top of the list; anything else renders as a regular card.

FAQ entries use a shortcode:

```
{{< faq "Question goes here?" >}}
Answer in **markdown**.
{{</ faq >}}
```

The homepage banner and the 404 illustration come from `data/homepage.yml` (`banner`, `description` and `error404` keys).

## Customizing the design

The theme is built on a small set of SCSS variables in `assets/scss/_variables.scss`:

```scss
$primary-color: #000000;   // accent: links, hovers, active states
$text-color:    #000000;
$body-color:    #FFFFFF;
$light:         #F4F4F4;   // pagination and muted backgrounds
$primary-font:  'Lato', sans-serif;
```

Changing `$primary-color` re-colors the whole theme — buttons, links, pagination, blockquotes and list bullets all derive from it. Partials are split by concern under `assets/scss/`: `_typography.scss`, `_buttons.scss`, `_common.scss` and `templates/`.

Overriding from your own site works the usual Hugo way: drop a file with the same path in your project root and it wins over the theme's.

## Deploy

`netlify.toml` is ready to use — it builds `exampleSite` and publishes `exampleSite/public`. For your own site, point the build at your project root instead:

```toml
[build]
  publish = "public"
  command = "hugo --gc --minify"

[build.environment]
  HUGO_VERSION = "0.164.0"
```

Netlify needs the extended binary; the version above includes it.

## Issues and questions

Search [existing issues](https://github.com/cristianmarint/sicily-hugo-theme/issues) first, then [open a new one](https://github.com/cristianmarint/sicily-hugo-theme/issues/new). Pull requests welcome.

## License

[MIT](https://github.com/cristianmarint/sicily-hugo-theme/blob/master/LICENSE) — free for personal and commercial use.

Built by [cristianmarint](https://www.flexyflow.co/), originally derived from [Bigspring](https://github.com/themefisher/bigspring-hugo-startup-theme) by Themefisher.

If the theme saved you time, you can [buy me a coffee](https://www.paypal.me/cristianmarint/10USD).
