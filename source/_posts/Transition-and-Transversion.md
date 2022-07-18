---
title: Transition and Transversion
date: 2020-10-07 22:26:59
tags: Rosalind 点突变 转换和颠换
---

```python
# A transition substitutes one purine for another (A↔G) or one pyrimidine for another (C↔T);
# a transversion is the interchange of a purine for a pyrimidine base, or vice-versa

# 思路计算转换和颠换次数
# 难点在于排除碱基相等的情况

seq_list = []
stseq = ''
for line in open('rosalind_tran.txt'):
    if line[0] == '>':
        if stseq != '':
            # 把 stseq 添加到 seq_list里
            seq_list.append(stseq)
            stseq = ''
        else:
            continue
    else:
        # 生成stseq
        stseq = stseq + line.strip('\n')
# 这一段的代码的核心是在这最后一行
seq_list.append(stseq)

seq_1 = seq_list[0]
seq_2 = seq_list[1]

total = len(seq_1)

transition = 0
transvertion = 0
for i in range(total):
    print(seq_1[i], seq_2[i] )
    if seq_1[i] in "AG" and seq_2[i] in "AG" and seq_1[i] != seq_2[i]:
        transition = transition + 1
    elif seq_1[i] in "CT" and seq_2[i] in "CT" and seq_1[i] != seq_2[i]:
        transition = transition + 1
    elif seq_1[i] != seq_2[i]:
        transvertion = transvertion + 1
print(transition/transvertion, total)

```

