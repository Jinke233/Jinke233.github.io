---
title: matplotlib 学习
date: 2020-10-19 21:16:06
tags: matplotlib 指引
---

 使用 Matplotlib 提供的面向对象 API，需要导入 `pyplot` 模块，并约定简称为 `plt`。

```python
from matplotlib import pyplot as plt
```

`pyplot` 模块中 `pyplot.plot` 方法是用来绘制折线图的。你应该会很容易联想到，更改后面的方法类名就可以更改图形的样式。的确，在 Matplotlib 中，大部分图形样式的绘制方法都存在于 `pyplot` 模块中。例如：



| 方法                               | 含义           |
| ---------------------------------- | -------------- |
| `matplotlib.pyplot.angle_spectrum` | 绘制电子波谱图 |
| `matplotlib.pyplot.bar`            | 绘制柱状图     |
| `matplotlib.pyplot.barh`           | 绘制直方图     |
| `matplotlib.pyplot.broken_barh`    | 绘制水平直方图 |
| `matplotlib.pyplot.contour`        | 绘制等高线图   |
| `matplotlib.pyplot.errorbar`       | 绘制误差线     |
| `matplotlib.pyplot.hexbin`         | 绘制六边形图案 |
| `matplotlib.pyplot.hist`           | 绘制柱形图     |
| `matplotlib.pyplot.hist2d`         | 绘制水平柱状图 |
| `matplotlib.pyplot.pie`            | 绘制饼状图     |
| `matplotlib.pyplot.quiver`         | 绘制量场图     |
| `matplotlib.pyplot.scatter`        | 散点图         |
| `matplotlib.pyplot.specgram`       | 绘制光谱图     |



`matplotlib.pyplot.plot(*args, **kwargs)` 方法严格来讲可以绘制线形图或者样本标记。其中，`*args` 允许输入单个 *𝑦* 值或 *𝑥*,*𝑦* 值

