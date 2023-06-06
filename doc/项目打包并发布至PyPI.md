#### 1. 编写setup.py文件

```python
from setuptools import setup, find_packages
from pathlib import Path

VERSION = "0.0.7"                                                   # 版本设置
DESCRIPTION = "Package for information estimation, independence test, etc."
this_directory = Path(__file__).parent
long_description = (this_directory/"README.md").read_text(encoding="utf-8") # NOTE: 使用UTF-8可识别中文

setup(
    name="giefstat",                                                # 包的名字
    version=VERSION,
    author="************",
    author_email="************@163.com",
    description=DESCRIPTION,                                        # 简介
    packages=find_packages(include=["giefstat", "giefstat.*"]),     # 需要打包的内容. NOTE: 注意giefstat.*的写法
    install_requires=["scikit-learn==0.24.0", "minepy==1.2.6"],     # 依赖
    keywords=["python", "information estimation"],
    python_requires=">=3.8.0",
    license="MIT License",
    long_description=long_description,                              # 这里使用了项目readme内容
    long_description_content_type="text/markdown",
    url="https://github.com/Ulti-Dreisteine/general-information-estimation-framework",  # GitHub地址
)
```

#### 2. 通过setup.py打包本地文件

```bash
python setup.py bdist_wheel sdist
```

#### 3. 上传至PyPI

安装twine

```bash
pip install twine -i https://mirrors.aliyun.com/pypi/simple/  
```

在PyPI上注册账号, 并在本地通过twine上传打包内容:

```bash
twine upload dist/* --verbose
```