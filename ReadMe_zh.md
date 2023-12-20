- [README 中文](./README_zh.md)
- [README English](./README.md)

![Last Commit](https://img.shields.io/github/last-commit/zhangjiequan/luadec?style=flat-square)
[![Open Issues](https://img.shields.io/github/issues-raw/zhangjiequan/luadec?style=flat-square)](https://github.com/zhangjiequan/luadec/issues)
![Contributors](https://img.shields.io/github/contributors/zhangjiequan/luadec?style=flat-square)
![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen?style=flat-square)

[![](https://img.shields.io/github/downloads/zhangjiequan/luadec/total?style=flat-square)](https://github.com/zhangjiequan/luadec/releases)
[![](https://img.shields.io/github/downloads/zhangjiequan/luadec/latest/total?style=flat-square)](https://github.com/zhangjiequan/luadec/releases/latest)
[![](https://img.shields.io/github/v/release/zhangjiequan/luadec?style=flat-square)](https://github.com/zhangjiequan/luadec/releases/latest)

[![GitHub watchers](https://img.shields.io/github/watchers/zhangjiequan/luadec?style=flat-square)](https://github.com/zhangjiequan/luadec/watchers)
[![GitHub forks](https://img.shields.io/github/forks/zhangjiequan/luadec?style=flat-square)](https://gitpop2.vercel.app/zhangjiequan/luadec)
[![GitHub stars](https://img.shields.io/github/stars/zhangjiequan/luadec?style=flat-square)](https://github.com/zhangjiequan/luadec/stargazers)

![Platform](https://img.shields.io/badge/platform-windows-lightgrey?style=flat-square)
[![License](https://img.shields.io/github/license/zhangjiequan/luadec?style=flat-square)](./LICENSE)

[![Github CI Status](https://github.com/zhangjiequan/luadec/actions/workflows/build.yml/badge.svg)](https://github.com/zhangjiequan/luadec/actions)

![Custom](https://img.shields.io/badge/zhangjiequan-Jackie@Baioo-green)

与原始仓库相比，此Fork的优势
---------

- **针对Lua 5.2/5.3的强大反编译支持**：此分支为Lua 5.2和5.3版本引入了强大的反编译支持，特别是针对已剥离调试信息的字节码。在此更新之前，工具在这些条件下会崩溃，但有了这次更新，反编译变得稳定且可靠。


概览
====

LuaDec 是一个针对 Lua 5.1 的反编译器，并且对 Lua 5.2 和 5.3 也有实验性支持。

它基于 Hisham Muhammad 的 luadec（针对 Lua 5.0.x）和 Zsolt Sz. Sztupak 的 LuaDec51。

LuaDec 是自由软件，并采用与原始 LuaDec 相同的许可证。


编译
-----
```
git clone https://github.com/zhangjiequan/luadec
cd luadec
git submodule update --init lua-5.1
cd lua-5.1
make linux
cd ../luadec
make LUAVER=5.1
```

如果你想为 Lua 5.2 或 5.3 构建它，只需将上面的 5.1 替换为 5.2 或 5.3。你也可以使用mingw32-make之类的工具来编译。例如：

```
git clone https://github.com/zhangjiequan/luadec
cd luadec
git submodule update --init lua-5.3
cd lua-5.3
mingw32-make mingw
cd ../luadec
mingw32-make LUAVER=5.3
```

这里还有 vc2008 的项目文件，已经过 vc2008 和 vc2013 的测试。

编译之前，请确保文件夹 lua-5.1、lua-5.2 或 lua-5.3 中有正确的源文件。


使用
----
* 反编译 Lua 二进制文件：  
  luadec abc.luac  
* 反编译 Lua 源文件，为了测试和比较：  
    luadec abc.lua  
* 反汇编 Lua 源文件或二进制文件  
    luadec -dis abc.lua  
* -pn 打印嵌套函数结构，加参考 -fn  
```
luadec -pn test.lua
0
0_0
0_0_0
0_1
```
* -f 只反编译特定嵌套函数  
    luadec -f 0_1 test.lua  
* -ns 不处理子函数  
    luadec -ns -f 0_1 test.lua  
* -fc 对每个函数执行指令对指令的比较  
    luadec -fc test.lua  
outputs:  
-- function check pass 0  
-- function check fail 0_0 : cannot compile  
-- function check fail 0_1 :  different code size; sizecode org: 66, decompiled: 67, same: 47;   

还有一些更多的选项，通常用于调试目的，或者用于内置的局部猜测器猜错的情况。
使用 -h 来获取完整的可用参数列表


鸣谢
-----

最初由 Hisham Muhammad (http://luadec.luaforge.net) 创建
 
由 Zsolt Sz. Sztupak 持续移植到 Lua 5.1 (https://github.com/sztupy/luadec51/)

Lua5.1 的内部机制是通过 Kein-Hong Man 的《Lua 5.1 VM 指令简介》学习的