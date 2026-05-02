# Seumas Blog

Hugo blog scaffold using the `risotto` theme.

## Local preview

```bash
hugo server -D
```

Open <http://localhost:1313/>.

## Build

```bash
hugo --minify
```

The generated site is written to `public/`.

## Add a post

```bash
hugo new content post/my-new-post.md
```

Then edit the generated Markdown file under `content/post/`.
