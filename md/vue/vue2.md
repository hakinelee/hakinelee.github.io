# Vue2 项目开发流程

## 1. 项目创建

```bash
vue create vue2-admin

# 安装依赖
yarn install

# 运行
yarn serve
```

## 2. 导入Element-ui

```bash
# 安装Element-ui
yarn add element-ui
```

```js
// main.js

// 完整引入ElementUI
// import ElementUI from 'element-ui';
// import 'element-ui/lib/theme-chalk/index.css';
// Vue.use(ElementUI);
```

> 按需引入：借助 babel-plugin-component，只引入需要的组件，以达到减小项目体积的目的

```bash
yarn add babel-plugin-component
```

```js
// main.js

// 按需引入ElementUI
import { Button, Select } from 'element-ui';
Vue.use(Button)
Vue.use(Select)
```

```js
// babel.config.js

module.exports = {
  presets: [
    '@vue/cli-plugin-babel/preset',
    ["@babel/preset-env", { "modules": false }]
  ],
  "plugins": [
    [
      "component",
      {
        "libraryName": "element-ui",
        "styleLibraryName": "theme-chalk"
      }
    ]
  ]
}
```

## 3. 引入Vue-router

```bash
yarn add vue-router@3.6.5
```

> 在一个模块化工程中使用，必须要通过 Vue.use() 安装路由功能

```js
// main.js

import VueRouter from 'vue-router'
Vue.use(VueRouter)
```

> 新建src/router目录，新建index.js，用于书写配置路由相关功能

```vue
<!-- App.vue -->

<template>
  <div id="app">
    <!-- 路由出口 -->
    <!-- 路由匹配到的组件将渲染在这里 -->
    <router-view></router-view>
  </div>
</template>
```

```js
// router/index.js

// 0. 如果使用模块化机制编程，导入Vue和VueRouter，要调用 Vue.use(VueRouter)
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter);

// 1. 创建 (路由) 组件，可以从其他文件 import 进来
//// 新建src/views目录，用于存放路由组件，新建Home.vue
import viewsHome from "@/views/viewsHome.vue";
//// 或者: import viewsHome from '../views/viewsHome.vue'
import viewsUser from "@/views/viewsUser.vue";


// 2. 定义路由：将路由与组件进行映射。
const routes = [
  { path: "/home", component: viewsHome },
  { path: "/user", component: viewsUser },
];


// 3. 创建router实例，然后传 `routes` 配置。
const router = new VueRouter({
  routes // (缩写) 相当于 routes: routes
})

// 4. 对外暴露router实例
export default router
```

```js
// 5. 创建和挂载根实例。
// main.js

// 引入VueRouter
import router from './router'
// 或者: import router from './router/index.js'

new Vue({
  router,
  render: h => h(App),
}).$mount('#app')
```

## 3.1 嵌套路由

> 新建views/viewsMain.vue文件

```js
// router/index.js

import viewsMain from "@/views/viewsMain.vue";

// 定义路由：将路由与组件进行映射
const routes = [
  // 主路由
  {
    path: '/', 
    component: viewsMain,
    children: [
      // 子路由
      { path: 'home', component: viewsHome },
      { path: 'user', component: viewsUser }
    ]
  }
];
```

```vue
<!-- App.vue -->

<template>
  <div id="app">
    <!-- 这里属于主路由出口 -->
    <router-view></router-view>
  </div>
</template>
```

```vue
<!-- viewsMain.vue -->

<template>
  <div class="">
    <h1>Main</h1>
    <!-- 这里是子路由出口 -->
    <router-view></router-view>
  </div>
</template>
```

## 4. eslint-disable

> 关闭eslint-disable

```js
// vue.config.js

const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  lintOnSave: false //关闭eslint校验
})
```

## 5. 整体UI的搭建

```vue
<!-- viewsMain  -->

<template>
  <div class="">
    <el-container>
      <el-aside width="200px">Aside</el-aside>
      <el-container>
        <el-header>Header</el-header>
        <el-main>
          <!-- 路由出口 -->
          <!-- 路由匹配到的组件将渲染在这里 -->
          <router-view></router-view
        ></el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import commonAside from "@/components/commonAside.vue";
export default {
  data() {
    return {};
  },
  components: {
    commonAside
  }
};
</script>
```

```js
// main.js

// 按需引入ElementUI
import { Aside, Button, Container, Header, Main, Menu, MenuItem, MenuItemGroup, Select, Submenu } from 'element-ui';

Vue.use(Aside)
Vue.use(Button)
Vue.use(Container)
Vue.use(Header)
Vue.use(Main)
Vue.use(Menu)
Vue.use(MenuItem)
Vue.use(MenuItemGroup)
Vue.use(Select)
Vue.use(Submenu)
```

> 封装公共组件: 新建src/components/commonAside.vue文件

```vue
<!-- commonAside  -->
<template>
  <div class="">
    <el-menu
      default-active="1-4-1"
      class="el-menu-vertical-demo"
      @open="handleOpen"
      @close="handleClose"
      :collapse="isCollapse"
    >
      <el-submenu index="1">
        <template slot="title">
          <i class="el-icon-location"></i>
          <span slot="title">导航一</span>
        </template>
        <el-menu-item-group>
          <span slot="title">分组一</span>
          <el-menu-item index="1-1">选项1</el-menu-item>
          <el-menu-item index="1-2">选项2</el-menu-item>
        </el-menu-item-group>
        <el-menu-item-group title="分组2">
          <el-menu-item index="1-3">选项3</el-menu-item>
        </el-menu-item-group>
        <el-submenu index="1-4">
          <span slot="title">选项4</span>
          <el-menu-item index="1-4-1">选项1</el-menu-item>
        </el-submenu>
      </el-submenu>
      <el-menu-item index="2">
        <i class="el-icon-menu"></i>
        <span slot="title">导航二</span>
      </el-menu-item>
      <el-menu-item index="3" disabled>
        <i class="el-icon-document"></i>
        <span slot="title">导航三</span>
      </el-menu-item>
      <el-menu-item index="4">
        <i class="el-icon-setting"></i>
        <span slot="title">导航四</span>
      </el-menu-item>
    </el-menu>
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      isCollapse: true,
    };
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
  },
};
</script>
  
<style scoped>
/*@import url(); 引入公共css类*/
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 200px;
  min-height: 400px;
}
</style>
```
