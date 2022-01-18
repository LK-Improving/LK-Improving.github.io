---
title: React的Sass配置
date: 2022-01-18 13:24:42
tags: 
- React
categories:
- Web
- 前端开发
---
## 一、在已有项目下安装node-sass

```
npm install node-sass -D
```
有个小坑，node-sass版本不同对node的要求不一样。

Node 11 ----->  node-sass 4.10+, <5.0

Node 10 ---->  node-sass 4.9+, <6.0

Node 8   -----> node-sass 4.5.3+, <5.0

具体可查看[node-sass版本](https://www.npmjs.com/package/node-sass)

> 若要使用SASS MODULE，则需要将*.scss文件改为*.module.scss。
## 二、react中配置全局sass
### 1.安装sass

```
npm i sass-loader --save-dev
```

### 2.安装resource依赖

```
 npm install sass-resources-loader -D
```

### 3.安装完成后，发现通过create-react-app下载的脚手架项目没有webpack.config，这时去node_module下找react-scripts/config/webpack.config.js即为该项目的webpack文件，找到exclude: sassModuleRegex,修改如下即可完成全局配置公用样式

              {
				test: sassRegex,
              exclude: sassModuleRegex,
              use: getStyleLoaders(
                {
                  importLoaders: 3,
                  sourceMap: isEnvProduction
                    ? shouldUseSourceMap
                    : isEnvDevelopment,
                },
                'sass-loader'
              ).concat({
                loader:'sass-resources-loader',
                options:{
                  resources:[
                    // 按照文件路径填写
                    path.resolve('./src/styles/sassConfig.scss')
                  ]
                }
              }),
