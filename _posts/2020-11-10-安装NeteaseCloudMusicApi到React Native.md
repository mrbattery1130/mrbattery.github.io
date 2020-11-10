# 安装`NeteaseCloudMusicApi`到`React Native`

## 创建RN工程

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

## 移植`NeteaseCloudMusicApi`代码

1. 下载`NeteaseCloudMusicApi`代码；
2. 复制`NeteaseCloudMusicApi-master`根目录下`module`、`module_example`、`plugin`、`test`、`util`、`main.js`到项目根目录；
3. 复制`NeteaseCloudMusicApi-master`根目录下`package.json`中`dependencies`和`devDependencies`节点下内容到项目根目录下`package.json`中。

## 安装依赖

1. 运行`yarn install`安装`package.json`中的依赖；
2. `React Native`不包含 `nodejs`部分基本库 ，使用`rn-nodeify`添加 `nodejs` 核心模块：
   - 安装`rn-nodeify`：`npm i --save-dev rn-nodeify@latest`
   - 在`package.json`中`script`下添加`"postinstall": "rn-nodeify --install fs,dgram,process,path,console --hack"`

3. 

## 运行RN项目

1. 
