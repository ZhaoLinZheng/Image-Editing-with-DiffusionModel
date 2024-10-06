### Null-Text inversion

| 模型简称 | 论文全称 | 作用域 | 发表时间 | 期刊/Arxiv | 方法类型 | 方法细分 |
| --- | --- | --- | --- | --- | --- | --- |
| Null-Text inversion | Null-text Inversion for Editing Real Images using Guided Diffusion Models | real | 2023 | CVPR | train-finetuning free | Inversion/SampleModification |

主要动机：目前基于classifier-free的IE受无条件预测影响大，因而试图改进null-text embedding。

主要创新点：（w=1）DDIM inversion as pivot，（w>1）pivotal tuning，optimize the null text embedding。

缺点：推理速度太慢，使用SD带来的编辑人脸图像时会出现伪影，和不能进行大幅度修改的问题。

说明：进行DDIM反演时，w=1,只采用条件DFM。

---
### 详细介绍
#### 摘要
文本引导扩散模型具有很强的图像生成能力。最近有大量的工作仅利用文本来使用这些sota模型对生成的图像进行修改。而对于使用这些模型来编辑真实图像，必须要首先把图像和一个对应的text prompt来invert into the pretrained models domin（得到真实图像变为噪声的扩散轨迹）。本文一种直观精确的inversion技术，它主要包含两个关键部分：（1）Pivotal inversion for diffusion model。现有的方法旨在将多个随机噪声样本对应到单张图像，而我们对每个timestamp使用单个枢纽噪声向量，并且围绕它进行优化。（2）null-text inversion。我们只修改classifier-free guidance中的无条件文本嵌入，保持文本嵌入不变。以此保持模型权重和条件嵌入intact，同时避免了对模型权重繁琐的finetuning。
#### 介绍
现有基于文本条件的编辑方法在synthesis images具有很好的效果，允许用户很容易地仅用文本就可以修改图像。

但是基于文本条件的编辑方法在真实图像上需要首先将给定的图像和文本提示进行inversion。也就是，找到一个初始化噪声向量，当这个向量与给定的文本一起进行denoising时，能够产生我们初始时给定的图像。（重建，同时保持模型的编辑能力）

对于无条件扩散模型，DDIM inversion是有效的，但对于使用classifier-free guidance的文本引导扩散模型，它是不足的。尽管如此，DDIM仍然可以offer a promising starting point for the inversion.

第一个可以使prompt2prompt进行真实图像编辑的方法。
#### 方法
I: a real image

I^star: an edited image

P: source prompt (由一个off-the-shelf captioning model Clip-cap生成)

P^star: edited prompt

我们的方法基于两个观察：首先，当应用无分类器引导时，DDIM反演产生了不令人满意的重建，但为优化提供了一个良好的起点，使我们能够有效地实现高保真度的反演。其次，优化无条件零嵌入，用于无分类器引导，允许精确的重建同时避免对模型和条件嵌入的微调。

我们意识到使用DDIM inversion（w=1）提供了原始图像的粗略近似，这是高度可编辑的，但不够精确。由于高可编辑性，我们将w = 1的初始DDIM inversion作为我们的pivot轨迹；在w>1的时候，我们进行denoising，围绕pivot对null-text embedding进行优化。



















