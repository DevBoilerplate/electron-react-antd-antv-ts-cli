# electron-react-antd-antv-ts-cli

一个集成electron、react、antd、antv的ts版开发脚手架，便于快速搭建基于react开发的electron桌面应用

> EdeverClient可视化客户端便于更好的获取脚手架更新动态, 基于`electron-react-antd-antv-cli`构建! GitHub: [HerbertHe/EdeverClient](https://github.com/HerbertHe/EdeverClient/releases), Gitee: [HerbertHe/EdeverClient](https://gitee.com/HerbertHe/EdeverClient/releases)

## 环境依赖

* nodejs [未安装可参考](https://herberthe.gitee.io/2020/01/26/Nodejs%E5%AE%89%E8%A3%85%E8%8B%A5%E5%B9%B2%E9%97%AE%E9%A2%98%E9%81%BF%E5%9D%91/)
* yarn

> 关于electron的镜像，electron7.x之后需要设置单独的镜像，不然会安装报错；根据官方文档，中国地区镜像为: `https://cdn.npm.taobao.org/dist/electron/`

在Windows的环境下命令为:

```shell
npm config set ELECTRON_MIRROR="https://cdn.npm.taobao.org/dist/electron/"

# 验证设置
npm config ls

# 成功配置输出
ELECTRON_MIRROR="https://cdn.npm.taobao.org/dist/electron/"
```

## 更新记录

* 2020/03/16: 引入`.yarnclean`优化打包代码
* 2020/03/13: 新增完整的项目依赖云云

## 快速使用

* `clone` 仓库

```shell
# github
git clone https://github.com/HerbertHe/electron-react-antd-antv-ts-cli.git

# gitee
git clone https://gitee.com/HerbertHe/electron-react-antd-antv-ts-cli.git
```

* 进入仓库

* 下载依赖

```shell
yarn
```

* 验证安装

```shell
yarn run ele:dev
```

## 关于项目

查看项目从`package.json`开始，项目的`README.md`可能更新不及时

1. 已提供的指令

    ```shell
        "react:dev": "启动react的预览",
        "react:build": "构建react的产物",
        "react:test":  "react测试",
        "react:eject": "react-scripts eject",
        "ele:dev": "启动electron开发预览"
        "build:win64": "打包生成64位windows应用"
        # 下面详述包及自定义配置，目前只针对electron的开发做了脚本
    ```

    ```shell
        # 项目启动后在任何时间都可以在命令行输入rs回车使用nodemon强制项目更新
        rs
        # Ctrl + c后输入y即可退出命令行启动预览环境
    ```

2. 项目的默认包管理

    本项目默认使用`yarn`进行包管理

3. 项目依赖包详解

    * 项目中使用的开发依赖`react-app-rewired` `customize-cra` `babel-plugin-import` `less` `less-loader` `antd-dayjs-webpack-plugin` 全部基于 `antd`的[高级配置](https://ant.design/docs/react/use-with-create-react-app-cn)，没有使用`eject`对外暴露`webpack`来修改配置，使用了`react-app-rewired`的解决方案。`react-app-rewired`依赖`customize-cra`，对于自定义的webpack设置可以参考 [api](https://github.com/arackaf/customize-cra/blob/master/api.md) 获取使用所有`customize-cra`提供的API。配置文件为根目录的`config-overrides.js`

    * 项目的`dev`指令详解：`package.json`中对应指令为`nodemon --watch main.js --exec concurrently \"wait-on http://localhost:3000 && electron .\" \"cross-env BROWSER=none yarn start\"`，其中利用`nodemon`依赖监听`main.js`文件修改重载指令；`concurrently`并行`wait-on http://localhost:3000 && electron .`和`cross-env BROWSER=none yarn start`指令；`wait-on`依赖用于监听本地react服务的启动情况，当本地加载完成时执行`electron .`；`cross-env`利用了交叉环境设置环境变量`BROWSER=none`从而避免react自动启动浏览器预览

    * 项目自带了`antd`和`bizCharts`，提供了样式库和图形可视化的能力，`bizCharts`是阿里基于antv g2的React商业化封装，具体文档可参考下面的文档引用

4. 关于本项目打包的详解

    本项目使用`electron-builder`进行打包，第一次打包出现问题是必然的，下面的参考文章详细的记录了我配置打包文件的过程！

    * 你一定会遇到的错误（网络问题），参考这篇文章（Win10开发环境）[国内electron-vue build报错解决方法](https://juejin.im/post/5d102497e51d4556be5b3a74)，其实就是github下载慢的问题

        > 一定要自己去找最新版的`electron` `winCodeSign` `nsis` `nsis-resources`

    * 如何使用？我这个项目你直接跑就可以了`yarn build:win64`
    * 配置文件参考官方文档[electron-builder](https://www.electron.build/configuration/configuration)

## 打包更新信息

> 请参考`electron-react-antd-antv-cli`的**打包优化参考建议**

## 参考文档

* [在`create-react-app`中使用](https://ant.design/docs/react/use-with-create-react-app-cn)
* [react-app-rewired](https://github.com/timarney/react-app-rewired#alternatives)
* [customize-cra](https://github.com/arackaf/customize-cra)
* [bizCharts](https://bizcharts.net/index)
* [Ant Design of React](https://ant.design/docs/react/introduce-cn)
* [electron](https://www.electronjs.org/docs)
* [electron-builder](https://www.electron.build/configuration/configuration)
