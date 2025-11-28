+++
title = "Terminal Theme Features Demo"
date = "2025-11-25"
author = "Max"
tags = ["demo", "tutorial", "terminal-theme"]
description = "A comprehensive guide to all the styling features available in the Terminal theme (my current blog template)"
cover = ""
+++

This post demonstrates all the special features and styling options available in the Terminal Hugo theme.

## Basic Text Formatting

This is a regular paragraph with **bold text**, *italic text*, and ***bold italic text***. You can also use ~~strikethrough~~ text.

## Headings

# H1 Heading
## H2 Heading
### H3 Heading
#### H4 Heading

---

## Lists

### Unordered List
- First item
- Second item
  - Nested item 1
  - Nested item 2
- Third item

### Ordered List
1. First step
2. Second step
3. Third step

---

## Code Blocks

### Inline Code
Use `const variable = "value"` for inline code snippets.

### Basic Code Block
```javascript
function greet(name) {
  console.log(`Hello, ${name}!`);
  return true;
}

greet("World");
```

### Python Code with Syntax Highlighting
```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

# Generate first 10 Fibonacci numbers
for i in range(10):
    print(f"F({i}) = {fibonacci(i)}")
```

### Java Code
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Terminal Theme!");
    }
}
```

---

## Special Shortcodes

### Image Shortcode

Images with special styling and positioning:

{{< image src="https://via.placeholder.com/600x400" alt="Demo Image" position="center" style="border-radius: 8px;" >}}

### Code Shortcode with Title

{{< code language="css" title="Custom CSS Example" >}}
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.button {
  background: var(--accent);
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
}
{{< /code >}}

---

## Blockquotes

> This is a blockquote. It's perfect for highlighting important information or quotes from other sources.
>
> — Max, 2025

> **Pro Tip**: Use blockquotes to make important information stand out!

---

## Tables

| Feature | Description | Status |
|---------|-------------|--------|
| Syntax Highlighting | Beautiful code colors | ✅ |
| Responsive Design | Mobile-friendly | ✅ |
| Custom Colors | Terminal.css support | ✅ |
| Fast Loading | Optimized performance | ✅ |

---

## Links and References

- [Hugo Documentation](https://gohugo.io/)
- [Terminal Theme GitHub](https://github.com/panr/hugo-theme-terminal)
- [Terminal.css](https://panr.github.io/terminal-css/)

---

## Horizontal Rules

You can use horizontal rules to separate sections:

---

## Task Lists

- [x] Completed task
- [x] Another completed task
- [x] Pending task
- [ ] Another pending task

---

## Nested Elements

You can combine different elements:

1. **First Point**: This is important
   - Sub-point with `inline code`
   - Another sub-point with [a link](https://example.com)

2. **Second Point**:
   ```bash
   echo "Code in a list!"
   ```

3. **Third Point**:
   > A quote inside a list

---

## Emphasis and Special Characters

- Use **strong emphasis** for important points
- Use *emphasis* for subtle highlights
- Use `code` for technical terms
- Special characters: © ® ™ § ¶ • – — … " " ' '

---

## Summary

The Terminal theme offers:

1. **Beautiful Syntax Highlighting** - Powered by Chroma
2. **Custom Shortcodes** - For images and code blocks
3. **Responsive Design** - Looks great on all devices
4. **Customizable Colors** - Via Terminal.css
5. **Fast Performance** - Hugo's speed + minimal theme

Try experimenting with these features in your own posts!
