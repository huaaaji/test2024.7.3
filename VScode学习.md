# VScode之学习

## 简介

vscode由typescript，采用electron架构，对于JavaScript、TypeScript和Node.js有内置支持，并为其他语言提供了丰富的拓展生态系统

## VSCode的快捷键

按键|操作
---|---
`Ctrl+C/X`|复制/剪切当前行（当没有选择内容时）
`Ctrl+Shift+K`|删除当前行
`Alt+Up/Down`|行上移/下移
`Alt+Shift+Up/Down`|行向上/向下复制
`Ctrl+/`|切换行注释
`Ctrl+[/]`|行向左/右缩进
`Ctrl+Shift+[/]`|行折叠/展开
`Ctrl+P`|打开最近打开的文件
`Alt+Z`|切换自动折行
`Alt+F12`|速览定义（如函数的定义）
`Ctrl+Shift+\`|跳转到匹配括号
`Ctrl+T`|在工作区中查找符号（在文件夹中查找指定名称函数等）

## VScode的扩展

### 使用Code Runner运行代码

这是一个简单的编译和运行C++程序的方法，即使用扩展：Code Runner
其是一种可以一键运行代码的扩展，支持Node.js、Python、C、C++、Java、PHP、Perl、Ruby、Go 等 40 多种语言

安装后在编辑页面即可直接通过运行按钮运行程序，或使用快捷键 `Ctrl`+`Alt`+`N` 

### 使用C/C++拓展以编译并调试，及智能补全代码

#### 安装拓展

略

>在配置前，请确保系统已经安装了 G++ 或 Clang，并已添加到了 PATH 中。请使用 CMD 或者 PowerShell，而不是 Git Bash 作为集成终端。

#### 配置GDB/LLDB调试器

##### GDB

>新建一份 C++ 代码文件，按照 C++ 语法写入一些内容（如 `int main(){}`），保存并按下F5，进入调试模式。 如果出现了「选择调试器」的提示，选择 C++ (GDB/LLDB)。在「选择配置」中，G++ 用户选择 g++.exe - 生成和调试活动文件；Clang 用户选择 clang++ - 生成和调试活动文件。

完成后，VS Code 将自动完成初始化操作在下方的集成终端中启动调试。至此，GDB 所有的配置流程已经完毕。

#### LLDB

如果需要采用 LLDB，需要安装另外一款扩展——CodeLLDB。从该项目的 Release 页面下载 `.vsix` 文件后，从 VS Code 的扩展页面安装（扩展页面有“从VSIX安装”的选项）。
先按照上文 GDB 的配置过程操作一遍，然后删除 .vscode/launch.json，按下F5，选择 LLDB，再把 launch.json 中的 `${workspaceFolder}/<executable file>` 更改为 `${fileDirname}/${fileBasenameNoExtension}.exe` 即可。

至此，LLDB 配置完成。再次按下F5即可看到软件下方的调试信息。

若要在以后使用 VS Code 编译并调试代码，所有的源代码都需要保存至这个文件夹内。若要编译并调试其他文件夹中存放的代码，需要重新执行上述步骤（或将旧文件夹内的 .vscode 子文件夹复制到新文件夹内）。

### 调试代码

打断点操作省略

按下F5进入调试模式，编辑器上方会出现一个调试工具栏，四个蓝色按钮从左至右分别代表 GDB 中的 continue,next,step 和 until：
![调试工具栏](N:/VSCODE2024.3.31/Markdown/pictures/vscode-6.png)
如果编辑器未自动跳转，点击左侧工具栏中的「调试」图标进入调试窗口，即可在左侧看到变量的值。

### 配置intellsense

以此调整VSCode的智能补全
如果你使用 Clang 编译器，在「IntelliSense 模式」中选择 clang-x64 而非默认的 msvc-x64；如果你使用 G++ 编译器，选择 gcc-x64 以使用自动补全等功能。否则会得到「IntelliSense 模式 msvc-x64 与编译器路径不兼容。」的错误。

## clangd

>Clangd is an implementation of the Language Server Protocol leveraging Clang. Clangd’s goal is to provide language "smartness" features like code completion, find references, etc. for clients such as C/C++ Editors.

>简单来说，clangd 是 Clang 对语言服务器协定（Language Server Protocol）的实现，提供了一些智能的特性，例如全项目索引、代码跳转、变量重命名、更快的代码补全、提示信息、格式化代码等，并且能利用 LSP 与 Vim、Emacs、VSCode 等编辑器协作。虽然官方给出的定义是 LSP 的实现，但 clangd 的功能更接近语言服务器（Language Server）而不仅仅只是协议本身。

>VS Code 的 C/C++ 扩展也有自动补全等功能，但在提示信息的易读程度的准确度等方面与 clangd 相比稍逊一筹，所以我们有时会使用 clangd 代替 C/C++ 扩展来实现代码自动补全等功能。

安装扩展后，如果弹出 clangd 要求关闭 Intellisense 的对话框，点击 "Disable Intellisense"，重新加载工作区，就可以享受 clangd 的自动补全等功能了。

## 经验补充

>Visual Studio Code 在调试和任务配置文件以及一些选择设置中支持变量替换。使用`${variableName}`语法，在`launch.json`和`tasks.json`文件中的键和值字符串中进行变量替换。

变量替换语法|解释
---|---
`${workspaceFolder}` | 在VS Code中打开的文件夹的最顶层路径（根文件夹）
`${workspaceFolderBasename}` | 在VS Code中打开的文件夹的名称，不包括 “ / ”
`${file}` | 当前打开的文件名称（绝对路径 + 主名 + 扩展名）
`${relativeFile}` | 相对文件名（文件夹名 + “/" + 文件全名）
`${relativeFileDirname}` | 当前文件的文件夹名（只有名字，没有路径）
`${fileBasename}` | 当前文件全名（主名+扩展名）
`${fileBasenameNoExtension}` | 当前文件主名（不含扩展名）
`${fileDirname}` | 文件的绝对路径，不包括文件名和末尾的路径分隔符
`${fileExtname}` | 当前打开的文件的扩展名
`${cwd}` | the task runner's current working directory on startup
`${lineNumber}` | 光标所在位置的代码的行号
`${selectedText}` | 当前编辑文件中选择的内容
`${execPath}` | Code.exe的路径
`${defaultBuildTask}` | 默认构建任务的名称

### 关于配置问题

配置c++调试环境时的配置文件(.vscode中)

#### launch.json

~~~json
{
    "configurations": [

    {
        "name": "(gdb) 启动",//这是显示出来的这一配置的名称
        "type": "cppdbg",//注意配置类型的选择
        "request": "launch",//请求配置类型。可以是“启动”或“附加”。
        "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
        "args": [],
        "stopAtEntry": false,
        "cwd": "${fileDirname}",
        "environment": [],
        "externalConsole": false,
        "MIMode": "gdb",
        "preLaunchTask": "C/C++: g++.exe 生成活动文件", //注意preLaunchTask,在vscode添加配置文件时不会生成这一键
        "miDebuggerPath": "N:\\CODE Confriguration\\mingw64\\bin\\gdb.exe",//MI 调试程序(如 gdb)的路径。如果未指定，将首先在路径中搜索调试程序。
        //需要指定
        "setupCommands": [
            {
                "description": "为 gdb 启用整齐打印",
                "text": "-enable-pretty-printing",
                "ignoreFailures": true
            },
            {
                "description": "将反汇编风格设置为 Intel",
                "text": "-gdb-set disassembly-flavor intel",
                "ignoreFailures": true
            }
        ]
    }
    ]
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
}
~~~

#### task.json

~~~json
{
    "tasks": [
        {
            "type": "cppbuild",//要自定义的任务类型
            "label": "C/C++: g++.exe 生成活动文件",//任务名称。
            "command": "N:\\CODE Confriguration\\mingw64\\bin\\g++.exe",
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": "build",
            "detail": "编译器: N:\\CODE Confriguration\\mingw64\\bin\\g++.exe"
        }
    ],
    "version": "2.0.0"
}
~~~