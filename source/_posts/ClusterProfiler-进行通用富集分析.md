---
title: ClusterProfiler 进行通用富集分析
date: 2021-03-11 16:09:35
tags: Universal Enrichment Analysis
---

  这两天一直帮师妹做富集分析。因为茶树是非模式物种，所以没有自己orgdb包。虽然自己能够构建物种包，但是就只是做个富集分析，所以就使用ClusterProfiler的通用富集分析enricher函数，进行富集分析。

```R
ego <- enricher(gene_list, 
                TERM2GENE = go2gene, 
                TERM2NAME = go2name, 
                pvalueCutoff = 0.05, 
                qvalueCutoff = 0.05,
                pAdjustMethod = "fdr",
                minGSSize = 10)
```



核心点是 自己准备TERM2GENE 和   TERM2NAME 文件

TERM2GENE

|   Term    |   Gene    |
| :-------: | :-------: |
| GO:000001 | TEA000001 |
| GO:000002 | TEA000002 |

TERM2NAME

|   Term    |      NAME       |
| :-------: | :-------------: |
| GO:000001 | Amine Transport |
| GO:000002 |  Amino Absorb   |

里面的意思是我随手写的，但是所有文件都可以自己从TPIA文件整理数据获得。

KO富集分析同理

