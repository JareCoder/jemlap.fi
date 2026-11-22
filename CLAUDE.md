# jemlap.fi

Personal portfolio and blog site of Jesse Lappalainen, live at https://jemlap.fi. It is built on the
[Astro Theme Pure](https://github.com/cworld1/astro-theme-pure) template, so much of the structure
and some leftover naming come from the theme rather than from this site.

## Tech stack

- **Astro 7** with TypeScript (strict), `.astro` components, Markdown/MDX content
- **astro-pure 1.4.9** theme, installed from npm, provides layout pieces, UI components
  (`astro-pure/user`, `astro-pure/advanced`, `astro-pure/components/pages`) and the `astro-pure` CLI.
  It still pins Astro 6, so `overrides` in `package.json` run it on Astro 7. Remove the `astro`,
  `@astrojs/mdx` and `katex` overrides once a theme release supports Astro 7
- **UnoCSS** for styling, added by the theme integration (Tailwind-style utility classes, typography
  preset in `uno.config.ts`)
- **Vercel** adapter with `output: 'server'`; pages are server-rendered unless they export
  `prerender = true` (blog, archives and tag pages do)
- **Pagefind** search, **Waline** comments and pageviews (external server), KaTeX math, Shiki code
  highlighting
- ESLint + Prettier (no semicolons, single quotes, 100 columns, no trailing commas)

## Commands

Uses **npm** (`package-lock.json`) on **Node 24**. Run `npm install` to set up.

- `npm run dev` starts the dev server
- `npm run build` runs `astro-pure check`, `astro check`, then `astro build`
- `npm run check` type checks, `npm run lint` runs ESLint with `--fix`, `npm run format` runs Prettier
- `npm run new -- "Post title"` scaffolds a blog post in `src/content/blog/`

There are no tests. `npm run build` is the verification step.

## Git workflow

- All new additions go through a feature branch and a pull request. Never commit or push directly
  to `main`.
- Always get Jesse's confirmation for a PR before merging it.

## Where content goes

| Content | Location |
| --- | --- |
| Site title, author, description, header menu, footer, integrations (Waline, Pagefind, links logbook) | `src/site.config.ts` |
| Blog posts | `src/content/blog/<slug>/index.md` (or `.mdx`), with the post's images in the same folder |
| Blog frontmatter schema | `src/content.config.ts` |
| Home page: intro, experience, education, skills | `src/pages/index.astro` (hardcoded in the page) |
| Projects list | `src/pages/projects/index.astro` (arrays passed to `ProjectSection`) |
| About page: bio, hobbies, tools, social links, website history timeline | `src/pages/about/index.astro` |
| Links page data: recommended courses, friends, other links | `public/links.json` |
| Links page layout | `src/pages/links/index.astro` |
| Legal pages | `src/pages/terms/*.md` |
| Avatar and imported images | `src/assets/` |
| Tool icons for the About page | `src/assets/tools/*.svg` |
| Project card images | `src/assets/projects/` (referenced by filename via the `image` prop) |
| Favicons and static files served as-is | `public/` |
| Site font (Satoshi, fetched at build time) | `fonts` in `astro.config.mjs` |

Notes on specific content types:

- **Blog posts** require `title` (max 60 chars), `description` (max 160 chars) and `publishDate`.
  Optional: `updatedDate`, `heroImage` (`{ src, color }`), `tags`, `language`, `draft`, `comment`.
- **Links** in `public/links.json` are read by array index in `src/pages/links/index.astro`
  (`friends[0]` courses, `[1]` inactive courses, `[2]` friends, `[3]` broken friend links,
  `[4]` other links), so keep the group order stable. The course logbook timeline lives in
  `integ.links.logbook` in `src/site.config.ts`. Friend avatars are stored in
  `public/images/avatars/`, because LinkedIn image URLs expire. An entry can set an optional
  `ribbon` (such as `"Open to work"`) to show a green corner ribbon on its card.
- **Project links** take a `type` of `github`, `site`, `doc` or `release`, which selects the icon.
- **Website history**: notable site changes get an entry in the timeline at the bottom of
  `src/pages/about/index.astro`.
- Pages using `CommonPage.astro` define their table of contents manually through a `headings`
  array; keep it in sync with the `<h2 id>` elements when adding sections.

## Code layout

- `src/pages/` routes (blog listing and post pages, tags, archives, search, RSS, robots.txt, 404)
- `src/layouts/` page shells: `BaseLayout`, `CommonPage` (static pages), `BlogPost`,
  `IndividualPage` (Markdown pages such as terms), `ContentLayout`
- `src/components/` site-specific components, grouped by the page that uses them. Waline comments
  and view counts are in `src/components/waline/`
- `src/plugins/` local rehype and Shiki plugins
- `src/assets/styles/` global styles (`app.css`, `global.css`)
- `astro.config.mjs`, `uno.config.ts` build and styling config
- Import aliases: `@/components/*`, `@/layouts/*`, `@/assets/*`, `@/plugins/*`, `@/utils/*`,
  `@/site-config`

## Leftovers from the theme template

- `packages/pure/` is an outdated vendored copy of the theme (1.2.5). The site resolves `astro-pure`
  from npm, so edits here have no effect. Check `node_modules/astro-pure/` for current component
  props.
- `preset/` is not referenced by the site.
- `.github/` issue templates, `CODE_OF_CONDUCT.md` and the `faithful-field` package name come from
  the template.
