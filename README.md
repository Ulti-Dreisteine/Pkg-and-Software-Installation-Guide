# software-config-files

各软件配置文件

## 1. Pycharm + Anaconda环境配置

1. 下载Anaconda和Pycharm进行安装：
   
   > Anaconda3: 2020.02 for MacOS + Pycharm: 2019.3.4 community
   > Anaconda3: 2020.02 for Windows + PyCharm 2019.3.5 professional

   * 博士论文环境: Python 3.8.8 (Anaconda 2021.5)

2. 环境clone
   **<font color=red>(注意: 在Anaconda Prompt而非系统Terminal中执行以下命令)</font>**

   > conda create -n *新环境名* --clone *老环境名*

3. 在MacOS上进行环境配置，运行numpy或matplotlib时可能遇到如下情况：

   > OMP: Error #15: Initializing libiomp5.dylib, but found libiomp5.dylib already initialized.

   可能问题是numpy或matplotlib等相关包版本文件有问题，建议卸载本地相关包，并清空缓存：

   ```bash
   pip uninstall numpy matplotlib scikit-image scikit-learn seaborn scipy
   conda clean -p
   ```

   然后通过pip重新安装相关包, 注意版本：

   ```bash
   pip install --user numpy==1.18.1 -i https://mirrors.aliyun.com/pypi/simple/
   pip install --user matplotlib==3.1.3 -i https://mirrors.aliyun.com/pypi/simple/
   pip install --user scikit-learn==0.22.1 -i https://mirrors.aliyun.com/pypi/simple/
   pip install --user seaborn==0.10.0 -i https://mirrors.aliyun.com/pypi/simple/
   pip install --user scipy -i https://mirrors.aliyun.com/pypi/simple/
   ```

   > ImportError: DLL load failed while importing _sqlite3: 找不到指定的模块

   可能是Anaconda里Scipy的问题, 卸载重装即可.

## 2. Pycharm主题settings设置

参见file.pycharm中的settings.zip

## 3. Mac安装Homebrew

国内安装(可用), 建议采用腾讯或阿里云:

```zsh
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

## 4. Python包安装

* <u>**PyTorch安装**</u>

  * 安装CUDA和CUDNN: 对于GTX 1060, 显卡驱动版本$\geq$442.59, CUDA选择10.1或10.2
  * 将torch和torchvision文件下载至本地使用pip安装, 文件地址: <https://download.pytorch.org/whl/torch_stable.html>

  * RTX 4090D：
     * Cuda Toolkit 12.1（因为PyTorch只有对应Cuda11.8和12.1的版本）
   
   安装好以后，进行耗时测试：
  ```{python}
  import torch
  import time
   
  def train(size_list, epochs):
   
     for s in size_list:
   
        # CPU
        start_time1 = time.time()
        a = torch.ones(s,s)
        for _ in range(epochs):
           a += a
        cpu_time = time.time() - start_time1
   
        # GPU
        start_time2 = time.time()
        b = torch.ones(s,s).cuda()
        for _ in range(epochs):
           b += b
        gpu_time = time.time() - start_time2
   
        print('s = %d, CPU_time = %.4fs, GPU_time = %.4fs'%(s, cpu_time, gpu_time))
   
  size_list = [8, 32, 128, 512]
  epochs = 100000
  train(size_list, 100000)
  ```

* <u>**LightGBM安装**</u>

  * 注意不同版本对应结果有很大差异，这里选择使用2.3.1版本：

    ```
    pip install lightgbm==2.3.1
    ```

* <u>**PyMC3安装**</u>

  以下安装在python 3.8.8及以下版本测试有效, 更高python版本待测试:

  **<font color=red>(注意: 在Anaconda Prompt而非系统Terminal中执行以下命令)</font>**

  ```
  pip install pymc3 -i https://mirrors.aliyun.com/pypi/simple/
  conda install numpy scipy mkl-service libpython m2w64-toolchain
  conda install -c conda-forge blas
  conda install -c conda-forge python-graphviz
  ```

  若出现warning:

  > WARNING (theano.tensor.blas): Using NumPy C-API based implementation for BLAS functions

  则进行以下安装:

  ```
  conda install mkl
  conda install mkl-service
  conda install blas
  conda install -c conda-forge python-graphviz
  ```

  然后在"C:\Users\Administrator等用户名"下新建".theanorc.txt"文件，里面输入:

  ```
  [blas]
  ldflags=-lmkl_rt
  ```

  或

  ```
  [blas]
  ldflags=-lblas
  ```

  <font color="red">安装完毕后可运行file.pymc_running_test.ipynb对PyMC进行运行测试</font >

## 5. R + Jupyter Notebook

* <u>安装Jupyter Notebook中的R内核</u>

  * 参见https://blog.csdn.net/qq_43198568/article/details/105641104
  
    ```
    conda install -c r r-essentials
    ```

## 6. VS Code中的Pylint安装

* <u>安装pylint</u>
  
  ```
  pip install pylint
  ```

* <u>安装VS Code中的PyLint包</u>, 设置相关参数
* <u>卸载pylint</u>

  ```
  pip uninstall pylint
  ```

## 7. Conda重建索引

清除缓存：

```bash
conda clean --all
```

重建索引：

```bash
conda update --all conda
```
