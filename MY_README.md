Hugo 版本: [hugo_extended_0.102.3](https://github.com/gohugoio/hugo/releases/tag/v0.102.3)

（一）创建首页

```
hugo new _index.md
```

（二）创建 `about` 页面

```
hugo new about.md
```

（三）新增 `archives` 页面

1. 创建 `archives` 页面

```
hugo new archives.md
```

2. `archives.md` 的 frontmatter 应包含以下内容：

```
title: "Archives"
layout: "archives"
```

3. `config.yaml` 内的 `menu\nav` 中新增 `archives`：

```
menu:
  nav:
    - name: Home
      url: /
      weight: 1
    - name: Blog
      url: /post/
      weight: 2
    - name: Tags
      url: /tags/
      weight: 3
    - name: Archives
      url: /archives/
      weight: 4
    - name: About
      url: /about/
      weight: 5
    - name: RSS
      url: /index.xml
      weight: 6
```

4. 在 `themes\cupper-hugo-theme\layouts\_default` 目录下新建 `archives.html` 页面，并加入以下代码：

```
{{ define "main" }}
<main class="content" role="main">
    <h1>{{ .Title }}</h1>
    <div class="inner">
        {{ range (.Site.RegularPages.GroupByDate "2006") }}
            <h2>{{ .Key }}</h2>

            <ul class="patterns-list" id="list">
                {{ range (where .Pages "Type" "post") }}
                    <li>
                        <h4><a href="{{ .RelPermalink }}">{{ .PublishDate.Format "01-02" }} : {{ .Title }}</a></h4>
                    </li>
                {{ end }}
            </ul>
        {{ end }}
    </div>
</main>
{{ end }}
```

（四）增加 Katex 的行内公式功能

在 `themes\cupper-hugo-theme\layouts\partials\katex.html` 中添加以下内容：

```javascript
<script>
    document.addEventListener("DOMContentLoaded", function() {
        renderMathInElement(document.body, {
            delimiters: [
              {left: "$$", right: "$$", display: true},
              {left: "$", right: "$", display: false}
            ]
        });
    });
</script>
```

（五）删去评论功能

