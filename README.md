如何创建DirectX9项目并编译源码

1.确保自己的VS有C++并且支持窗口程序开发
    打开Visual Studio Installer
    勾选"使用C++的游戏开发"并安装

2.安装DirectX 9 SDK
    运行DXSDK_Jun10.exe并安装

3.创建VS项目
    选C++，空项目
    资源管理器栏右键项目，选属性
        VC++ 目录
            包含目录，添加SDK的头文件：$(DXSDK_DIR)Include
            库目录，添加SDK的库目录：$(DXSDK_DIR)Lib\x86
            注：这里填的是环境变量目录，如何上一步SDK不是常规安装的没有环境变量，可以改为绝对路径
        链接器
            输入
                附加依赖项，添加winmm.lib;d3d9.lib;d3dx9.lib;这三个链接库，分别是win相关函数库，dx9库
            系统
                子系统，修改为窗口(/SUBSYSTEM:WINDOWS)，默认是控制台程序，改这样才有图形界面
    资源管理器源文件右键，选添加，现有项，把代码都包括进来，例如第一章的d3dInit.cpp，d3dUtility.cpp，d3dUtility.h

4.勘误与编译
    此时是编译不过的，因为源码是比较久了，当时的WindowAPI还比较旧，关于文本的参数都是可以窄字符，而新版的都改为宽字符了
    把所有出现字符串的地方，都改为宽字符，即在"ABC"前面加个L，变成L"ABC"这样就不报错了
    此时可以正常编译通过并运行了（默认是x64的，记得改为win32的来运行，因为我们上面配置的链接库是x86的）