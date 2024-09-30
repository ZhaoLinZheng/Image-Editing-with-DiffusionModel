### 1 Collaborative Diffusion

| 模型简称 | 论文全称 | 作用域 | 发表时间 | 期刊/Arxiv | 方法类型 | 方法细分 |
| --- | --- | --- | --- | --- | --- | --- |
| Collaborative Diffusion | Collaborative Diffusion for Multi-Modal Face Generation and Editing | realfaceimage | 2023 | CVPR | training free testing finetuning | Mask Guidance&Input-Text refinement |

主要动机：已有的扩散模型大多基于单模态控制（uni-modal control）,文章尝试探索在生成或编辑人脸图像时使用text和face shape进行control。观点：不同模态的模型是互补的。

主要创新点：通过meta network(UNet) dynamic diffusers计算每一种模态扩散模型的influence function来实现collaborative diffusion。

缺点：模型很依赖预训练扩散模型本身的性能，需要在更大的数据集上训练出来的DFM。（论文展示的人脸图像编辑的操作只涉及到改变年龄，改变性别，以及胡须长度，可能与mask有关？attention？对背景的保存能力也不太行）

说明：（见补充材料）论文中dfm采用Imagic方法，以文本条件为例：首先优化target文本条件，使扩散模型可以重建输入的图像，为了优化输入图像的保真度，模型会固定优化后的文本条件，优化模型参数theta，之后真正的编辑文本条件会是target文本条件与优化后文本条件的插值，以此来实现人脸图像的编辑。（这个方法不需要source text）

