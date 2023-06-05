#### 1. 编写setup.py文件

#### 2. 通过setup.py打包本地文件
python setup.py bdist_wheel sdist

#### 3. 上传至PyPI
pip install twine -i https://mirrors.aliyun.com/pypi/simple/
twine upload dist/* --verbose