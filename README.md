# Build C/C++ Environment with VS Code

In this repo, you will learn how to install a complete development environment, and run the ''HelloWorld'' demo.

通过阅读本菜鸟包的内容，你将学会如何安装一套完整的开发环境，并在该环境上尝试运行一个简单的“HelloWorld”程序。

## Compiler | 编译器

Compilers are tools to compile executable programs from source code files. It ''translates'' advanced programming language source code files (eg. C/C++) to binary executable programs.

编译器是用来将源代码文件编译成可执行文件的工具，它将高级语言（例如C/C++）的源代码“翻译”成机器上的二进制可执行代码。

In this repo, you will learn how to install **MinGW** on Windows.

在本次菜鸟包中，你将学习如何在Windows系统上安装**MinGW**编译环境。

### MinGW Installation | MinGW安装

1. Download MinGW from the [source forge](https://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/).

    从[官网](https://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/)下载MinGW。

![MinGW Download](figure/mingw-w64.png)

2. Install MinGW. Choose newest version. Choose the right architecture according to your system WORD.(i686 for 32 bits system and x86_64 for 64 bits system) Wait.. Until the progress complete.

    安装MinGW。选择最新的版本，按照系统的位数选择正确的体系结构。（32系统位选择i686，64位系统选择x86_64）等待下载器下载和安装。

    ![](figure/mingw-install.png)

3. Add path. Right click ''My Computer'' and select ''Properties -> Advanced Setting -> Advanced -> Environmental Variables''.  Put the absolute path of ''bin'' in mingw64 into the path list.

添加环境变量。右键单击“我的电脑”，选择“属性->高级系统设置->高级->环境变量”，将mingw64目录中的bin子目录放入列表中。

![MinGW Environmental Path](figure/mingw_path.png)

5. Open command line console, and input ''gcc -v'' command.

    打开命令行窗口，输入“gcc -v”命令。

![MinGW Test](figure/mingw_test.png)

### Visual Studio Code Installation

Download Visual Studio Code(VS Code) from the [official website](https://code.visualstudio.com/).

Choose version according to youroperating system.(Stable and Insiders are both Okay.)

![](figure/vscode-download.png)

### VS Code Extension Installation

Click the Extension button at left side.

Search "c++".

Install "C/C++" and "C++ Intellisense".

![](figure/vscode-extension.png)

### VS Code Configure

1. Create an empty folder to hold your code. (eg. "C:\Users\***\Documents\WorkSpace\Code")

   Open this folder from VS Code.

![](figure/vscode-folder.png)

2. Create a demo cpp file for test.

```cpp
#include <iostream>
using namespace std;

int main()
{
	cout << "Don't say hello world again." << endl;
	return 0;
}
```

![](figure/vscode-cpp.png)

3. Add task configuration for compile and debug. Choose "Default Configuration".

![](figure/vscode-config.png)

Then we have generated a file -- "launch.json".

![](figure/vscode-launch1.png)

Modify "enter program name, for example \${workspaceFolder}/a.exe" to "​\${file}.out".

Modify "/path/to/gdb" to gdb path which you have added to System PATH.

Modify "externalConsole" to "true".

Add one line: 	

```text
"preLaunchTask": "compile",
```

![](figure/vscode-launch0.png)

Go back to your code and press F5. You will get error message as following:

![](figure/vscode-launch2.png)

Click "Configure Task". Choose "Create tasks.json file from template". Choose Others.

![](figure/vscode-task.png)

![](figure/vscode-task1.png)

Copy the following code to "tasks.json":

```json
{
        // See https://go.microsoft.com/fwlink/?LinkId=733558
        // for the documentation about the tasks.json format
        "version": "2.0.0",
        "tasks": [
            {
                "label": "compile",
                "type": "shell",
                "command": "g++",
                "args": [
                    "-g",
                    "-std=c++14",
                    // "-lpthread",
                    "\"${file}\"",
                    "-o",
                    "${file}.out"
                ],
                "presentation": {
                    "reveal": "always",
                    "panel": "shared",
                    "focus": false,
                    "echo": true
                },
                "group": {
                    "kind": "build",
                    "isDefault": true
                },
                "problemMatcher": {
                    "owner": "cpp",
                    "fileLocation": "absolute",
                    "pattern": {
                        "regexp": "^(.*):(\\d+):(\\d+):\\s+(error):\\s+(.*)$",
                        "file": 1,
                        "line": 2,
                        "column": 3,
                        "severity": 4,
                        "message": 5
                    }
                }
            }
        ]
}
```

Go back to your code, add a breakpoint and Press F5 to run your program !

![](figure/vscode-run.png)

Now you have successfully run your first program.

Next time you want to enjoy coding, create and edit a cpp file in this folder. And then you can press F5 to run it directly. Yeah, simple and quick !