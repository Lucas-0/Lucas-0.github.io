# Template & Module


---

&nbsp;&nbsp;

可能会用到的简易网页设计，在此记录一下。

&nbsp;&nbsp;

&nbsp;&nbsp;

# 设置对齐和字体大小 #

```html
<p style="text-align:center"><font size="5">
size可取1~6，3为默认
</font></p>
```

---

# 提示块 (note)  #

```xml
{% note default %}
default 提示块标签
{% endnote %}

{% note primary no-icon %}
primary 提示块标签
{% endnote %}

{% note success %}
success 提示块标签
{% endnote %}

{% note info %}
info 提示块标签
{% endnote %}

{% note warning %}
warning 提示块标签
{% endnote %}

{% note danger %}
danger 提示块标签
{% endnote %}
```

![](https://cdn.jsdelivr.net/gh/Lucas-0/Img/20200411211619.png)

---
# Gallery #

在 page 中使用：

```html
<div class="gallery-group-main">
{% galleryGroup name description link img-url %}
{% galleryGroup name description link img-url %}
{% galleryGroup name description link img-url %}
</div>
```

或者在文章中加入：

```html
{% gallery %}
markdown 圖片格式
{% endgallery %}
```

---
# 设置页内跳转 #

```html
[跳转到页脚位置](#PageFooter)
<span id="PageFooter">Hello World</span>
```

---
# 设置 `hideblock` #

```html
{% hideBlock display,bg,color %}
content
{% endhideBlock %}

{% hideInline content,display,bg,color %}

```

---

# 卡片样式 #

```html
<table border="2" cellspacing="3%" frame="hsides" style="background-color:#d1eac157;opacity:0.9">
   <tr>
     <th align="center">作品名</th>
     <th align="center">Comment</th>
  </tr>
   <tr>
     <td width=30% align="center">
         <img src="" alt="" max-width:100% max-width:100% "/></td>
     <td width=70% style="text-align:left"></td>
   </tr>
   <tr>
        <td align=center>评分：</td>
        <td align=center>★★★★☆</td>
   </tr>
</table>
```

例如下面的效果(图片使用3：4）：

<table border="2" cellspacing="3%" frame="hsides" style="background-color:#d1eac157;">
   <tr>
     <th align="center">钢之炼金术师 FULLMETAL ALCHEMIST</th>
     <th align="center">say something</th>
  </tr>
   <tr>
     <td width=30% align="center">
         <img src="https://cdn.jsdelivr.net/gh/Lucas-0/Img/20200408180330.jpg" alt="" max-width:100% max-width:100% /></td>
     <td width=70% style="text-align:left">The last century saw a gradual increase in literacy and thus in the number of readers. As readers increased, so the number of listeners dropped, and thus there was some reduction in the need to read aloud. As reading for the benefit of listeners grew less common, so came the popularity of reading as a private activity in such public places as libraries, trains and offices, where reading aloud would disturb other readers in a way.HTML table cellpadding 屬性可用來設計表格欄位內元素與邊框間的距離，屬於HTML 表格的基本屬性，預設的HTML 表格內的文字或圖片，會跟邊框黏在一起.</td>
   </tr>
   <tr>
        <td align=center>评分：</td>
        <td align=center>★★★★★★</td>
   </tr>
</table>
另外可用 `style="padding: 9% 0% 0% 0%"` 调整图片布局

&nbsp;&nbsp;

---

&nbsp;&nbsp;

# GitHub Flavored Markdown #

新学到的一些 syntax ，来自[https://github.blog/2020-04-09-github-protips-tips-tricks-hacks-and-secrets-from-lee-reilly/](https://github.blog/2020-04-09-github-protips-tips-tricks-hacks-and-secrets-from-lee-reilly/)

## 1. 键盘样式标签 ` <kbd></kbd>`  ##

```
Press <kbd>W</kbd> to go up, and <kbd>A</kbd> to go down.
If you can find the <kbd>ESC</kbd>, pressing that will fire missiles
```

Press <kbd>W</kbd> to go up, and <kbd>A</kbd> to go down.
If you can find the <kbd>ESC</kbd>, pressing that will fire missiles

## 2. 十六进制颜色 `#C6E48B`  ##

```
GitHub contribution graph colors: `#C6E48B` `#7AC96F` `#249A3C` `#196127`
```

但是在 typora 里渲染不出来，可能是 GitHub 独家的功能吧。

## 3. Visualizing diffs ##

```
​```diff
10 PRINT “BASIC IS COOL”
- 20 GOTO 11
+ 20 GOTO 10
​```
```

```diff
10 PRINT “BASIC IS COOL”
- 20 GOTO 11
+ 20 GOTO 10
```

## 4. The devil’s in the details （节约页面空间） ##

```
Having some problems firing up the laser.

<details>
<summary>Click here to see terminal history + debug info</summary>
<pre>
488 cd /opt/LLL/controller/laser/
489 vi LLLSDLaserControl.c
490 make
491 make install
492 ./sanity_check
493 ./configure -o test.cfg
494 vi test.cfg
495 vi ~/last_will_and_testament.txt
496 cat /proc/meminfo
497 ps -a -x -u
498 kill -9 2207
499 kill 2208
500 ps -a -x -u
501 touch /opt/LLL/run/ok
502 LLLSDLaserControl -ok1
</details>
```

Having some problems firing up the laser.

<details>
<summary>Click here to see terminal history + debug info</summary>
<pre>
488 cd /opt/LLL/controller/laser/
489 vi LLLSDLaserControl.c
490 make
491 make install
492 ./sanity_check
493 ./configure -o test.cfg
494 vi test.cfg
495 vi ~/last_will_and_testament.txt
496 cat /proc/meminfo
497 ps -a -x -u
498 kill -9 2207
499 kill 2208
500 ps -a -x -u
501 touch /opt/LLL/run/ok
502 LLLSDLaserControl -ok1
</details>


## 5. 小字标签 ##
`<sub></sub>` or `<sup></sup>` （适合图片注释）

```
<sup><strong>Fig 1:</strong> Megatocat into action</sup>
<sub><strong>Fig 1:</strong> Megatocat into action</sub>
```

<div align="center"><sup><strong>Fig 1:</strong> Megatocat into action
  </sup><br><sub><strong>Fig 1:</strong> Megatocat into action</sub></div>

&nbsp;&nbsp;

&nbsp;&nbsp;

