---
title: Hello World
---

# C# Markdown组件

GITHUB C#实现的Markdown:
https://github.com/xoofx/markdig

GITHUB:为ASPNETCORE做的适配：
https://github.com/RickStrahl/Westwind.AspNetCore.Markdown

`Westwind.AspNetCore.Markdown`的实现说明解释：
https://www.codemag.com/Article/1811071/Marking-up-the-Web-with-ASP.NET-Core-and-Markdown

---
*以下都是瞎测这玩的*

## 图
```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

## task list

- [ ] Item1
- [x] Item2
- [ ] Item3
- [ ] Item4



<ul class="contains-task-list">
<li class="task-list-item"><input disabled="disabled" type="checkbox" /> Item1</li>
<li class="task-list-item"><input disabled="disabled" type="checkbox" checked="checked" /> Item2</li>
<li class="task-list-item"><input disabled="disabled" type="checkbox" /> Item3</li>
<li>Item4</li>
</ul>


^^^
This is a figure
^^^ This is a *caption*

<figure>
<p>This is a figure</p>
<figcaption>This is a <em>caption</em></figcaption>
</figure>



Term 1
:   This is a definition item
    With a paragraph
    > This is a block quote

    - This is a list
    - with an item2

    ```java
    Test


    ```

    And a last line
:   This ia another definition item

Term2
Term3 *with some inline*
:   This is another definition for term2
.
<dl>
<dt>Term 1</dt>
<dd><p>This is a definition item
With a paragraph</p>
<blockquote>
<p>This is a block quote</p>
</blockquote>
<ul>
<li>This is a list</li>
<li>with an item2</li>
</ul>
<pre><code class="language-java">Test


</code></pre>
<p>And a last line</p>
</dd>
<dd>This ia another definition item</dd>
<dt>Term2</dt>
<dt>Term3 <em>with some inline</em></dt>
<dd>This is another definition for term2</dd>
</dl>


This is a test with a :) and a :angry: smiley
.
<p>This is a test with a 😃 and a 😠 smiley</p>
