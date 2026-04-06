---
layout: post
title: 贝叶斯公式：从思想到应用 (Codex测试博客)
date: 2025-08-30 09:00:00 +0800
description: 追溯贝叶斯思想的由来，与频率学派对比，诠释贝叶斯公式的含义与计算，并展示典型应用及与其他领域的连接
tags: bayes probability statistics inference machine-learning
categories: statistics
related_posts: false
---

贝叶斯公式看似简单，却提供了在不确定性下学习与决策的一套统一范式：用先验表达信念，用似然描述数据如何产生，用后验整合二者并给出不确定性量化。

## 思想的由来

- 托马斯·贝叶斯与拉普拉斯奠定了“逆概率”的思想：由结果反推原因。
- 之后频率学派强调“长程频率”与重复抽样性质，追求无先验的客观程序。
- 现代贝叶斯在计算工具（MCMC、变分推断）与建模语言的支持下，已能处理高维复杂问题。

## 频率学派 vs 贝叶斯学派（要点）

- 概率含义：频率学派视为长期频率；贝叶斯视为合理信念度。
- 参数本质：频率学派中参数固定未知；贝叶斯中参数具随机性，赋予先验。
- 推断对象：频率学派给点估计、置信区间、显著性检验；贝叶斯给后验分布、置信（可信）区间与后验预测。

## 公式及其形态

以参数 \(\theta\) 与数据 \(D\) 为例：

$$
p(\theta\mid D) = \frac{p(D\mid \theta)\,p(\theta)}{p(D)} \propto p(D\mid \theta)\,p(\theta).
$$

分母 \(p(D)\) 为证据（边际似然）：

\begin{equation}
\label{eq:evidence}
p(D) = \int p(D\mid \theta)\,p(\theta)\,d\theta.
\end{equation}

在二分类检验中，常用“胜算”形式：

$$
\frac{p(H\mid E)}{p(H^c\mid E)} = \underbrace{\frac{p(E\mid H)}{p(E\mid H^c)}}_{\text{贝叶斯因子}} \cdot \frac{p(H)}{p(H^c)}.
$$

诠释小结：

- “后验 ∝ 似然 × 先验”：数据在先验基础上修正信念。
- 证据衡量模型对数据的整体解释力，并对复杂模型施加惩罚。
- 先验等价于正则化：高斯先验≈L2，拉普拉斯先验≈L1；先验平坦时，MAP 逼近 MLE。

## 共轭示例

1）Beta–二项（硬币正面率）。先验 \(\theta\sim \mathrm{Beta}(\alpha,\beta)\)，观测 n 次中 k 次为正面：

$$
\theta\mid D \sim \mathrm{Beta}(\alpha+k,\,\beta+n-k),\quad 
\mathbb E[\theta\mid D]=\frac{\alpha+k}{\alpha+\beta+n}.
$$

2）高斯–高斯（均值未知，方差已知）。先验 \(\mu\sim\mathcal N(\mu_0,\tau_0^2)\)，数据 \(x_i\stackrel{iid}{\sim}\mathcal N(\mu,\sigma^2)\)：

\begin{equation}
\label{eq:gauss}
\mu\mid D\;\sim\;\mathcal N\!\left(\frac{\frac{\mu_0}{\tau_0^2}+\frac{n\bar x}{\sigma^2}}{\frac{1}{\tau_0^2}+\frac{n}{\sigma^2}},\;\;\frac{1}{\frac{1}{\tau_0^2}+\frac{n}{\sigma^2}}\right).
\end{equation}

## 实务中的计算

- 解析：依赖共轭结构与小规模模型。
- 近似：拉普拉斯近似、期望传播等。
- 采样：MCMC（MH、HMC/NUTS）适用于一般后验。
- 优化：变分推断把推断转化为 ELBO 最大化。

## 典型应用

- A/B 测试：用 Beta–二项后验比较转化率，置信则决策。
- 医学诊断：用似然比（贝叶斯因子）更新疾病胜算。
- 垃圾邮件过滤：朴素贝叶斯按词项似然组合打分。
- 推荐系统：层级贝叶斯在用户/物品间共享统计强度。
- 跟踪与控制：卡尔曼滤波是线性–高斯贝叶斯的在线实现。
- 贝叶斯优化：在高代价实验中用 GP 后验与采集函数选择下一步。

## 与其他领域的连接

- 信息论：证据可分解为拟合与复杂度，MDL 与贝叶斯密切相关。
- 机器学习：先验=正则化；贝叶斯神经网络量化不确定性；dropout 可视为近似贝叶斯集成。
- 因果推断：把结构性知识作为先验编码到图或效应上。
- 决策理论：在后验下最小化期望损失，形成一致的决策准则。
- 金融与风险：动态更新收益与波动率的信念分布。

## 小结

- 贝叶斯公式提供了统一的“从数据中学习”的范式。
- 先验表达约束与结构，后验刻画不确定性并驱动决策。
- 证据用于模型比较与自动平衡复杂度。

作为参考，式 \eqref{eq:evidence} 源自全概率公式：

$$
p(D) = \int p(D,\theta)\,d\theta = \int p(D\mid\theta)\,p(\theta)\,d\theta.
$$

