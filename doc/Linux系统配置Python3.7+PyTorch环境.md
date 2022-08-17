## 配置步骤

#### 注意事项

* 低版本的Pytorch可能无法加载高版本Pytorch训练所得模型
* Pytorch的cudatoolkit版本必须与机器的CUDA版本完全一致
* nvidia-smi中显示的CUDA版本为驱动程序支持的CUDA最高版本

#### 1. 配置Anaconda环境

下载：
```
wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-2020.02-Linux-x86_64.sh
```
然后使用bash命令安装文件

#### 2. 配置基于CUDA的Pytorch.

##### 2.1 查看本地CUDA版本:

```
nvidia-smi
```

获得CUDA Version: 10.1或其他，本文以CUDA 10.1为例.

##### 2.2 如果要离线安装的话需要下载对应版本PyTorch安装包:

```
https://download.pytorch.org/whl/torch_stable.html
```

找到适用于CUDA 10.1的torch和torchvision文件并下载至本地.

##### 2.3 安装Pytorch.

进入文件所在目录，使用conda命令安装：

```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/menpo/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
conda config --show-sources
```

```
conda install pytorch torchvision cudatoolkit=10.1
```

##### 2.4 环境变量配置

```
vi /.bashrc
```

在打开的文件中另起一行，输入以下环境变量：

```
export CUDA_HOME=/usr/local/cuda-10.1
export PATH=$PATH:/usr/local/cuda-10.1/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-10.1/lib64:/usr/local/cuda10.1/lib
export LIBRARY_PATH=$LIBRARY_PATH:/usr/local/cuda-10.1/lib64
```

使用":wq"保存退出，然后更新环境变量：

```
source ~/.bashrc
```

##### 2.5 测试PyTorch安装结果

```
python
>>> import torch
>>> torch.__version__
'1.6.0'
>>> torch.cuda.is_available()
True
```

只要显示torch.cuda为True即说明基于GPU的Pytorch已经安装成功.