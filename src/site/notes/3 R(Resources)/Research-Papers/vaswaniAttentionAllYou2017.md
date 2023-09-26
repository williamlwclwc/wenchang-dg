---
{"dg-publish":true,"permalink":"/3-r-resources/research-papers/vaswani-attention-all-you2017/","tags":["Preprint"],"noteIcon":"1"}
---


## Attention Is All You Need

URL: http://arxiv.org/abs/1706.03762
Zotero Link: [arXiv Fulltext PDF](zotero://select/library/items/L8BZ5H6M)


Topics: [[2 A(Areas)/Computer Science/AI/NLP/NLP\|NLP]], [[2 A(Areas)/Computer Science/AI/NLP/Transformers\|Transformers]], [[2 A(Areas)/Computer Science/AI/NLP/LLM\|LLM]], [[2 A(Areas)/Computer Science/AI/NLP/Attention\|Attention]]





### Formatted Bibliography

Vaswani, Ashish, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Lukasz Kaiser, and Illia Polosukhin. “Attention Is All You Need.” arXiv, December 5, 2017. [https://doi.org/10.48550/arXiv.1706.03762](https://doi.org/10.48550/arXiv.1706.03762).





### Abstract

The dominant sequence transduction models are based on complex recurrent or convolutional neural networks in an encoder-decoder configuration. The best performing models also connect the encoder and decoder through an attention mechanism. We propose a new simple network architecture, the Transformer, based solely on attention mechanisms, dispensing with recurrence and convolutions entirely. Experiments on two machine translation tasks show these models to be superior in quality while being more parallelizable and requiring significantly less time to train. Our model achieves 28.4 BLEU on the WMT 2014 English-to-German translation task, improving over the existing best results, including ensembles by over 2 BLEU. On the WMT 2014 English-to-French translation task, our model establishes a new single-model state-of-the-art BLEU score of 41.8 after training for 3.5 days on eight GPUs, a small fraction of the training costs of the best models from the literature. We show that the Transformer generalizes well to other tasks by applying it successfully to English constituency parsing both with large and limited training data.




### Notes


#### Pass 1 略读

##### Q1 简单总结论文想要干嘛？

提出Transformer结构，全部基于Attention，不需要RNN和CNN

##### Q2 这是否是新领域？如何归类？之前的研究有什么不足？

不是新领域，之前有过相关工作。但是RNN无法高效并行，处理长句子尤其明显。之前的Attention也不能脱离RNN单独工作。

#### Pass 2 全面了解

##### Q3 论文提出的解决方案的关键点都是？

* Encoder-Decoder结构
* Attention Block
* Self-Attention
* Multihead Attention
* Position Encoding

##### Q4 论文想要验证的假设是？

只使用Attention的Transformer结构可以更好地并行训练以及在NLP的任务(e.g. 机器翻译)中取得更好的效果

##### Q5 论文的实验和结果有没有很好地支持要验证的假设？

有，并行和效果都有提高。

#### Pass 3 精读

##### Q6 论文的方案具体是怎么做的？能否用一个例子过一遍整个pipeline？

##### Q7 论文的实验是如何设计的？

* 通过比较在机器翻译的数据集上的表现，和之前的SOTA模型比较[[2 A(Areas)/Computer Science/AI/NLP/BLEU Score\|BLEU Score]]和Training Cost([[2 A(Areas)/Computer Science/AI/ML and DL Basics/FLOPs\|FLOPs]])
* 也测试了不同hyperparameters的表现，比较了[[2 A(Areas)/Computer Science/AI/NLP/PPL\|PPL]]和[[2 A(Areas)/Computer Science/AI/NLP/BLEU Score\|BLEU Score]]
* 同时测试了在English Constituency Parsing的表现来证明可以适用于其他NLP任务

##### Q8 论文的核心贡献到底是什么？

* 全新的Transformer结构，可以用于各种NLP任务，并行度高，效果好
* 全部基于Attention，不再需要CNN和RNN

#### (Optional) 研究领域相关工作调研

##### Q9 下一步能做什么？

将Transformer结构用于各种任务、预训练语言模型

##### Q10 有哪些相关的研究需要关注？

本文提出Transformer是后续著名[[2 A(Areas)/Computer Science/AI/NLP/LLM\|LLM]]例如[[2 A(Areas)/Computer Science/AI/NLP/BERT\|BERT]]、[[2 A(Areas)/Computer Science/AI/NLP/GPT\|GPT]]等的鼻祖。

##### Q11 使用了什么数据集/工具/评估方法？代码是否开源可复现？

使用了一些机器翻译的数据集进行测试，代码开源，目前热门的实现是HuggingFace Transformers

#### 其他评价

NLP大模型时代的奠基作，必读。




### Highlights




<span style="background-color: #ffd400"> The dominant sequence transduction models are based on complex recurrent or convolutional neural networks that include an encoder and a decoder. The best performing models also connect the encoder and decoder through an attention mechanism. </span> ([Page 1](zotero://open-pdf/library/items/L8BZ5H6M?page=1&annotation=3X465HUU))
		 总结之前处理序列的主流工作: CNN或RNN+encoder-decoder结构，最新的工作还加上了Attention的机理 
	
<span style="background-color: #5fb236"> We propose a new simple network architecture, the Transformer, based solely on attention mechanisms, dispensing with recurrence and convolutions entirely. </span> ([Page 1](zotero://open-pdf/library/items/L8BZ5H6M?page=1&annotation=UAKKEEVC))
		 本文的工作: 提出了Transformer结构，全部依靠Attention，不需要CNN和RNN 
	
<span style="background-color: #5fb236"> Experiments on two machine translation tasks show these models to be superior in quality while being more parallelizable and requiring significantly less time to train. </span> ([Page 1](zotero://open-pdf/library/items/L8BZ5H6M?page=1&annotation=4N8ZKGS8))
		 实验结构表明，效果好且好训练 
	
<span style="background-color: #5fb236"> We show that the Transformer generalizes well to other tasks by applying it successfully to English constituency parsing both with large and limited training data. </span> ([Page 1](zotero://open-pdf/library/items/L8BZ5H6M?page=1&annotation=JAZHCIII))
		 也可以应用到其他相关任务 
	
<span style="background-color: #ff6666"> This inherently sequential nature precludes parallelization within training examples, which becomes critical at longer sequence lengths, as memory constraints limit batching across examples. </span> ([Page 2](zotero://open-pdf/library/items/L8BZ5H6M?page=2&annotation=BKW4D2ZA))
		 RNN的缺陷，无法并行处理训练数据，在处理长句子时尤其明显 
	
<span style="background-color: #ff6666"> In all but a few cases [27], however, such attention mechanisms are used in conjunction with a recurrent network. </span> ([Page 2](zotero://open-pdf/library/items/L8BZ5H6M?page=2&annotation=2L8KKYR7))
		 之前的工作里Attention都和RNN一起 
	
<span style="background-color: #ffd400"> The goal of reducing sequential computation </span> ([Page 2](zotero://open-pdf/library/items/L8BZ5H6M?page=2&annotation=635D3WSU))
		
	
<span style="background-color: #ffd400"> all of which use convolutional neural networks as basic building block, computing hidden representations in parallel for all input and output positions. </span> ([Page 2](zotero://open-pdf/library/items/L8BZ5H6M?page=2&annotation=IQH77H34))
		
	
<span style="background-color: #ff6666"> In these models, the number of operations required to relate signals from two arbitrary input or output positions grows in the distance between positions, linearly for ConvS2S and logarithmically for ByteNet. This makes it more difficult to learn dependencies between distant positions [12]. </span> ([Page 2](zotero://open-pdf/library/items/L8BZ5H6M?page=2&annotation=UXXT3L4I))
		 前作尝试并行处理hidden representation计算，但是计算距离远的两个位置需要更多训练资源。Transformer通过多头注意力来解决这个问题 
	
<span style="background-color: #ffd400"> an encoder-decoder structure [5, 2, 35]. Here, the encoder maps an input sequence of symbol representations (x1, ..., xn) to a sequence of continuous representations z = (z1, ..., zn). Given z, the decoder then generates an output sequence (y1, ..., ym) of symbols one element at a time. At each step the model is auto-regressive [10], consuming the previously generated symbols as additional input when generating the next. </span> ([Page 2](zotero://open-pdf/library/items/L8BZ5H6M?page=2&annotation=M2GUJXPE))
		 介绍encoder-decoder结构 
	
<span style="background-color: #ffd400"> using stacked self-attention and point-wise, fully connected layers for both the encoder and decoder, </span> ([Page 2](zotero://open-pdf/library/items/L8BZ5H6M?page=2&annotation=BTSANEFC))
		 简单来说Transformer就是self-attention+全连接 
	
![ID8JQSZ7](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/ID8JQSZ7-TF-Arch.png) Transformer经典结构图 
<span style="background-color: #5fb236"> The first is a multi-head self-attention mechanism, and the second is a simple, positionwise fully connected feed-forward network. We employ a residual connection [11] around each of the two sub-layers, followed by layer normalization [1]. </span> ([Page 3](zotero://open-pdf/library/items/L8BZ5H6M?page=3&annotation=9AXREX2R))
		 encoder有6个block，每个block有两层，第一层是多头自注意力，第二层是全连接feed-forward(MLP)，每层都用残差连接一个layer norm 
	
<span style="background-color: #ffd400"> That is, the output of each sub-layer is LayerNorm(x + Sublayer(x)), where Sublayer(x) is the function implemented by the sub-layer itself. </span> ([Page 3](zotero://open-pdf/library/items/L8BZ5H6M?page=3&annotation=LBBAKBM5))
		
	
<span style="background-color: #ffd400"> produce outputs of dimension dmodel = 512. </span> ([Page 3](zotero://open-pdf/library/items/L8BZ5H6M?page=3&annotation=ZVT7D39Y))
		
	
<span style="background-color: #5fb236"> In addition to the two sub-layers in each encoder layer, the decoder inserts a third sub-layer, which performs multi-head attention over the output of the encoder stack. </span> ([Page 3](zotero://open-pdf/library/items/L8BZ5H6M?page=3&annotation=3M57S8TS))
		 decoder也是6个block，每个block在encoder的基础上多加了一个多头注意力来结合encoder传来的输入和output已经产生的输出作为新的输入。同时对output部分的attention加了mask处理 
	
<span style="background-color: #ffd400"> We also modify the self-attention sub-layer in the decoder stack to prevent positions from attending to subsequent positions. This masking, combined with fact that the output embeddings are offset by one position, ensures that the predictions for position i can depend only on the known outputs at positions less than i. </span> ([Page 3](zotero://open-pdf/library/items/L8BZ5H6M?page=3&annotation=YXWGC2BU))
		 i位置只能attendi之前的位置 
	
<span style="background-color: #ffd400"> An attention function can be described as mapping a query and a set of key-value pairs to an output, where the query, keys, values, and output are all vectors. The output is computed as a weighted sum of the values, where the weight assigned to each value is computed by a compatibility function of the query with the corresponding key. </span> ([Page 3](zotero://open-pdf/library/items/L8BZ5H6M?page=3&annotation=QF9JAXUL))
		 Attention是将q、k、v输入得到一个加权和作为输出。权重从q和k计算得到。 
	
![DLD922ZR](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/DLD922ZR-Attn-Fig.png)
<span style="background-color: #ffd400"> The input consists of queries and keys of dimension dk, and values of dimension dv. We compute the dot products of the query with all keys, divide each by √dk </span> ([Page 4](zotero://open-pdf/library/items/L8BZ5H6M?page=4&annotation=JB9TD34Q))
		 scale by sqrt(dk) 
	
![CJGF99FX](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/CJGF99FX-Attn.png)
<span style="background-color: #5fb236"> dot-product attention is much faster and more space-efficient in practice, since it can be implemented using highly optimized matrix multiplication code. </span> ([Page 4](zotero://open-pdf/library/items/L8BZ5H6M?page=4&annotation=CWBEY3KK))
		
	
<span style="background-color: #ffd400"> we found it beneficial to linearly project the queries, keys and values h times with different, learned linear projections to dk, dk and dv dimensions, respectively. </span> ([Page 4](zotero://open-pdf/library/items/L8BZ5H6M?page=4&annotation=WB4VJCS6))
		 每个qkv都投影出dimension个qkv，然后并行进行多头attention，把输出再拼起来得到dv维的向量的输出 
	
![SMP8IERT](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/SMP8IERT-MultiHead-Attn.png)
<span style="background-color: #ffd400"> In this work we employ h = 8 parallel attention layers, or heads. For each of these we use dk = dv = dmodel/h = 64. </span> ([Page 5](zotero://open-pdf/library/items/L8BZ5H6M?page=5&annotation=VGZZRRWY))
		
	
![RCVL96GX](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/RCVL96GX-FFN.png)
<span style="background-color: #ffd400"> The dimensionality of input and output is dmodel = 512, and the inner-layer has dimensionality dff = 2048. </span> ([Page 5](zotero://open-pdf/library/items/L8BZ5H6M?page=5&annotation=VM54J5MA))
		
	
<span style="background-color: #5fb236"> we use learned embeddings to convert the input tokens and output tokens to vectors of dimension dmodel. We also use the usual learned linear transformation and softmax function to convert the decoder output to predicted next-token probabilities </span> ([Page 5](zotero://open-pdf/library/items/L8BZ5H6M?page=5&annotation=ZUBZ4FHE))
		
	
<span style="background-color: #5fb236"> The positional encodings have the same dimension dmodel as the embeddings, so that the two can be summed. There are many choices of positional encodings, learned and fixed </span> ([Page 6](zotero://open-pdf/library/items/L8BZ5H6M?page=6&annotation=MQM64PEN))
		
	
![2XSVB2HC](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/2XSVB2HC-position-encoding.png)
<span style="background-color: #5fb236"> We also experimented with using learned positional embeddings [9] instead, and found that the two versions produced nearly identical results </span> ([Page 6](zotero://open-pdf/library/items/L8BZ5H6M?page=6&annotation=NJ8UA88B))
		
	
<span style="background-color: #ffd400"> In terms of computational complexity, self-attention layers are faster than recurrent layers when the sequence length n is smaller than the representation dimensionality d, which is most often the case with sentence representations used by state-of-the-art models in machine translations, such as word-piece [38] and byte-pair [31] representations. </span> ([Page 6](zotero://open-pdf/library/items/L8BZ5H6M?page=6&annotation=8SLIAMMS))
		
	
<span style="background-color: #5fb236"> In this work, we presented the Transformer, the first sequence transduction model based entirely on attention, replacing the recurrent layers most commonly used in encoder-decoder architectures with multi-headed self-attention. </span> ([Page 10](zotero://open-pdf/library/items/L8BZ5H6M?page=10&annotation=JMTXNFLC))
		 一句话总结本文贡献 
	






