# Blog 施工日志


---

&nbsp;&nbsp;

**2020.5.15 更新：**
转到 hugo.even

&nbsp;&nbsp;

---

&nbsp;&nbsp;

经过几天的倒腾，与 `Next` ， `Icarus` 等相比，确定了博客目前的 `Butterfly` 方案。

`Butterfly` 的教程还算完善，不过有些私人化的配置还是记下来比较好。

&nbsp;&nbsp;


&nbsp;&nbsp;

## 导航栏 ##

除了 `Archives` 之外，其他的都必须自己生成，虽然不难，姑且提一句。真正需要注意的是 `link` 的生成，按照原作者的教程是行不通的，而网上大多是不经验证的转载，所以都没能发现这一问题。

原因在于作者给出的 `link.yml` 模板中空格错误，所以不能正确被读取。按照下面文章的模板替换原作者的教程就行了。

[Hexo遇到的那些坑](https://xiabor.com/2019/12/07/hexo1/)

&nbsp;&nbsp;

---

&nbsp;&nbsp;

## Page ##

这部分看[原作者的教程](https://jerryc.me/)就好了，只不过导航栏的语言设置有点迷。除了 `archive` ，其他点进去都是英文。我本以为是在 `language` 中翻译，但是没有作用。因为这部分显示的是Page的title，需要在 `md` 文件改。同样，Page的顶栏图像是在 `md` 文件的头部描述设置，另外 `post` 模板可以把参数全写上，用不到的注释掉，这样每篇文章都能定制属性。

&nbsp;&nbsp;

---

&nbsp;&nbsp;

## 小改进 ##

把图标换成了国际象棋里的骑士。把默认字体大小改成了 16 px 。还有颜色都是按照[教程](https://xiabor.com/2020/03/29/hexo2/)来做的。

[Butterfly主题更新总结](https://xiabor.com/2020/03/29/hexo2)

### 修改打赏框 ###

原始的打赏框宽度为 320 px ，二维码宽度为 130 px ，如果想用更大的框装更大的图。

方法：找到 `butterfly/source/css/_layout/reward.styl` 中的代码段：

```css
.reward-all
  display: inline-block
  margin: 0 0 0 -110px
  padding: 20px 10px 8px
  width: 320px
  border-radius: 4px
  background: $reward-pop-up-bg
```

`width` 为宽度， `margin` 为偏移。举例， `width` 增加100px，则 `margin` 绝对值增加 $100\div 2=50$ ​px 。
二维码宽度的修改在最下方，将宽度从 130 px 修改为 200 px （我用的是 3:4 的图片）。

```css
img
  position: relative
  max-width: 200px
  width: 200px
  border-radius: 5px
```

修改 `width` 数值即可。

### 修改 hover 旋转 ###


`aside.styl` 这一段设置主页头像的旋转角度，不知道为什么 540 ，实际用起来只有 180 。不过我不想要这个，设置成 0 .

```css
.card-info
  img
    display: inline-block
    width: 110px
    height: 110px
    border-radius: 70px
    transition: all .3s

    &:hover
      transform: rotate(540deg)
```

在下面的位置找到 `social-link-icon` 将旋转角度为 360 。
在 `flink.styl` 里将 `rotate` 属性设置为360。

### 修改 note 颜色 ###

`config.yml` 里面找不到的颜色，基本都可以去 `var.styl` 里面找到。下面是我修改了默认 `note` 的灰色为浅绿色，图标也可以修改。

```css
// Default
$note-default-border = #91b30dcf
```
### 修改图片排布方式 ###

`post.styl` 中，找到下面的代码

```css
#article-container
  a
    color: $theme-link-color

    &:hover
      text-decoration: underline

  img
    margin: 0 auto .8rem
```
将 `margin` 属性修改为 `0 0` 。这是在我用表格插入图片的时候发现的，居然没有居中对齐，不可原谅。

### 修改页面透明度 ###

默认的页面颜色为白色 `#FFFFFF` ,在启用动效之后，卡片、 post 会挡住彩带。经过一番鏖战，定位到 `var.styl` 中，宏定义了 `$white= #FFFFFF` ,在此修改透明度，比如改成 `#FFFFFF47` 。另外， `F12`+`VSCode` 大法真香。

### Comment ###

从 `livere` 切换到 `Utterances` 。前者加载略慢，而且要拉到底部才开始加载。不过本来也不会有啥评论的🤣

### 修改弹窗文字居中 ###

vscode搜索 `snackbar` ，发现 `css` 在 cdn 链接中不能直接修改。复制到本地修改，并把链接指向本地文件。

```
#https://cdn.jsdelivr.net/npm/node-snackbar/dist/snackbar.min.css
justify-content:space-between #将space-between改为center
```

---

细小的修改很难全部写出来，也无必要，为了让文章不致那么琐碎，就用上面那些作为例子吧。
博客作为一种 old-fashion 的存在，提供了一个既公开又疏远的空间，正好用来躲避社群生活的毒素，用于干净的思考。孔子说：“质胜文则野，文胜质则史。文质彬彬，然后君子。”就以此为目标前进吧。

&nbsp;&nbsp;

---

&nbsp;&nbsp;

## 参考链接 ##

[自写与收集的一些免费的API接口[获取QQ昵称、头像、QQ秀等等...]](https://www.nbmao.com/archives/4007)

[hexo 添加自定义页面](https://www.jianshu.com/p/a25bfaa4c7cb)

[Hexo安装并使用Butterfly主题](https://www.antmoe.com/posts/75a6347a/)

[Hexo-theme-butterfly修改调整记录教程](https://www.larscheng.com/butterfly/)

[Hexo写文章的一些小技巧](https://xiabor.com/2019/12/31/postskill)

&nbsp;&nbsp;

&nbsp;&nbsp;

