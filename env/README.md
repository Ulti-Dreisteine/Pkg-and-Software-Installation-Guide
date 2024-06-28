### 环境配置
```bash
conda create -n work python=3.10
conda activate work
conda install numpy pandas scikit-learn matplotlib
conda install jupyter
```



### Anaconda版本

Anaconda 2021.05 对应于Python 3.8

### Conda换源

Anaconda Prompt中运行:

```bash
conda config --set channel_priority strict 
conda config --set show_channel_urls yes
```

记事本打开"C:\Users\\**用户名**\\.condarc", 输入以下内容

```
channels:
  - conda-forge
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch-lts: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
```

### PyCaret安装

注意：Anaconda 2021.05中自带了PyCaret 3.0.4，~~仍需补充安装~~，卸载吧！！！！！：

~~```~~
conda install plotly
pip install matplotlib_inline -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install category_encoders -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install xxhash -i https://pypi.tuna.tsinghua.edu.cn/simple
~~```~~

其他情况下安装PyCaret：

```
conda create --name pycaret_env python=3.8
conda activate pycaret_env

pip install --user pycaret -i https://pypi.tuna.tsinghua.edu.cn/simple
python -m ipykernel install --user --name pycaret_env --display-name "display-name"
```
