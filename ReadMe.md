- [README 中文](./ReadMe_zh.md)
- [README English](./ReadMe.md)

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

Advantages of This Fork Compared to the Original Repository
---------

- **Robust Decompilation for Lua 5.2/5.3**: This fork introduces robust decompilation support for Lua versions 5.2 and 5.3, specifically targeting bytecode with stripped debug information. Previous versions of the tool would crash under these conditions, but with this update, decompilation is stable and reliable.


Overview
========

LuaDec is a Lua decompiler for lua 5.1 , and experimental for lua 5.2 and 5.3.

It is based on Hisham Muhammad's luadec which targeted lua 5.0.x and LuaDec51 by Zsolt Sz. Sztupak.

LuaDec is free software and uses the same license as the original LuaDec.


Compiling
---------
```
git clone https://github.com/zhangjiequan/luadec
cd luadec
git submodule update --init lua-5.1
cd lua-5.1
make linux
cd ../luadec
make LUAVER=5.1
```

If you want to build it for lua 5.2 or 5.3 , just replace 5.1 above to 5.2 or 5.3. You can also compile using tools like mingw32-make. For example:

```
git clone https://github.com/zhangjiequan/luadec
cd luadec
git submodule update --init lua-5.3
cd lua-5.3
mingw32-make mingw
cd ../luadec
mingw32-make LUAVER=5.3
```

There are also project files for vc2008, tested for vc2008 and vc2013.  

Before compiling, make sure there are correct sources in lua-5.1 , lua-5.2 or lua-5.3.


Usage
-----
* decompile lua binary file:  
  luadec abc.luac  
* decompile lua source file for testing and comparing:  
    luadec abc.lua  
* disassemble lua source or binary  
    luadec -dis abc.lua  
* -pn print nested functions structure, could be used by -fn  
```
luadec -pn test.lua
0
  0_0
    0_0_0
  0_1
```
* -f decompile only specific nested function  
    luadec -f 0_1 test.lua  
* -ns donot process sub functions  
    luadec -ns -f 0_1 test.lua  
* -fc perform a instruction-by-instruction compare for each function  
    luadec -fc test.lua  
outputs:  
-- function check pass 0  
-- function check fail 0_0 : cannot compile  
-- function check fail 0_1 :  different code size; sizecode org: 66, decompiled: 67, same: 47;   

There are some more options, usually for debug purposes, or for cases where the built in local guesser guesses wrong.
Use -h to get a complete list of usable parameters


Credits
-------

Original by Hisham Muhammad (http://luadec.luaforge.net)
 
Ongoing port to Lua 5.1 by Zsolt Sz. Sztupak (https://github.com/sztupy/luadec51/)

The internals of Lua5.1 was learned from Kein-Hong Man's A No-Frills Introduction to Lua 5.1 VM Instructions
