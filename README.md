# vue-vant-project

>  基于vue+vant的项目模板

# web移动端项目框架 vue-cli3 + vant 
 
## Project setup

```javascript

npm install

```

### Compiles and hot-reloads for development

```javascript

npm run development

```

### Compiles and minifies for production

```javascript

npm run build

```

### Run your tests

```javascript

npm run test

```

### Lints and fixes files

```javascript

npm run lint

```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).

```javascript

├── dist                       // 生产打包目录  
├── dist_test                  // 测试打包目录  
├── dist_development           // 开发环境打包目录
├── src                        // 源代码
│   ├── api                    // 所有请求
│   ├── assets                 // 主题 字体等静态资源
│   ├── components             // 全局公用组件
│   ├── mock                   // 项目mock 模拟数据
│   ├── router                 // 路由
│   ├── store                  // 全局 store管理
│   ├── utils                  // 全局公用方法
│   ├── vendor                 // 公用vendor
│   ├── views                  // view
│   ├── App.vue                // 入口页面
│   └── main.js                // 入口 加载组件 初始化等
│
├── public                     // 公共资源路径
│   ├── favicon.ico            // favicon图标
│   ├── xhDetection.html       // xhDetection.html
│   └── index.html             // index.html
├── .babelrc                   // babel-loader 配置
├── .eslintrc.js               // eslint 配置项
├── .gitignore                 // git 忽略项
├── .env.development           // 开发环境打包配置
├── .env.test                  // 测试环境打包配置
├── .env.production            // 生产环境打包配置
├── favicon.ico                // favicon图标
├── vue.config.js              // vue-cli 3.0 配置文件
├── package-lock.json          // package-lock.json
└── package.json               // package.json

```


### 新增项目配置流程

```javascript

1.修改 vue.config.js 配置文件
- pages选项新增项目相关配置
- 参照现有项目

```

### 版本说明：A.B.C

* A 主版本号：功能模块有大的变动，比如增加多个模块或者整体架构发生变化。

* B 子版本号：当功能有一定的增加或变化，比如增加了对权限控制、增加自定义视图等功能。此版本号由项目决定是否修改。

* C 阶段版本号：一般是 Bug 修复或是一些小的变动，要经常发布修订版，时间间隔不限，修复一个严重的bug即可发布一个修订版。此版本号由项目经理决定是否修改。

-----------------------------------

### version 1.1.2 20190530

* 版本1说明信息还是完整报告，都要显示的修改

-----------------------------------

### version 1.1.0

* 版本1说明
