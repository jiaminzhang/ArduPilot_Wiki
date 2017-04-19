# 编译代码

```Tracker
新发布的版本代码编译方式已经改变，已经用waf工具替换了make。

在大多是情况下，waf和make在所描述的构建依赖关系是相同的，唯一更改的部分是waf的构建指令。

请参阅https://github.com/ArduPilot/ardupilot/blob/master/BUILD.md
```

以下链接的文章解释了如何在受支持的开发环境（Linux，Windows，Mac OSX）上为不同的目标硬件编译生成ArduPilot固件。附带的链接还包括建立地面站的代码。

## 固定翼(Plane), 多旋翼(Copter), 小车(Rover), 穿越机(Tracker) 

#### Windows 用户：

* [利用Bash在Windows10上编译](Dev/building-ardupilot-onwindows10.md)
* [利用make在Windows上编译](Dev/building-px4-with-make.md)
* [利用Eclipse在Windows上编译](Dev/editing-the-code-with-eclipse.md)
