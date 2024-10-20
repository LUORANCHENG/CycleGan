## 参考项目
https://github.com/junyanz/CycleGAN

https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix

https://github.com/eriklindernoren/PyTorch-GAN

[GAN生成对抗网络原理及cyclegan pytorch实战：天气季节转换 物种变换 医疗转换 建筑外立面转设计图_计算机视觉](https://www.bilibili.com/video/BV1qVmwYfEN4/?spm_id_from=333.337.search-card.all.click&vd_source=1a02178b1644ddc9b579739c3c1616b4)

[精读CycleGAN论文-拍案叫绝的非配对图像风格迁移](https://www.bilibili.com/video/BV1Ya411a78P/?spm_id_from=333.337.search-card.all.click&vd_source=1a02178b1644ddc9b579739c3c1616b4)


## 项目简介

本项目为深度学习的课程作业，使用CycleGan模型实现将现实的照片转换为莫奈风格的画
![image](https://github.com/user-attachments/assets/dc83474c-0e9c-47fb-92c9-6b5b3a5b1832)



## 安装
    $ conda create -n CycleGan python=3.8
    $ conda activate CycleGan
    $ git clone https://github.com/LUORANCHENG/CycleGan.git
    $ cd CycleGan/
    $ pip install -r requirements.txt

## 运行
Linux系统下可通过bash脚本下载数据集:

    $ cd datasets/
    $ bash download_cyclegan_dataset.sh monet2photo

Windows系统则需要手动下载数据集:

复制网址`http://efrosgans.eecs.berkeley.edu/cyclegan/datasets/`到浏览器打开选择monet2photo数据集下载，并调整为如下所示的文件目录结构

下载好的数据集目录应该为:
```
datasets
 └── monet2photo
   └── train
    ├── A
    └── B
   └── test
    ├── A
    └── B
```
回到项目根目录下，执行`cyclegan.py`开始训练

    $ python cyclegan.py --dataset_name monet2photo
## 原理介绍
### 1.什么是生成对抗网络gan

GAN的核心思想是通过生成器和判别器之间的对抗过程，使得生成器能够生成以假乱真的数据，而判别器则努力区分真实数据和生成的数据。这个过程类似于一个零和博弈，其中两个网络不断优化自己以提高对抗能力。

GAN的基本原理:生成器和判别器

生成器G:负责从随机噪声中生成新的数据样本。它的目标是生成能够欺骗判别器的数据。

判别器D:负责判断输入的数据是真实的还是由生成器生成的。它的目标是正确地区分真实数据和生成的数据。
![image](https://github.com/user-attachments/assets/6075edc0-e85f-4a54-894d-48ea2fe1b127)


GAN的核心公式：
![gan_公式](https://github.com/user-attachments/assets/1a6039d2-90bf-4b6a-99db-bc53dd1c1de6)

从判别器角度来理解公式：
![判别器角度](https://github.com/user-attachments/assets/875a36b1-c313-422a-9838-d9b8dade4574)

从生成器角度来理解公式：
![生成器角度](https://github.com/user-attachments/assets/a6a8a5f8-b566-4c86-88b4-cccead79309e)

训练过程：

在训练开始时，生成器和判别器的能力都很弱。通过交替训练这两个网络，判别器逐渐学会区分真实数据和生成数据，而生成器则学会生成更真实的数据以欺骗判别器。

这个过程通过最小化生成器和判别器之间的差异来进行，最终目标是使判别器无法区分真实数据和生成的数据，即达到 纳什均衡


