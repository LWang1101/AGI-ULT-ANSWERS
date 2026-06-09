# 这是 <h1> 一级标题

## 这是 <h2> 二级标题

### 这是 <h3> 三级标题

#### 这是 <h4> 四级标题

##### 这是 <h5> 五级标题

###### 这是 <h6> 六级标题

# 这个标题拥有 1 个 id {#my_id}

# 这个标题有 2 个 classes {.class1 .class2}

*这会是 斜体 的文字*  
_这会是 斜体 的文字_

**这会是 粗体 的文字**  
__这会是 粗体 的文字__  

_你也 **组合** 这些符号_

~~这个文字将会被横线删除~~

- Item 1
- Item 2
  - Item 2a
  - Item 2b

1. Item 1
1. Item 2
1. Item 3
   1. Item 3a
   1. Item 3b

![GitHub Logo](/images/logo.png)
Format: ![Alt Text](url)

https://github.com - 自动生成！
[GitHub](https://github.com)

正如 Kanye West 所说：

> We're living the future so
> the present is our past.

如下，三个或者更多的

---

连字符

---

星号

---

下划线

我觉得你应该在这里使用
`<addr>` 才对。

你可以在你的代码上面和下面添加 ``` 来表示代码块。

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```

代码块 class（MPE 扩展的特性）  
你可以给你的代码块设置 class。

例如，添加 class1 class2 到一个 代码块：

```javascript {.class1 .class}
function add(x, y) {
  return x + y
}
```

如果你想要你的代码块显示代码行数，只要添加 line-numbers class 就可以了。

例如：

```javascript {.line-numbers}
function add(x, y) {
  return x + y
}
```

高亮代码行数
你可以通过添加 highlight 属性的方式来高亮代码行数：

```javascript {highlight=10}
```

```javascript {highlight=10-20}
```

```javascript {highlight=[1-10,15,20-22]}
```

任务列表
- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
- [x] this is a complete item
- [ ] this is an incomplete item

表格
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column

表格  
需要在插件设置中打开 enableExtendedTableSyntax 选项来使其工作。
![example](https://user-images.githubusercontent.com/1908863/28243710-945e3004-699a-11e7-9a5f-d74f6c944c3b.png)

Emoji & Font-Awesome  
只适用于 markdown-it parser 而不适用于 pandoc parser  。
缺省下是启用的。你可以在插件设置里禁用此功能。  

:smile:
:car:

上标  
30^th^  

下标  
H~2~O

脚注  
Content [^1]  
[^1]: Hi! This is a footnote

缩略  
*[HTML]: Hyper Text Markup Language  
*[W3C]: World Wide Web Consortium  
The HTML specification  
is maintained by the W3C.  
标记  
==marked==  
