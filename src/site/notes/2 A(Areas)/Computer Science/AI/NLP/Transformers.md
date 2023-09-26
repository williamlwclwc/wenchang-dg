---
{"dg-publish":true,"permalink":"/2-a-areas/computer-science/ai/nlp/transformers/","tags":["AI/NLP/LLM"],"noteIcon":"1"}
---


## Overview

Transformer最早提出自[[3 R(Resources)/Research-Papers/vaswaniAttentionAllYou2017\|Attention Is All You Need]]这篇论文，是一种完全基于[[2 A(Areas)/Computer Science/AI/NLP/Attention\|Attention]]的模型结构，在此之前Attention通常和RNN一起使用。

Transformers是后续大模型的骨架，[[2 A(Areas)/Computer Science/AI/NLP/BERT\|BERT]]、[[2 A(Areas)/Computer Science/AI/NLP/GPT\|GPT]]底层都是Transformer。

* 参考资料: 
	* [Shusen Wang's YouTube Video](https://www.youtube.com/watch?v=aJRsr39F4dI&list=PLvOO0btloRntpSWSxFbwPIjIum3Ub4GSC&index=2)
	- [Slides](https://github.com/wangshusen/DeepLearning/tree/master)
	- [Paper Arxiv Link](http://arxiv.org/abs/1706.03762)

## Architecture

### Attention without RNN

* Attention的输入有两个部分
	* Encoder的输入 vectors $x_1, x_2, ..., x_m$
	* Decoder的输入 vectors $x_1^{'}, x_2^{'}, ..., x_t^{'}$
	* **K(Keys), Values(V)**: 基于Encoder的输入，通过两个学习到的Weight $W_K$、$W_V$将$x_i$投影到$k_i = W_K x_i$和$v_i = W_V x_i$ 这样每个$x_i$就可以得到一个$k_i$和一个$v_i$
	* **Q(Query)**: 基于Decoder的输入，也是通过学习到的Weight $W_q$将$x_j^{'}$投影到$q_j = W_q x_j^{'}$ 这样每个$x_i^{'}$就可以得到一个$q_j$
* 之后的计算部分，需要计算一个基于k和q相似度的attention score $\alpha$ 和 基于attention score $\alpha$ 和 v的context c。如果作为输出的话，可以再将c通过一个[[2 A(Areas)/Computer Science/AI/ML and DL Basics/Softmax\|Softmax]]得到最后的输出token。
	* 计算attention score ${\alpha}_i = Softmax(K^{T}q_i)$ 这里的$K^T$ 就是所有$k_i$组成的矩阵，也就是说每个attention score都包含了所有encoder的信息和对应q的信息。
		* ![compute-attn-score](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/compute-attn-score.png)
	* 计算context vector $c_i = V \alpha_i$ 这里的V就是所有$v_i$组成的矩阵，也就是说每个context vector包含了所有encoder的信息和对应attention的信息。
		* ![compute-context-vec](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/compute-context-vec.png)
	* 比如在机器翻译的任务中，我们每次拿一个q和encoder的所有k、v一起生成一个c，然后用c得到输出token，然后再拿新生成的token得到新的decoder的输入
		* ![attn-for-MT](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/atten-for-MT.png)
* 合在一起看就是Attention Layer，整个Attention Layer就是通过encoder和decoder的输入$x_1, x_2, ..., x_m$和$x_1^{'}, x_2^{'}, ..., x_t^{'}$，逐一计算context vector $c_i$ 最后得到整个输出$C=[c_1, ..., c_t]$
	* ![attn-layer](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/attn-layer.png)

### Self-Attention

* Self-Attention是什么呢？
	* 其实就是没有decoder输入的Attention。
	* 之前q是通过decoder输入得到的，现在q也通过encoder输入来得到，也就是说，每个$x_i$我们通过三个Weight $W_Q, W_K, W_V$分别得到$q_i=W_Q x_i, k_i=W_k x_i, v_i=W_V x_i$
	* 有了q、k、v之后，后面计算attention和context就和Attention Layer一样了
	* ![](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/self-attn-layer.png)

### Multi-Head Attention

* 将 $h$ 个single-head Attention组合在一起(不share Weight参数)
* 然后讲这些single-head Attention的输出做concatenation，比如single-head的输出是一个$d\times m$的矩阵，那么multi-head的输出就成了$(hd)\times m$的矩阵
* 这样的Multi-Head Attention就是论文 [[3 R(Resources)/Research-Papers/vaswaniAttentionAllYou2017\|Attention Is All You Need]] 中的图了
	* ![DLD922ZR](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/DLD922ZR-Attn-Fig.png)
	* Scale这里是将Q、K的点积除以$\sqrt{d_k}$, $d_k$ 指的是Q、K的dimension数量。
		* $Attention(Q, K, V) = softmax(\frac{QK^T}{\sqrt{d_k}})V$
	* Mask: decoder中计算`i`位置的attention score和context的时候不让attend `i`之前的位置

### Transformer Encoder-Decoder Architecture

* ![ID8JQSZ7](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/ID8JQSZ7-TF-Arch.png)
* Encoder Block: 叠加Self-Attention Layers，从图中我们可以看到每个encoder的block由一个Multi-Head Self-Attention和一个Feed Forward(也就是Dense、全连接层)，Attention和Feed Forward都接了一个LayerNorm: $LayerNorm(x+subLayer(x))$ subLayer可以是Multi-Head Attention也可以是Feed Forward。
	* ![](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/TF-Encoder.png)
* Decoder Block: 叠加Attention Layers，从图中看到上半部分和encoder相似，一个Multi-Head Attention和一个Feed Forward，不过k、v来自于encoder的输出，而q则来自于下面一个Masked Multi-Head Self-Attention的输出。
	* ![](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/TF-Decoder.png)
	* 整个encoder-decoder的粗略示意图如下:
		* ![](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/encoder-decoder.png)

## Positional Encoding

* 由于没有了CNN和RNN，我们只是参考了输入每个token的attention权重，但是没有了sequence信息，所以本文加上了position encoding，其方式就是对每个输入token都加上一个相同dimension的embedding $d_{model}$ (dim相同，直接做向量加法)
* 生成position encoding的方式有很多种，本文使用的是三角函数生成，也可以直接学习一个模型
- ![2XSVB2HC](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/2XSVB2HC-position-encoding.png)
## Example on MT

* ![](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/MT-Example.png)
* Encoder部分，输入输出长度对应，m个词输入，编码成m维词向量X，输出依然是相同shape的U，然后decoder从start sign开始，用U和start sign生成y1，y1生成第一个词，然后第一个词输入进decoder得到y2...直到生成出stop sign。

