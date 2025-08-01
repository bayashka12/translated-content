---
title: 常规流中的块和内联布局
slug: Web/CSS/CSS_display/Block_and_inline_layout_in_normal_flow
---

在这篇指南中，我们会探讨块级元素和内联元素在常规流中是怎样工作的。

在 CSS 2.1 规范中我们定义了[常规流（Normal Flow）](https://www.w3.org/TR/CSS2/visuren.html#normal-flow)。常规流中的任何一个盒子总是某个*格式区域*（_formatting context_）中的一部分。块级盒子是在*块格式区域*（_block formatting context_）中工作的盒子，而内联盒子是在*内联格式区域*（_inline formatting context_）中工作的盒子。任何一个盒子总是块级盒子或内联盒子中的一种。

规范中还规定了块格式区域与内联格式区域中的元素行为。对于块级格式环境，规范内规定：

> “在一个块格式区域中，盒子会从包含块的顶部开始，按序垂直排列。同级盒子间的垂直距离会由“margin”属性决定。相邻两个块级盒子之间的垂直间距会遵循外边距折叠原则被折叠。
>
> 在一个块格式区域中，每个盒子的左外边缘会与包含块左边缘重合（如果是从右到左的排版顺序，则盒子的右外边缘与包含块右边缘重合）。” - 9.4.1

对于内联格式区域中的元素：

> “在内联格式区域中，盒子会从包含块的顶部开始，按序水平排列。只有水平外边距、边框和内边距会被保留。这些盒子可以以不同的方式在垂直方向上对齐：可以底部对齐或顶部对其，或者按文字底部进行对齐。我们把包含一串盒子的矩形区域称为一个线条框。” - 9.4.2

需要注意的是，CSS 2.1 规范将文档的书写模式定义为从上到下横板排布，这从块级盒子的垂直间距这一属性就能看出来。在竖版书写模式工作时，块元素和内联元素的行为是相同的，关于这个我们将在未来的流布局与书写模式指南中进行探讨。

## 块格式区域中的元素

比如在英语环境中，块元素工作于横板书写模式中，此时的块元素会垂直排布，一个在另一个之下。

![](mdn-horizontal.png)

而在竖版书写模式中，块元素会水平排布。

![](mdn-vertical.png)

在本指南的例子中，我们使用的是英语，因此会按横板模式进行书写。不过，即使你的文档是按照竖版模式进行书写的，描述的所有内容也都应该以相同的方式工作。

如规范中所定义，外边距使得两个块级盒子分开。这个例子展示了一个非常简单的由两个段落组成的排版，每个段落都加了一个边框。浏览器的默认样式表通过增加外边距（margin）的方式在每个段落的顶部和底部留出一定空间。

```html live-sample___normal-flow
<div class="box">
  <p>
    One November night in the year 1782, so the story runs, two brothers sat
    over their winter fire in the little French town of Annonay, watching the
    grey smoke-wreaths from the hearth curl up the wide chimney. Their names
    were Stephen and Joseph Montgolfier, they were papermakers by trade, and
    were noted as possessing thoughtful minds and a deep interest in all
    scientific knowledge and new discovery.
  </p>
  <p>
    Before that night—a memorable night, as it was to prove—hundreds of millions
    of people had watched the rising smoke-wreaths of their fires without
    drawing any special inspiration from the fact.
  </p>
</div>
```

```css live-sample___normal-flow
p {
  border: 2px solid green;
}
```

{{EmbedLiveSample("normal-flow", "", "200px")}}

如果我们将 p 元素的边距设置为 0，两个边框会紧贴在一起。

```html live-sample___normal-flow-margin-zero
<div class="box">
  <p>
    One November night in the year 1782, so the story runs, two brothers sat
    over their winter fire in the little French town of Annonay, watching the
    grey smoke-wreaths from the hearth curl up the wide chimney. Their names
    were Stephen and Joseph Montgolfier, they were papermakers by trade, and
    were noted as possessing thoughtful minds and a deep interest in all
    scientific knowledge and new discovery.
  </p>
  <p>
    Before that night—a memorable night, as it was to prove—hundreds of millions
    of people had watched the rising smoke-wreaths of their fires without
    drawing any special inspiration from the fact.
  </p>
</div>
```

```css live-sample___normal-flow-margin-zero
p {
  border: 2px solid green;
  margin: 0;
}
```

{{EmbedLiveSample("normal-flow-margin-zero")}}

默认情况下，块级元素将占据这一内联方向的所有空间，因此我们的段落会铺开分布在多行，尽可能排满他的包含块。如果限定了段落元素的宽度，第二个段落仍然会排布在第一个段落的下面——即使有足够空间使它们并排。每个块级元素都会从包含块的起始边开始，因此，在当前书写模式下，所有句子会从包含块的起始边开始。

```html live-sample___normal-flow-width
<div class="box">
  <p>
    One November night in the year 1782, so the story runs, two brothers sat
    over their winter fire in the little French town of Annonay, watching the
    grey smoke-wreaths from the hearth curl up the wide chimney. Their names
    were Stephen and Joseph Montgolfier, they were papermakers by trade, and
    were noted as possessing thoughtful minds and a deep interest in all
    scientific knowledge and new discovery.
  </p>
  <p>
    Before that night—a memorable night, as it was to prove—hundreds of millions
    of people had watched the rising smoke-wreaths of their fires without
    drawing any special inspiration from the fact.
  </p>
</div>
```

```css live-sample___normal-flow-width
p {
  border: 2px solid green;
  width: 40%;
}
```

{{EmbedLiveSample("normal-flow-width", "", "370px")}}

### 外边距折叠

在规范中提到，块级元素之间的外边距会发生折叠。这意味着，如果一个具有上边距的元素排在在一个具有下边距的元素之下时，他们之间的间距不会是这两个外边距的和，即外边距会发生折叠，简单来说就是，间距与两个外边距中的较大者一样大。

在下面的例子中，段落的上边距设为`20px`，下边距设为`40px`，而段落之间的间距大小会是`40px`。这是因为第二段中的上边距比较小被折叠，间距跟随了第一个段落更大的下边距。

```html live-sample___normal-flow-collapsing
<div class="box">
  <p>
    One November night in the year 1782, so the story runs, two brothers sat
    over their winter fire in the little French town of Annonay, watching the
    grey smoke-wreaths from the hearth curl up the wide chimney. Their names
    were Stephen and Joseph Montgolfier, they were papermakers by trade, and
    were noted as possessing thoughtful minds and a deep interest in all
    scientific knowledge and new discovery.
  </p>
  <p>
    Before that night—a memorable night, as it was to prove—hundreds of millions
    of people had watched the rising smoke-wreaths of their fires without
    drawing any special inspiration from the fact.
  </p>
</div>
```

```css live-sample___normal-flow-collapsing
p {
  border: 2px solid green;
  margin: 20px 0 40px 0;
}
```

{{EmbedLiveSample("normal-flow-collapsing", "", "230px")}}

你可以在我们的文章《[掌握外边距折叠](/zh-CN/docs/Web/CSS/CSS_box_model/Mastering_margin_collapsing)》中阅读更多关于这一部分的内容。

> [!NOTE]
> 如果不确定是否发生了外边距折叠，你可以使用浏览器的开发人员工具查看盒模型。准确的外边距值可以帮助你判断是否有外边距折叠发生。
>
> ![](box-model.png)

## 内联格式区域中的元素

内联元素按照句子在特定书写模式下运行的方向依次显示。虽然我们不倾向于认为内联元素有一个框，就像 CSS 中的所有元素一样。这些内嵌的盒子一个接一个排列。如果包含块中没有足够的空间容纳所有框，则框可以换行。创建的行称为行框。

在下面的示例中，我们有三个由段落创建的内联框，其中包含一个强元素。

```html live-sample___inline
<p>
  Before that night—<strong>a memorable night</strong>, as it was to
  prove—hundreds of millions of people had watched the rising smoke-wreaths of
  their fires without drawing any special inspiration from the fact.
</p>
```

{{EmbedLiveSample("inline")}}

在强元素前和强元素后的单词周围的框称为匿名框，引入的框确保所有内容都包装在一个框中，但我们不能直接针对它们。

块方向上的线框大小（以英文工作时的高度为准）由其内部最高的框定义。在下一个示例中，我将强元素 300% 设为内容，该内容现在定义了该行上行框的高度。

```html live-sample___line-box
<p>
  Before that night—<strong>a memorable night</strong>, as it was to
  prove—hundreds of millions of people had watched the rising smoke-wreaths of
  their fires without drawing any special inspiration from the fact.
</p>
```

```css live-sample___line-box
strong {
  font-size: 300%;
}
```

{{EmbedLiveSample("line-box")}}

在我们的视觉格式模型指南中，了解更多关于块和内联框的行为。

## 显示属性和流布局

除了 CSS2.1 中现有的规则之外，新级别的 CSS 还进一步描述了块和内联框的行为。“显示”属性定义框及其内部的所有框的行为方式。在 CSS 显示模型级别 3 中，我们可以进一步了解显示属性如何更改框及其生成的框的行为。

一个元素的显示类型定义了外部显示类型，这规定了该框如何与同一格式上下文中的其他元素一起显示。它还定义了内部显示类型，该类型指示此元素内的框的行为方式。在考虑灵活布局时，我们可以很清楚地看到这一点。在下面的示例中，我有一个 DIV，我已经给出了 display:flex。flex 容器的行为类似于一个块元素，它显示在一条新行上，并占用它在内联方向上可以占用的所有空间。这是块的外部显示类型。

但是，flex 项正在参与 flex 格式上下文，因为它们的父级是带有 display:flex 的元素，后者具有 flex 的内部显示类型，为直接子级建立 flex 格式上下文。

```html live-sample___flex
<div class="container">
  <div>Flex Item</div>
  <div>Flex Item</div>
  <div>
    <div>Children</div>
    <div>are in</div>
    <div>normal flow</div>
  </div>
</div>
```

```css live-sample___flex
.container {
  display: flex;
}

.container > * {
  border: 1px solid green;
}
```

{{EmbedLiveSample("flex")}}

因此，你可以想到 CSS 中的每个框都是以这种方式工作的。盒子本身有一个外部显示类型，所以它知道如何与其他盒子一起工作。然后它有一个内部显示类型，它改变了它的子对象的行为方式。然后，这些子级也有一个外部和内部显示类型。上一个示例中的 flex 项变为 flex 级别框，因此它们的外部显示类型取决于它们是 flex 格式上下文的一部分。然而，他们有一种内在的流动显示类型，这意味着他们的孩子参与正常的流动。嵌套在 flex 项中的项将自己设置为块和内联元素，除非有什么改变了它们的显示类型。

外部和内部显示类型的概念很重要，因为这告诉我们，由于这些方法的外部显示类型为块，因此使用 flexbox（display:flex）和 grid layout（display:grid）等布局方法的容器仍在参与块和内联布局。

### 更改元素参与的格式上下文

浏览器将项目显示为块或内联格式上下文的一部分，根据该元素通常的意义。例如，强元素用于突出显示单词，并在浏览器中显示粗体。一般来说，将该强元素显示为块级元素并中断到新行是没有意义的。如果确实希望所有强元素显示为块元素，可以通过将 display:block 设置为强来实现。这意味着你可以始终使用最语义的 HTML 元素标记内容，然后使用 CSS 更改其显示方式。

```html live-sample___change-formatting
<p>
  Before that night—<strong>a memorable night</strong>, as it was to
  prove—hundreds of millions of people had watched the rising smoke-wreaths of
  their fires without drawing any special inspiration from the fact.
</p>
```

```css live-sample___change-formatting
strong {
  display: block;
}
```

{{EmbedLiveSample("change-formatting")}}

## 总结

在本指南中，我们研究了元素在正常流中如何显示为块和内联元素。由于这些元素的默认行为，一个完全没有 CSS 样式的 HTML 文档将以可读的方式显示。通过了解正常流的工作方式，你将更容易找到布局，因为你了解更改元素显示方式的起点。

## 参见

- [CSS Basic Box Model](/zh-CN/docs/Web/CSS/CSS_box_model)
- _[Normal Flow](/zh-CN/docs/Learn_web_development/Core/CSS_layout/Introduction)_ - Learn Layout
- [Inline elements](/zh-CN/docs/Glossary/Inline-level_content)
- [Block-level elements](/zh-CN/docs/Glossary/Block-level_content)
