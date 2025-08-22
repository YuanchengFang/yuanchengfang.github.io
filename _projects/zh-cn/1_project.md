---
page_id: project_1
layout: page
title: 项目示例
description: 带有背景图片
img: assets/img/12.jpg
importance: 1
category: work
related_publications: true
---

每个项目都可以有一个漂亮的功能展示页面。  
你可以很方便地在一个灵活的三列网格中插入图片。  
你的照片可以是 1/3、2/3，或者占满整行。

如果你想在作品集页面里给项目加一个背景图，只需要在 front matter 中添加 `img` 标签即可，例如：

    ---
    layout: page
    title: project
    description: 一个带背景图的项目
    img: /assets/img/12.jpg
    ---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    很容易就能给照片加上说明。左边，一条公路穿过隧道；中间，落叶在文艺摄影中随风飘落；右边，在另一场文艺摄影里，一个伐木工抓着一把松针。
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    这张图片同样可以有说明，就像变魔术一样。
</div>

你也可以在图片行之间加入普通文字，甚至是引用 {% cite einstein1950meaning %}。  
比如你想在贴出剩余的图片前，先写一点关于你项目的介绍。  
你可以描写自己为项目付出的辛劳、汗水，甚至是“流血”，然后……在下一行图片里揭示它的荣耀。

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    你也可以像这样做成艺术感十足的 2/3 + 1/3 图片组合。
</div>

代码其实很简单。  
只需把图片包裹在 `<div class="col-sm">` 里，再放到 `<div class="row">` 里面（更多信息可以参考 <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> 系统）。  
要让图片自适应，可以为它们添加 `img-fluid` 类；要让边角圆润、带阴影，可以使用 `rounded` 和 `z-depth-1` 类。  
下面就是上面最后一行图片的代码：

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
