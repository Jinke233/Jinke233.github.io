---
title: FPKM TPM 再探
date: 2021-04-07 15:53:03
tags: FPKM TPM
---

 今天遇到一个问题， 有人问我FPKM什么意思？我没口述出来。
FPKM 全称是 Fragments per kilobase per Million. 
这里的 kilobase是指 外显子长度的单位。
Million是指 reads 个数的单位。
每1kbp的外显子长度对应多少百万reads个数。

FPKM和TPM的最主要区别在于对测序深度的标准化不同。
他们俩对于基因长度的标准化处理是一致的，但是
FPKM对测序深度直接除以总reads数目,TPM除以的是基因长度归一化之后的 reads数目。
这两点有什么不一致吗？

这里首先需要回答为什么需要FPKM和TPM的统计量？
因为我们想知道某一个基因的表达量在整个样本中的比例。
但是FPKM既然已经对基因长度归一化之后，可以理解为知道每个基因已经有多少转录本了，这时候应该除以总转录本数目了。

但是N/10^6是由测序深度决定，和总转录本数量无线性关系。所以TPM更准确。

