---
title: Orthofinder
date: 2021-04-07 16:53:18
tags: Orthofinder OrthoMCL
---

Orthofinder的建树方法是 super tree做的, 根据 STAG算法。

Otrhofinder和 OrthoMCL的异同？

  OrthoMCL uses BLAST to compute sequence similarity scores between sequences in multiple species and then uses the MCL xlustering algorithm to identify highly-connected clusters (groups of highly similar sequences) within this dataset.

1. 在BLAST层面 Orthofinder 克服 基因长度偏差
2. 后续的鉴定仍然是延续 reciprocal nest (normalized) hit.







如何查找一段插入序列？

外源片段插入位置，可以通过 WGS 查看bam 格式利用IGV可视化。

或者使用载体标记序列,进行 BLAST。