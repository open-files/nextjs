---
created_at: 2026-02-03
updated_at: 2026-02-03
---

[![Read on readonly.page][readonly-badge]][read-on-readonly]

# Next.js Cheat Sheet

Next.js is a framework based on [**React**][react] and is maintained by
[**Vercel, Inc**](https://vercel.com/).

## Start an app

### Create a new app with the CLI

```sh
# pnpm / npm / yarn / bun
pnpm create next-app@latest my-app --yes
```

`--yes` skips prompts using defaults.

[Official Docs][quick-start]

### Manual installation

```sh
# pnpm / npm / yarn / bun
pnpm i next@latest react@latest react-dom@latest
```

[Official Docs][manual-installation]

## Project structure

Next.js uses **file-system** routing.

### `app` folder

Two options to place `app` folder:

#### Option 1: in _root_ folder

```text
my-app/
└─ app/
```

#### Option 2: in `src` folder

```text
my-app/
└─ src/
   └─ app/
```

### `layout`, root `layout`, and `page`

- `page` exposes a route, `layout` is for shared UI.
- A [root `layout`][root-layout] is the top-most `layout` that defines the
  `<html>` and `<body>` tags.
- Multiple root `layout` files is allowed.(See: [root layout][root-layout])
- `layout` and `page` must use `export default` (component name doesn't matter)

### `route` file

[`route`][route] file exposes an API endpoint.

### URL path folders

- Regular folders define fixed URL segments, e.g. `app/blog/page.tsx` =>
  `/blog`.
- Square brackets define dynamic URL segments:
  - `app/shop/[slug]/page.tsx` matches `/shop/clothing`.
  - `app/shop/[...slug]/page.tsx` matches `/shop/clothing`,
    `/shop/clothing/shirts`.
  - `app/shop/[[...slug]]/page.tsx` matches `/shop`, `/shop/clothing`,
    `/shop/clothing/shirts`.

### Non-URL path folders

These folders do not add an extra URL segment:

- `(group)` for grouping files ([route groups][route-groups]).
- `_folder` is a [private folder][private-folder] (not routable).
- `@folder` for a named [slot][slots] ([parallel routes][parallel-routes]).
- `(.)folder`, `(..)folder`, `(..)(..)folder`, and `(...)folder` are
  intercepting folders ([intercepting routes][intercepting-routes]).

### Component hierarchy

`layout` > `template` > `error` > `loading` > `not-found` > `page` (or nested
`layout`)

More about [Component hierarchy][component-hierarchy].

## Parallel Routes

`children` prop is an implicit slot. It means `app/page.tsx` equals to
`app/@children/page.tsx`

## Build-in Components

### `Link`

`<Link>` is preferred for navigating between internal routes. For external
links, `<Links>` usually makes no difference compared to `<a>`.

## Metadata and SEO

### Files

[`robots`][static-robotstxt] files must be in `/app` folder (`robots.text` can
be in `/public` folder).

Other metadata files see: [Metadata file conventions][metadata-file-conventions]

### Metadata

Do not add `<title>` and `<meta>` tags manually, use [**Metadata
API**][metadata-and-og-images] instead.

[readonly-badge]:
  https://img.shields.io/badge/Read_on-Readonly.page-blue?style=for-the-badge
[read-on-readonly]:
  https://readonly.page/read#url=open-files.github.io/nextjs/cheatsheet.md
[react]: https://react.dev/
[quick-start]:
  https://nextjs.org/docs/app/getting-started/installation#quick-start
[root-layout]:
  https://nextjs.org/docs/app/api-reference/file-conventions/layout#root-layout
[route-groups]:
  https://nextjs.org/docs/app/api-reference/file-conventions/route-groups#convention
[private-folder]:
  https://nextjs.org/docs/app/getting-started/project-structure#private-folders
[slots]:
  https://nextjs.org/docs/app/api-reference/file-conventions/parallel-routes#slots
[parallel-routes]:
  https://nextjs.org/docs/app/api-reference/file-conventions/parallel-routes
[intercepting-routes]:
  https://nextjs.org/docs/app/api-reference/file-conventions/intercepting-routes
[component-hierarchy]:
  https://nextjs.org/docs/app/getting-started/project-structure#component-hierarchy
[static-robotstxt]:
  https://nextjs.org/docs/app/api-reference/file-conventions/metadata/robots#static-robotstxt
[metadata-file-conventions]:
  https://nextjs.org/docs/app/getting-started/project-structure#metadata-file-conventions
[manual-installation]:
  https://nextjs.org/docs/app/getting-started/installation#manual-installation
[metadata-and-og-images]:
  https://nextjs.org/docs/app/getting-started/metadata-and-og-images
[route]: (https://nextjs.org/docs/app/api-reference/file-conventions/route)
