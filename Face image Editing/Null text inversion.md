### Null-Text inversion

| 模型简称 | 论文全称 | 作用域 | 发表时间 | 期刊/Arxiv | 方法类型 | 方法细分 |
| --- | --- | --- | --- | --- | --- | --- |
| Null-Text inversion | Null-text Inversion for Editing Real Images using Guided Diffusion Models | real | 2023 | CVPR | train-testing free | Inversion/SampleModification |

主要动机：目前基于classifier-free的IE受无条件预测影响大，因而试图改进null-text embedding。

主要创新点：（w=1）DDIM inversion as pivot，（w>1）pivotal tuning，optimize the null text embedding。

缺点：推理速度太慢，使用SD带来的编辑人脸图像时会出现伪影，和不能进行大幅度修改的问题。

说明：进行DDIM反演时，w=1,只采用条件DFM。

---
具体介绍
