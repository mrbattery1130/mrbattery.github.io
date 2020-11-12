---
layout:     post
title:      安装NeteaseCloudMusicApi到React Native
subtitle:   
date:       2020-11-10
author:     电池君
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - Blog
---

# 创建RN工程

// 1. 使用`WebStorm`新建`React Native`工程；

1. 新建文件夹，用VS Code打开文件夹；

2. 安装`create-react-native-app`；

   - ``npm install -g create-react-native-app`

   - 使用`create-react-native-app --version`检测版本

3. 创建项目；

   - `create-react-native-app projectName`

   - 安装时选择`How would you like to start » Default new app`

4. 安装`Expo`；

   - `npm install -g expo`；

5. 尝试修改根目录 `App.js` ，并通过`Expo`连接手机调试程序；

   - `cd projectName`
   - ` expo start`

# 移植`NeteaseCloudMusicApi`代码

1. 下载`NeteaseCloudMusicApi`代码；
2. 复制`NeteaseCloudMusicApi-master`根目录下`module`、`module_example`、`plugin`、`test`、`util`、`main.js`到项目根目录；
3. 复制`NeteaseCloudMusicApi-master`根目录下`package.json`中`dependencies`和`devDependencies`节点下内容到项目根目录下`package.json`中。

# 安装依赖

1. 运行`yarn install`安装`package.json`中的依赖；
2. `React Native`不包含 `nodejs`部分基本库 ，使用`rn-nodeify`添加 `nodejs` 核心模块；
   - 安装`rn-nodeify`：`npm i --save-dev rn-nodeify@latest`
   - 在`package.json`中`script`下添加`"postinstall": "rn-nodeify --install fs,dgram,process,path,console --hack"`
   - install all shims and run package-specific hacks：`rn-nodeify --install --hack`
   - `rn-nodeify --install "http,stream,path,net,tls,crypto,https,fs,zlib,dns,vm,dgram,os，constants，asyncstorage-down" --hack`
3. 修改main.js引入依赖；
   ```js
   import { readdirSync } from 'fs'
   import { join } from 'path'
   import request from './util/request'
   import { cookieToJson } from './util/index'
   ```
   
   ```js
    let fileModule = requirejs(join(__dirname, 'module', file))
   ```
   
// 4. 安装`asyncstorage-down`；
//   - `yarn add asyncstorage-down`
 
# 运行RN项目

1. 确保你的设备已经成功连接。可以输入adb devices来查看:
   ```
   $ adb devices
   List of devices attached
   emulator-5554 offline   # Google模拟器
   14ed2fcc device         # 真实设备
   在右边那列看到device说明你的设备已经被正确连接了。注意，你只应当连接仅仅一个设备。
   ```
   > 如果你连接了多个设备（包含模拟器在内），后续的一些操作可能会失败。拔掉不需要的设备，或者关掉模拟器，确保`adb devices`的输出只有一个是连接状态。

2. 运行react-native run-android来在设备上安装并启动应用了。
   - 译注：在真机上运行时可能会遇到白屏的情况，请找到并开启悬浮窗权限。

3. 启用开发服务器，可以快速的迭代修改应用，然后在设备上查看结果
   > 大部分现代的安卓设备已经没有了硬件"Menu"按键，这是我们用来调出开发者菜单的。在这种情况下你可以通过摇晃设备来打开开发者菜单(重新加载、调试，等等……)
   > (Android 5.0及以上)使用adb reverse命令
   > 首先把设备通过USB数据线连接到电脑上，并开启USB调试
   - 运行`adb reverse tcp:8081 tcp:8081`
   - 使用`Reload JS`和其它的开发选项
