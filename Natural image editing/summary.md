### Null-Text inversion

| 模型简称 | 论文全称 | 作用域 | 发表时间 | 期刊/Arxiv | 方法类型 | 方法细分 |
| --- | --- | --- | --- | --- | --- | --- |
| Null-Text inversion | Null-text Inversion for Editing Real Images using Guided Diffusion Models | real | 2023 | CVPR | train-testing free | Inversion/SampleModification |

主要动机：目前基于classifier-free的IE受无条件预测影响大，因而试图改进null-text embedding。

主要创新点：（w=1）DDIM inversion as pivot，（w>1）pivotal tuning，optimize the null text embedding。

缺点：推理速度太慢，使用SD带来的编辑人脸图像时会出现伪影，和不能进行大幅度修改的问题。

说明：进行DDIM反演时，w=1,只采用条件DFM。

---

### Prompt2Prompt

| 模型简称 | 论文全称 | 作用域 | 发表时间 | 期刊/Arxiv | 方法类型 | 方法细分 |
| --- | --- | --- | --- | --- | --- | --- |
| Prompt2Prompt | Prompt-to-Prompt Image Editing with Cross Attention Control | synthesis | 2022 | Arxiv | train-testing free | AttentionModification |

主要动机：目前的text-based models在IE方面受到挑战，对于text prompt的微小改动会导致生成的图像差别很大；由此观察到crossAttention map决定图像的空间布局和形状，因此尝试控制它来进行图像编辑。

主要创新点：对不同任务进行不同的crossAttentionMap的控制（swap word/refinement/reweighing）。

缺点：使用SD带来的编辑人脸图像时会出现伪影，和不能进行大幅度修改的问题。

说明：进行DDIM反演时，w=1,只采用条件DFM。

---

### PRedItOR

| 模型简称 | 论文全称 | 作用域 | 发表时间 | 期刊/Arxiv | 方法类型 | 方法细分 |
| --- | --- | --- | --- | --- | --- | --- |
| PRedItOR | PRedItOR: Text Guided Image Editing with Diffusion Prior | real&synthesis | 2023 | Arxiv | train-testing free | Input-Text refinement |

主要动机：text-baesd扩散模型图像编辑的主要挑战是要给input找到对应的prompt，当前方法主要通过优化的方法得到精确的prompt，或者假定存在最优prompt，因此我们不使用source prompt。

主要创新点：PRedItOR的Diffusion Prior和Diffusion Decoder采样都是从蕴含语义或者结构先验信息的向量开始，而不是高斯噪声开始。

缺点：不能编辑人脸图像，不能编辑训练数据中未见过的label。

说明：与InstructEdit相同的是在反演时都不是反演到T，而是在某个中间步。

---

### Captioning and Injection

| 模型简称 | 论文全称 | 作用域 | 发表时间 | 期刊/Arxiv | 方法类型 | 方法细分 |
| --- | --- | --- | --- | --- | --- | --- |
| Captioning and Injection | User-friendly Image Editing with Minimal Text Input：Leveraging Captioning and Injection Techniques | real&synthesis | 2023 | Arxiv | train-testing free | Input-Text refinement |

主要动机：目前的text-based models编辑结果受input prompts的影响很大，对图像的描述越详细准确编辑结果越好，而用户编辑图像时提供精确的描述是一个费时费力的工作，因此提出一个uers-friendly的方法使用户仅提供几个词就可以实现跟详细描述一样的编辑效果。

主要创新点：提出一种方法，有效利用现有的标题生成框架来填充用户所给简单单词之外的上下文信息，使得用户不必进行繁琐的文本提示工程。提出了一种将用户提供的源属性注入到由标题模型生成的提示中的方法，以指定要在源图像中编辑的区域。（captioning-based method）利用PEZ框架继续优化得到的input Prompts（固定要编辑的源属性的token）。通过比较生成的Prompt与删掉某个token之后的Prompt的CLIP分数，来确定是否存在冗余的token。

缺点：对于人脸的重建/编辑效果较差。

说明：与InstructEdit相同的是在反演时都不是反演到T，而是在某个中间步。

---

### DiffEdit

| 模型简称 | 论文全称 | 作用域 | 发表时间 | 期刊/Arxiv | 方法类型 | 方法细分 |
| --- | --- | --- | --- | --- | --- | --- |
| DiffEdit | DIFFEDIT：DIFFUSION-BASED SEMANTIC IMAGE EDITING WITH MASK GUIDANCE | real&synthesis | 2023 | ICLR | train-testing free | Mask Guidance |

主要动机：许多情况下，语义图像编辑只需要编辑某一部分，而保持其他部分不变，然而，iinput text query并不能明确地识别这个区域，而且一个简单的方法可能允许对整个图像进行编辑，从而有可能在不需要编辑的区域中修改它的输入，为了解决这个问题提出动态mask引导图像编辑的方法。

主要创新点：主要的贡献是能够通过对比基于不同文本提示的扩散模型的预测(在对加噪后的input image进行去噪时，不同的ref和query text会使text-conditioned diffusion model预测的噪声会有不同，根据两个预测间的差值作为生成mask的依据)，自动生成需要编辑的输入图像的屏蔽区域。

缺点：未完待续。

说明：与无文本反演不同，进行DDIM反演时采用的是w=0，非条件DFM。

---

### InstructEdit

| 模型简称 | 论文全称 | 作用域 | 发表时间 | 期刊/Arxiv | 方法类型 | 方法细分 |
| --- | --- | --- | --- | --- | --- | --- |
| InstructEdit | DIFFEDIT：DIFFUSION-BASED SEMANTIC IMAGE EDITING WITH MASK GUIDANCE | real | 2023 | Arxiv | train-testing free | Input-Text refinement |

主要动机：许多情况下，语义图像编辑只需要编辑某一部分，而保持其他部分不变，然而，iinput text query并不能明确地识别这个区域，而且一个简单的方法可能允许对整个图像进行编辑，从而有可能在不需要编辑的区域中修改它的输入，为了解决这个问题提出动态mask引导图像编辑的方法。

主要创新点：主要的贡献是能够通过对比基于不同文本提示的扩散模型的预测(在对加噪后的input image进行去噪时，不同的ref和query text会使text-conditioned diffusion model预测的噪声会有不同，根据两个预测间的差值作为生成mask的依据)，自动生成需要编辑的输入图像的屏蔽区域。

缺点：未完待续。

说明：与无文本反演不同，进行DDIM反演时采用的是w=0，非条件DFM。

---

### Collaborative Diffusion

| 模型简称 | 论文全称 | 作用域 | 发表时间 | 期刊/Arxiv | 方法类型 | 方法细分 |
| --- | --- | --- | --- | --- | --- | --- |
| Collaborative Diffusion | Collaborative Diffusion for Multi-Modal Face Generation and Editing | realfaceimage | 2023 | CVPR | training free testing finetuning | Mask Guidance&Input-Text refinement |

主要动机：已有的扩散模型大多基于单模态控制（uni-modal control）,文章尝试探索在生成或编辑人脸图像时使用text和face shape进行control。观点：不同模态的模型是互补的。

主要创新点：通过meta network(UNet) dynamic diffusers计算每一种模态扩散模型的influence function来实现collaborative diffusion。

缺点：模型很依赖预训练扩散模型本身的性能，需要在更大的数据集上训练出来的DFM。（论文展示的人脸图像编辑的操作只涉及到改变年龄，改变性别，以及胡须长度，可能与mask有关？attention？对背景的保存能力也不太行）

说明：（见补充材料）论文中dfm采用Imagic方法，以文本条件为例：首先优化target文本条件，使扩散模型可以重建输入的图像，为了优化输入图像的保真度，模型会固定优化后的文本条件，优化模型参数theta，之后真正的编辑文本条件会是target文本条件与优化后文本条件的插值，以此来实现人脸图像的编辑。（这个方法不需要source text）
