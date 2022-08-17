
## 用CLion吧, 把mingw64配置好了就行~~

## 基于VS Code的C++环境配置
### 基本步骤
#### 1. VS Code安装  
  * 下载并安装VS Code
  * 安装"C/C++ tools", "C/C++ Clang Command Adapter"

#### 2. mingw-w64配置（实现C++编译和调试）
  <u>*在线安装（下载很慢）*</u>
  * 搜索和下载mingw-w64的exe安装文件：<u>https://sourceforge.net/</u>
  * 安装mingw-w64:
    * Architecture: x86_64
    * Threads: win32
    * Exception: SEH
  * 将安装好的MinGW-w64的bin目录添加到Windows的Path环境变量中

  <u>*离线安装*</u>
  * 解压pkg文件夹中已下载好的压缩包
  * 将解压后的"mingw64"文件夹拷贝至安装目录下
  * 配置环境变量：在Administrator环境变量的path中添加你的mingw64/bin，如"D:\mingw64\bin"
  * 在cmd窗口使用"gcc -v"查看安装状态

#### 3. Clang环境配置（实现C++自动补全）
  * 文件下载和安装：在<u>https://clang.llvm.org/</u>中找到合适的LLVM对应Windows(64-bit)版本，并下载安装
  *


#### 4. 在VS Code上对C++的编译运行进行配置
1. 打开任务文件夹
2. 在最上层目录下新建.vscode目录, 并添加以下文件:

    **launch.json**
    ```
    {
        "version": "0.2.0",
        "configurations": [
            {
                "name": "g++.exe build and debug active file",
                "type": "cppdbg",
                "request": "launch",
                "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
                "args": [],
                "stopAtEntry": false,
                "cwd": "${workspaceFolder}",
                "environment": [],
                "externalConsole": true,  // 修改此项，让其弹出终端
                "MIMode": "gdb",
                "miDebuggerPath": "D:\\mingw64\\bin\\gdb.exe",  // 对应mingw64的安装目录
                "setupCommands": [
                    {
                        "description": "Enable pretty-printing for gdb",
                        "text": "-enable-pretty-printing",
                        "ignoreFailures": true
                    }
                ],
                "preLaunchTask": "task g++"  // 修改此项, 对于tasks.json里的label
            }
        ]
    }
    ```  

    **tasks.json**
    ```
    {
        "version": "2.0.0",
        "tasks": [
            {
                "type": "shell",
                "label": "task g++",    //修改此项
                "command": "D:\\mingw64\\bin\\g++.exe",  // 对应mingw64的安装目录
                "args": [
                    "-g",
                    "${file}",
                    "-o",
                    "${fileDirname}\\${fileBasenameNoExtension}.exe"
                ],
                "options": {
                    "cwd": "D:\\mingw64\\bin"  // 对应mingw64的安装目录
                },
                "problemMatcher": [
                    "$gcc"
                ],
                "group": "build"
            }
        ]
    }
    ```

3. 新建*.cpp文件，使用F5即可调试
