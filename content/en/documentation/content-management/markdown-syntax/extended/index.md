---
title: Extended Markdown Syntax
date: 2023-02-24T21:42:22+08:00
type: posts
author:
  name: Lruihao
  link: https://lruihao.cn
description: This article shows the extended Markdown syntax and format in FixIt theme.
resources:
  - name: featured-image
    src: featured-image.webp
tags:
  - Markdown
  - Content
  - HTML
  - Advanced
categories:
  - Documentation
collections:
  - Markdown Syntax
math: true
---
<!-- markdownlint-disable-file reference-links-images -->
**FixIt** theme has some extended syntax elements for you to write articles.

<!--more-->

## Alerts {#alerts}

{{< version 0.3.10 >}}

> This syntax is compatible with the [GitHub Alert][github-alert] Markdown extension.

Also known as callouts or admonitions, alerts are blockquotes used to emphasize critical information. An example of all five types:

```markdown {data-open=true}
> [!NOTE]
> Highlights information that users should take into account, even when skimming.

> [!TIP]
> Optional information to help a user be more successful.

> [!IMPORTANT]
> Crucial information necessary for users to succeed.

> [!WARNING]
> Critical content demanding immediate user attention due to potential risks.

> [!CAUTION]
> Negative potential consequences of an action.
```

Here is how they are displayed:

> [!NOTE]
> Highlights information that users should take into account, even when skimming.

> [!TIP]
> Optional information to help a user be more successful.

> [!IMPORTANT]
> Crucial information necessary for users to succeed.

> [!WARNING]
> Critical content demanding immediate user attention due to potential risks.

> [!CAUTION]
> Negative potential consequences of an action.

## Inserted Text {#inserted-text}

**Hugo** supports an **inserted text** Markdown extension:

```markdown
The author of FixIt theme is ++Lruihao++.
```

The rendered output looks like this:

The author of FixIt theme is ++Lruihao++.

## Marked Text {#marked-text}

**Hugo** supports a **marked text** Markdown extension:

```markdown
==FixIt== is an awesome Hugo theme!
```

The rendered output looks like this:

==FixIt== is an awesome Hugo theme!

## Subscript {#subscript}

**Hugo** supports a **subscript** Markdown extension:

```markdown
The chemical formula of water is H~2~O.
```

The rendered output looks like this:

The chemical formula of water is H~2~O.

## Superscript {#superscript}

**Hugo** supports a **superscript** Markdown extension:

```markdown
2^10^ equals 1024.
```

The rendered output looks like this:

2^10^ equals 1024.

{{< admonition info "How to enable Hugo extended syntax" >}}

[Inserted Text](#inserted-text), [Marked Text](#marked-text), [Subscript](#subscript), and [Superscript](#superscript) syntax are disabled by default. You need to update Hugo to version `0.128.0` or later and enable the following configuration:

```toml {title="hugo.toml"}
[markup]
  [markup.goldmark]
    [markup.goldmark.extensions]
      strikethrough = false
      # https://gohugo.io/getting-started/configuration-markup/#extras
      [markup.goldmark.extensions.extras]
        [markup.goldmark.extensions.extras.delete]
          enable = true
        [markup.goldmark.extensions.extras.insert]
          enable = true
        [markup.goldmark.extensions.extras.mark]
          enable = true
        [markup.goldmark.extensions.extras.subscript]
          enable = true
        [markup.goldmark.extensions.extras.superscript]
          enable = true
```

{{< /admonition >}}

## Emoji Support

This part is shown in the [emoji support page][emoji-support].

## Mathematical Formula

{{< version 0.2.16 changed >}}

**FixIt** theme supports mathematical formulas based on [$\KaTeX$][katex].

Set the property `enable = true` under `[params.math]` in your [theme configuration][theme-config]
and the property `math: true` of the article front matter to enable the automatic rendering of mathematical formulas.

{{< admonition tip >}}
Here is a list of [$\TeX$ functions supported by $\KaTeX$](https://katex.org/docs/supported.html).
{{< /admonition >}}

{{< admonition note "Notes on Escape Characters" false >}}
Since Hugo generates HTML documents according to the syntax such as `_`, `*`, `^`, `>>` when rendering Markdown documents,
and some text content in the form of escape characters (such as `\(`, `\)`, `\[`, `\]`, `\\`) escape processing will be performed automatically,
therefore, additional escape character expressions are required for these places to achieve automatic rendering:

- `_` -> `\_`
- `*` -> `\*`
- `^` -> `\^` (If you have enabled [superscript syntax](#superscript))
- `>>` -> `\>>`
- `\(` -> `\\(`
- `\)` -> `\\)`
- `\[` -> `\\[`
- `\]` -> `\\]`
- `\\` -> `\\\\`

If you don't want to write these escape characters, **FixIt** theme supports [`raw` shortcode]({{< relref path="/documentation/content-management/shortcodes/extended/introduction#raw" >}}) to help you write raw mathematical formula content.

Example `raw` input:

```markdown
{?{}{?{}< raw >}}Inline Formula: \(\mathbf{E}=\sum_{i} \mathbf{E}_{i}=\mathbf{E}_{1}+\mathbf{E}_{2}+\mathbf{E}_{3}+\cdots\){?{}{?{}< /raw >}}

{?{}{?{}< raw >}}
Block Formula:
\[ a=b+c \\ d+e=f \]
\[ f(x)=\int_{-\infty}^{\infty} \hat{f}(\xi) e^{2 \pi i \xi x} d \xi \]
{?{}{?{}< /raw >}}
```

The rendered output looks like this:

{{< raw >}}Inline Formula: \(\mathbf{E}=\sum_{i} \mathbf{E}_{i}=\mathbf{E}_{1}+\mathbf{E}_{2}+\mathbf{E}_{3}+\cdots\){{< /raw >}}

{{< raw>}}
Block Formula:
\[ a=b+c \\ d+e=f \]
\[ f(x)=\int_{-\infty}^{\infty} \hat{f}(\xi) e^{2 \pi i \xi x} d \xi \]
{{< /raw >}}
{{< /admonition >}}

### Inline Formula

The default inline delimiters are:

- `$ ... $`
- `\( ... \)` (escaped: `\\( ... \\)`)

For example:

```tex
$c = \pm\sqrt{a\^2 + b\^2}$ 和 \\(f(x)=\int_{-\infty}\^{\infty} \hat{f}(\xi) e\^{2 \pi i \xi x} d \xi\\)
```

The rendered output looks like this:

$c = \pm\sqrt{a\^2 + b\^2}$ 和 \\(f(x)=\int_{-\infty}\^{\infty} \hat{f}(\xi) e\^{2 \pi i \xi x} d \xi\\)

### Block Formula

The default block delimiters are:

- `$$ ... $$`
- `\[ ... \]` (escaped: `\\[ ... \\]`)
- `\begin{equation} ... \end{equation}` (unnumbered: `\begin{equation*} ... \end{equation*}`)
- `\begin{align} ... \end{align}` (unnumbered: `\begin{align*} ... \end{align*}`)
- `\begin{alignat} ... \end{alignat}` (unnumbered: `\begin{alignat*} ... \end{alignat*}`)
- `\begin{gather} ... \end{gather}` (unnumbered: `\begin{gather*} ... \end{gather*}`)
- `\begin{CD} ... \end{CD}`

{{< admonition warning >}}
When there are newlines in the block formula, please turn on `goldmark.renderer.hardWraps` carefully, set it to true, Goldmark will render the newlines as `<br>` elements.
{{< /admonition >}}

For example:

```tex
$$ c = \pm\sqrt{a\^2 + b\^2} $$

\\[ f(x)=\int_{-\infty}\^{\infty} \hat{f}(\xi) e\^{2 \pi i \xi x} d \xi \\]

\begin{equation*}
  \rho \frac{\mathrm{D} \mathbf{v}}{\mathrm{D} t}=\nabla \cdot \mathbb{P}+\rho \mathbf{f}
\end{equation*}

\begin{equation}
  \mathbf{E}=\sum_{i} \mathbf{E}\_{i}=\mathbf{E}\_{1}+\mathbf{E}\_{2}+\mathbf{E}_{3}+\cdots
\end{equation}

\begin{align}
  a&=b+c \\\\
  d+e&=f
\end{align}

\begin{alignat}{2}
   10&x+&3&y = 2 \\\\
   3&x+&13&y = 4
\end{alignat}

\begin{gather}
   a=b \\\\
   e=b+c
\end{gather}

\begin{CD}
   A @>a\>> B \\\\
@VbVV @AAcA \\\\
   C @= D
\end{CD}
```

The rendered output looks like this:

$$ c = \pm\sqrt{a\^2 + b\^2} $$

\\[ f(x)=\int_{-\infty}\^{\infty} \hat{f}(\xi) e\^{2 \pi i \xi x} d \xi \\]

\begin{equation*}
  \rho \frac{\mathrm{D} \mathbf{v}}{\mathrm{D} t}=\nabla \cdot \mathbb{P}+\rho \mathbf{f}
\end{equation*}

\begin{equation}
  \mathbf{E}=\sum_{i} \mathbf{E}\_{i}=\mathbf{E}\_{1}+\mathbf{E}\_{2}+\mathbf{E}_{3}+\cdots
\end{equation}

\begin{align}
  a&=b+c \\\\
  d+e&=f
\end{align}

\begin{alignat}{2}
   10&x+&3&y = 2 \\\\
   3&x+&13&y = 4
\end{alignat}

\begin{gather}
   a=b \\\\
   e=b+c
\end{gather}

\begin{CD}
   A @>a\>> B \\\\
@VbVV @AAcA \\\\
   C @= D
\end{CD}

{{< admonition tip >}}
You can add more inline and block delimiters in your [theme configuration]({{< relref path="/documentation/getting-started/configuration#theme-configuration" >}}).
{{< /admonition >}}

### Copy-tex

**[Copy-tex][copy-tex]** is an extension for **$\KaTeX$**.

By the extension, when selecting and copying $\KaTeX$ rendered elements, copies their $\LaTeX$ source to the clipboard.

Set the property `copyTex = true` under `[params.math]` in your [theme configuration][theme-config] to enable Copy-tex.

Select and copy the formula rendered in the previous section, and you can find that the copied content is the LaTeX source code.

### mhchem

**[mhchem][mhchem]** is an extension for **$\KaTeX$**.

By the extension, you can write beautiful chemical equations easily in the article.

Set the property `mhchem = true` under `[params.math]` in your [theme configuration][theme-config] to enable mhchem.

```markdown
$$ \ce{CO2 + C -> 2 CO} $$

$$ \ce{Hg\^2+ ->[I-] HgI2 ->[I-] [Hg\^{II}I4]\^2-} $$
```

The rendered output looks like this:

$$ \ce{CO2 + C -> 2 CO} $$

$$ \ce{Hg\^2+ ->[I-] HgI2 ->[I-] [Hg\^{II}I4]\^2-} $$

## Ruby Annotation {#ruby}

An extended Markdown syntax for **ruby annotation** is supported in **FixIt** theme:

```markdown
[Hugo]{?^}(An open-source static site generator)
```

The rendered output looks like this:

[Hugo]^(An open-source static site generator)

## Fraction {#fraction}

An extended Markdown syntax for **fraction** is supported in **FixIt** theme:

```markdown
[Light]{?/}[Dark]

[99]{?/}[100]
```

The rendered output looks like this:

[Light]/[Dark]

[90]/[100]

## Font Awesome {#fontawesome}

**FixIt** theme uses [Font Awesome V6][fontawesome] as the icon library.
You can easily use these icons in your articles.

Get the `class` of icons you wanted from the [Font Awesome website][fontawesome-icons].

```markdown
Gone camping! {?:}(fa-solid fa-campground fa-fw): Be back soon.

That is so funny! {?:}(fa-regular fa-grin-tears):
```

The rendered output looks like this:

Gone camping! :(fa-solid fa-campground fa-fw): Be back soon.

That is so funny! :(fa-regular fa-grin-tears):

## Escape character {#escape-character}

In some special cases (when writing this theme documentation :(fa-regular fa-grin-squint-tears):),
your content will conflict with basic or extended Markdown syntax, and it is inevitable.

The escape character syntax can help you build the content you wanted:

```markdown
{{??}X} -> X
```

For example, two `:` will enable emoji syntax, which is not the behavior you want. The escape character syntax is like this:

```markdown
{{??}:}joy:
```

The rendered output looks like this:

**{?:}joy{?:}** instead of **:joy:**

{{< admonition tip >}}
This is related to **[an issue for Hugo](https://github.com/gohugoio/hugo/issues/4978)**, which has not been resolved.
{{< /admonition >}}

Another example is:

```markdown
[link{{??}]}(#escape-character)
```

The rendered output looks like this:

**[link{?]}(#escape-character)** instead of **[link](#escape-character)**.

## Markdown attributes

> Update your site configuration to enable [Markdown attributes][markdown-attributes] for block-level elements.

Hugo supports Markdown attributes on images and block elements including blockquotes, fenced code blocks, headings, horizontal rules, lists, paragraphs, and tables.

### Syntax

```md
some Markdown content
{#id .class1 .class2 key1="value1" key2="value2"}
```

In most cases, place the attribute list beneath the markup element. For headings and fenced code blocks, place the attribute list on the right.

| Element           | Position of attribute list |
| :---------------- | :------------------------- |
| blockquote        | bottom                     |
| fenced code block | right                      |
| heading           | right                      |
| horizontal rule   | bottom                     |
| image             | bottom                     |
| list              | bottom                     |
| paragraph         | bottom                     |
| table             | bottom                     |

### Examples

#### horizontal rule

A horizontal rule with a CSS class:

```md
---
{.awesome-hr}
```

The rendered output looks like this:

---
{.awesome-hr}

#### blockquote

A blockquote with a CSS class:

```md
> The quick brown fox jumps over the lazy dog.
{.blockquote-center}
```

The rendered output looks like this:

> The quick brown fox jumps over the lazy dog.
{.blockquote-center}

#### table & list

There are some current limitations: For tables you can currently only apply it to the full table, and for lists the `ul`/`ol`-nodes only, e.g.:

```md
* Fruit
  * Apple
  * Orange
  * Banana
  {.text-success}
* Dairy
  * Milk
  * Cheese
  {.text-warning}
{.text-primary}
```

The rendered output looks like this:

- Fruit
  - Apple
  - Orange
  - Banana
  {.text-success}
- Dairy
  - Milk
  - Cheese
  {.text-warning}
{.text-primary}

#### code fences

Note that attributes in [code fences][code-fences] must come after the opening tag, with any other highlighting processing instruction, e.g.:

````markdown
```go {.myclass linenos=table,hl_lines=[8,"15-17"],linenostart=199}
// ... code
```
````

Add `title` attribute to a code block, for example:

````markdown
```js {title="test.js"}
console.log('hello FixIt!');
```
````

The rendered output looks like this:

```js {title="test.js"}
console.log('hello FixIt!');
```

{{< version 0.3.9 >}}

Add `no-header` class to a code block to hide the header, for example:

````markdown
```js {.no-header}
function forEach(elements, handler) {
  elements = elements || [];
  for (let i = 0; i < elements.length; i++) {
    handler(elements[i]);
  }
}
```
````

The rendered output looks like this:

```js {.no-header}
function forEach(elements, handler) {
  elements = elements || [];
  for (let i = 0; i < elements.length; i++) {
    handler(elements[i]);
  }
}
```

{{< version 0.3.9 >}}

Add `data-open` attribute to a code block to force expand or collapse the code block, for example:

````markdown
```js {data-open=false}
console.log('hello FixIt!');
```
````

The rendered output looks like this:

```js {data-open=false}
console.log('hello FixIt!');
```

## Code Fences Extended

### GoAT

This part is shown in the [diagrams support][diagrams-support-goat] page.

### Mermaid

This part is shown in the [diagrams support][diagrams-support-mermaid] page.

### Timeline

This part is shown in the [Timeline support][timeline-support] page.

<!-- link reference definition -->
[github-alert]: https://github.com/orgs/community/discussions/16925
[emoji-support]: {{< relref path="/guides/emoji-support" >}}
[katex]: https://katex.org/
[theme-config]: {{< relref path="/documentation/getting-started/configuration#theme-configuration" >}}
[copy-tex]: https://github.com/Khan/KaTeX/tree/master/contrib/copy-tex
[mhchem]: https://github.com/Khan/KaTeX/tree/master/contrib/mhchem
[fontawesome]: https://fontawesome.com/
[fontawesome-icons]: https://fontawesome.com/icons?d=gallery
[markdown-attributes]: https://gohugo.io/content-management/markdown-attributes/
[code-fences]: https://gohugo.io/content-management/syntax-highlighting/#highlighting-in-code-fences
[diagrams-support-goat]: {{< relref path="/documentation/content-management/diagrams#goat" >}}
[diagrams-support-mermaid]: {{< relref path="/documentation/content-management/diagrams#mermaid" >}}
[timeline-support]: {{< relref path="/documentation/content-management/timeline-support" >}}
