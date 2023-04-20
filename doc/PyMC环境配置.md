#### Step 1: 安装PyPy运行环境

```bash
# conda create -c conda-forge -n pypy_env pypy python=3.8
# conda activate pypy_env

conda create -c conda-forge -n pymc_env python=3.8 "pymc>=4"  # pymc==5.3.0
conda activate pymc_env
```

#### Step 2: 安装PyMC及相关包

```bash
conda install pymc
conda install ipykernel
conda install -c conda-forge python-graphviz
```

#### Step 3: 安装Jax

NOTE: 目前Windows上的PyMC还不支持Jax

<!-- * 文件安装:
  Jax下载地址: https://whls.blob.core.windows.net/unstable/index.html
  
  ```bash
  pip install jaxlib-0.3.25-cp38-cp38-win_amd64.whl
  ```
* pip安装(推荐)
  ```
  pip install --upgrade "jax[cpu]" -i https://mirrors.aliyun.com/pypi/simple/
  ```

```
pip install numpyro
pip install blackjax
``` -->