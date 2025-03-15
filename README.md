# Yuta Tokoi's Blog

This blog uses the [Miniblog template](https://github.com/nicholasdly/miniblog) for the Astro web framework.

## Getting Started

1. Enter Nix development shell:

```bash
nix-shell
```

2. Install dependencies:

```bash
npm install
```

3. Start the development server:

```bash
npm run dev
```

4. Optionally, format your code after making changes:

```bash
npm run format
```

## Customization

### Site Configuration

Edit the `src/consts.ts` file to update your information and site's metadata:

```ts
export const SITE_URL = "https://yutatokoi.com";
export const SITE_TITLE = "Yuta Tokoi";
export const SITE_DESCRIPTION = "Yuta Tokoi's Website | 床井祐太のウェブサイト";
```

### Blog Posts

Add new blog posts as Markdown or MDX files in the `src/content/posts/` directory. Use the following frontmatter structure:

```yml
---
title: "Lorem Ipsum"
description: "Lorem ipsum dolor sit amet."
date: "2024-11-06"
---
```

### Markdown Styling

All Markdown-specific CSS styling is customizable in `src/styles/global.css`:

```css
@layer components {
  article {
    /* ... */
  }
}
```

## License

This project is open source and available under the [MIT License](LICENSE).
