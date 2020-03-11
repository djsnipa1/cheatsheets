# Organizing information with tables

You can build tables to organize information in comments, issues, pull requests, and wikis.

### [In this article](#in-this-article)

*   [Creating a table](#creating-a-table)
*   [Formatting content within your table](#formatting-content-within-your-table)
*   [Further reading](#further-reading)

### [Creating a table](#creating-a-table)

You can create tables with pipes `|` and hyphens `-`. Hyphens are used to create each column's header, while pipes separate each column. You must include a blank line before your table in order for it to correctly render.

```
| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |

```

![Rendered table](https://help.github.com/assets/images/help/writing/table-basic-rendered.png)

The pipes on either end of the table are optional.

Cells can vary in width and do not need to be perfectly aligned within columns. There must be at least three hyphens in each column of the header row.

```
| Command | Description |
| --- | --- |
| git status | List all new or modified files |
| git diff | Show file differences that haven't been staged |

```

![Rendered table with varied cell width](https://help.github.com/assets/images/help/writing/table-varied-columns-rendered.png)

### [Formatting content within your table](#formatting-content-within-your-table)

You can use [formatting](https://help.github.com/en/articles/basic-writing-and-formatting-syntax) such as links, inline code blocks, and text styling within your table:

```
| Command | Description |
| --- | --- |
| `git status` | List all *new or modified* files |
| `git diff` | Show file differences that **haven't been** staged |

```

![Rendered table with formatted text](https://help.github.com/assets/images/help/writing/table-inline-formatting-rendered.png)

You can align text to the left, right, or center of a column by including colons `:` to the left, right, or on both sides of the hyphens within the header row.

```
| Left-aligned | Center-aligned | Right-aligned |
| :---         |     :---:      |          ---: |
| git status   | git status     | git status    |
| git diff     | git diff       | git diff      |

```

![Rendered table with left, center, and right text alignment](https://help.github.com/assets/images/help/writing/table-aligned-text-rendered.png)

To include a pipe `|` as content within your cell, use a `\` before the pipe:

```
| Name     | Character |
| ---      | ---       |
| Backtick | `         |
| Pipe     | \|        |

```

![Rendered table with an escaped pipe](https://help.github.com/assets/images/help/writing/table-escaped-character-rendered.png)

### [Further reading](#further-reading)

*   [GitHub Flavored Markdown Spec](https://github.github.com/gfm/)
*   "[Basic writing and formatting syntax](https://help.github.com/en/articles/basic-writing-and-formatting-syntax)"
