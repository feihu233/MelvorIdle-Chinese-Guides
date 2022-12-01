# GFM 额外支持机制
~~删除线~~：两个~  
链接不再需要\<>
单行分割线`---`
`<!-- 注释 -->`  
空两格换行  

## 脚注
维基不支持脚注[^1]  
[^1]: 这行可以放任意位置，但都会显示在页面底部

## 颜色标识
仅 issue，pull requset，discussion
* `#0969DA`
* `rgb(9, 105, 218)`
* `hsl(212, 92%, 45%)`

## 待办事项
- [ ] 代办1
- [x] 代办2 - 已完成

## Emoji
:grinning:  
:heart_eyes:  
https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md  
https://www.webfx.com/tools/emoji-cheat-sheet/  

## 折叠
<details>隐藏了喔</details>
<details open>
<summary>更改标题</summary>
默认可见
</details>

## 数学公式
行内公式用 `$`  
块公式用 `$$ $$`  
块公式还可用代码块，语言为 math  
<span>$</span>符号要用 span 标签包裹

## 关系图
支持 Mermaid 语法

## 容易疏漏的机制
<sub>下标</sub><sup>上标</sup>  
图片，可连外站 `![]()`  
`\*忽略 md 格式\*`

## 由 GFM 带到现代标准中的机制，或不明显的机制
表格，包括表格的左中右对齐  
代码块与语法高亮  
禁用部分标签
* title, plaintext
* textarea
* style, script
* noembed
* iframe, noframes

## 实验性质
需要在开头加 xx: true  
代码块流程图：sequence，flow

## 可能不支持的机制
_斜体_，在句中_不显示_<-“不显示”是斜体  