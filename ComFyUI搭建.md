# ComFyUI工作流搭建

[TOC]



## 第一步 选择大模型加载器



右键空白处，选择“添加节点”=》"加载器" =》“Checkpoint加载器（简易）”

<img src="images\buildComfyUI\01.png" align = left alt="some_text">



<img src="images\buildComfyUI\02.png " align = left alt="加载器界面" style="zoom:50%;" >

点击“Checkpoint”可以选择自己想要使用的模型

## 第二步添加K采样器



右键空白处，选择“添加节点”=》"采样" =》“K采样器”

<img src="images\buildComfyUI\03.png " align = left alt="加载器界面" style="zoom:50%;" >



| 随机种子：没次生成的图片都会带有随机种子数字代表图片的ID<br>运行后操作：<br/>固定：固定seed值，固定图片<br/>增加：seed值加1<br/>减少：seed值减1<br/>随机：默认<br/> | <img src="images\buildComfyUI\04.png " align = left alt="加载器界面" style="zoom:50%;" > |
| -------------------------------------------------------- | ------------------------------------------------------------ |

## 第三步添加VAE编码



右键空白处，选择“添加节点”=》"Latent" =》“VAE解码”

<img src="images\buildComfyUI\05.png " align = left alt="加载器界面" style="zoom:50%;" >

<img src="images\buildComfyUI\06.png " align = left alt="加载器界面" style="zoom:80%;" >

## 第四步添加clip文本编辑器



右键空白处，选择“添加节点”=》"条件" =》“Clip文本编辑器”

<img src="images\buildComfyUI\07.png " align = left alt="加载器界面" style="zoom:50%;" >

<img src="images\buildComfyUI\08.png " align = left alt="加载器界面" style="zoom:50%;" >

> [!NOTE]
>
> 由于正反提示词的需要，所以CLIP文本编码器需要创建两个，第二个可以通过复制ctrl+C/V复制



## 第五步创建空Latent



右键空白处，选择“添加节点”=》"Latent" =》“空Latent”

<img src="images\buildComfyUI\09.png " align = left alt="加载器界面" style="zoom:50%;" >

<img src="images\buildComfyUI\10.png " align = left alt="加载器界面" style="zoom:50%;" >



## 第六步创建图像保存



右键空白处，选择“添加节点”=》"图像" =》“保存图像”

<img src="images\buildComfyUI\11.png " align = left alt="加载器界面" style="zoom:50%;" >



## 第七步创建LORA加载器



右键空白处，选择“添加节点”=》"加载器" =》“LORA加载器（pyss）”

<img src="images\buildComfyUI\13.png " align = left alt="加载器界面" style="zoom:50%;" >

<img src="images\buildComfyUI\14.png " align = left alt="加载器界面" style="zoom:80%;" >

LoRA名称：选择要加载的LoRA模型

模型强度：根据模型推荐设置

CLIP强度：根据模型推荐设置



## 第八步连线



Checkpoint加载器的模型和CLIP分别连接LoRA的模型和CLIP，VAE链接VAE解码器的VAE口

<img src="images\buildComfyUI\15.png " align = left alt="加载器界面" style="zoom:80%;" >

LoRA加载器的模型口链接K采样器的模型口，CLIP口同时连接正/反提示词的CLIP文本编码器，

两个“CLIP文本编码器”根据自身设定“条件”分别连接K采样器的正面条件和负面条件。

”K采样器“Latent链接“空Latent”的Latent口



<img src="images\buildComfyUI\16.png " align = left alt="加载器界面" style="zoom:80%;" >

“K采样器”的Latent口链接“VAE解码”的Latent口，

"VAE解码"的图像口链接“保存图像”的图像口

<img src="images\buildComfyUI\17.png " align = left alt="加载器界面" style="zoom:80%;" >

最终结果如下:

此图连接了两个LoRA,实际可根据情况变动

<img src="images\buildComfyUI\18.png " align = left alt="加载器界面" style="zoom:80%;" >
