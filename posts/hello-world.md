Welcome! This whole blog is **plain files**: one `index.html`, a folder of markdown posts, and a folder of images. Nothing to install, nothing to build.

## Writing a post

1. Create `posts/my-post.md` and write normal markdown.
2. Add one entry to `posts/posts.json` with the slug, title, date, summary, and tags.
3. Refresh. Done.

## Images

Drop files into `images/` and reference them like any markdown image:

![A sample diagram](images/sample.svg)

## Code snippets

Fenced code blocks get syntax highlighting and a copy button:

```python
def greet(name: str) -> str:
    """The obligatory example."""
    return f"Hello, {name}!"

print(greet("world"))
```

```javascript
const posts = await fetch("posts/posts.json").then(r => r.json());
console.log(`Loaded ${posts.length} posts`);
```

## Everything else markdown gives you

> Blockquotes work, and so do inline `code spans`, **bold**, *italics*, and [links](https://example.com).

| Feature | Included |
|---|---|
| Search | press `/` anywhere |
| Dark mode | the ◐ button |
| RSS | no — add later if needed |

That's the whole system. If you can edit a text file, you can publish.
