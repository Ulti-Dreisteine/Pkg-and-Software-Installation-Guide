### Latex安装步骤

1. 进入Tex官网：https://www.tug.org/texlive/
   <img src="fig 1.png" width=600>
2. 选择国内镜像进行下载：
   <img src="fig 2.png" width=600>
   <img src="fig 3.png" width=600>
3. 下载后打开ios文件，找到install-tl-windows.bat，右键以管理员身份运行
4. 更改安装位置：
   <img src="fig 4.png" width=300>
5. 点击左下角Advanced可以更改更多安装选项，可选择只安装中英文：
   <img src="fig 5.png" width=300>
   <img src="fig 6.png" width=300>
6. 选好后点击右下角安装，等待安装完成即可，安装时间较长，一般情况大概在一小时左右。安装完成后在cmd中输入以下命令查看安装信息：
   ```bash
   tex -v
   latex -v
   xelatex -v
   ```
   若不返回安装信息，可在环境变量中添加如下路径：D:\texlive\2022\bin\win32，添加后再次在cmd中输入命令验证是否安装成功。

**安装 TEX Live 之后，建议升级全部宏包，升级方法：**
* 使用 cmd 或 terminal 运行 tlmgr update --all，
* 如果 tlmgr 需要更新，请使用 cmd 运行 tlmgr update --self；如果更新过程中出现了中断，请改用 tlmgr
update --self --all --reinstall-forcibly-removed 更新