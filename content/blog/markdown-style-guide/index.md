---
title: "Markdown Style Guide"
date: 2024-01-15
description: "A comprehensive guide showcasing all markdown elements and how they render on this blog."
tags:
  - markdown
  - style
  - reference
categories:
  - guides
---

This post demonstrates all the markdown elements supported by this blog. Use it as a reference for writing posts and to verify that styling looks correct.

## Headings

Headings help structure your content. Here's how each level looks:

# Heading Level 1

## Heading Level 2

### Heading Level 3

#### Heading Level 4

##### Heading Level 5

###### Heading Level 6

---

## Text Formatting

Regular paragraph text flows naturally. You can use **bold text** for emphasis, *italic text* for subtle emphasis, or ***bold and italic*** together. Sometimes you need ~~strikethrough~~ for corrections.

Here's another paragraph to show spacing between blocks of text. Good typography needs breathing room between elements.

---

## Blockquotes

> This is a blockquote. It's useful for highlighting quotes, important notes, or setting apart text that deserves special attention.
>
> Blockquotes can span multiple paragraphs.

Nested blockquotes work too:

> This is the outer quote.
>
> > And this is a nested quote inside it.
> >
> > It can have multiple lines as well.

---

## Lists

### Unordered Lists

- First item in the list
- Second item in the list
  - Nested item one
  - Nested item two
    - Even deeper nesting
- Third item in the list

### Ordered Lists

1. First step
2. Second step
   1. Sub-step A
   2. Sub-step B
3. Third step
4. Fourth step

### Mixed Lists

1. Start with a numbered item
   - Then add bullets
   - Another bullet
2. Back to numbers
   - More bullets here

---

## Code

### Inline Code

Use `inline code` for short snippets like variable names (`myVariable`), file paths (`/etc/config`), or commands (`npm install`).

### Code Blocks

Here's a JavaScript function:

```javascript
function greet(name) {
  const message = `Hello, ${name}!`;
  console.log(message);
  return message;
}

// Call the function
greet('World');
```

Python example:

```python
def fibonacci(n):
    """Generate Fibonacci sequence up to n terms."""
    a, b = 0, 1
    result = []
    for _ in range(n):
        result.append(a)
        a, b = b, a + b
    return result

print(fibonacci(10))
```

HTML example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Hello World</title>
</head>
<body>
  <h1>Welcome</h1>
  <p>This is a paragraph.</p>
</body>
</html>
```

Plain text block (no syntax highlighting):

```
This is just plain text
without any highlighting.
Useful for logs or simple output.
```

---

## Tables

| Name | Role | Location |
|------|------|----------|
| Alice | Developer | Tokyo |
| Bob | Designer | Osaka |
| Carol | Manager | Kyoto |

Tables with alignment:

| Left Aligned | Center Aligned | Right Aligned |
|:-------------|:--------------:|--------------:|
| Text | Text | Text |
| More text | More text | More text |
| Even more | Even more | Even more |

---

## Links

Here's a [link to an external site](https://example.com) and here's one to an [internal page](/about/).

You can also write bare URLs if needed, though linked text is usually cleaner.

---

## Images

Images would go here with the standard markdown syntax:

```markdown
![Alt text for the image](image.jpg)
```

---

## Horizontal Rules

Use horizontal rules to separate major sections:

---

Like this.

---

Or this.

---

## Japanese Text Sample

日本語テキストのサンプルです。フォントの表示を確認するために使用します。

### 漢字・ひらがな・カタカナ

吾輩は猫である。名前はまだ無い。どこで生れたかとんと見当がつかぬ。

カタカナも表示できます：コンピューター、プログラミング、インターネット。

### 長文サンプル

春はあけぼの。やうやう白くなりゆく山際、少し明かりて、紫だちたる雲の細くたなびきたる。夏は夜。月のころはさらなり、闇もなほ、蛍の多く飛びちがひたる。また、ただ一つ二つなど、ほのかにうち光て行くもをかし。雨など降るもをかし。

---

## Combined Elements

Sometimes you need to combine elements:

> **Note:** This blockquote contains `inline code` and a [link](#).
>
> - It can also have lists
> - With multiple items

1. Start with an ordered list
   > Include a blockquote inside
2. Continue the list
   ```
   Add a code block
   ```
3. And finish up

---

## Conclusion

This style guide covers the essential markdown elements. Use it to test your theme's typography and ensure everything renders correctly.

*Happy writing!*
