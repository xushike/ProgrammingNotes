# vue
## 一 概述
## 三 基础
## 五 问题
### 1 带整理
#### 异步加载模块
vue中异步加载模块只需要将`import Foo from './Foo.vue'`改成`const Foo = () => import('./Foo.vue')`