## Vue
Hello , 我是小恒


### 文档
vue3

https://vuejs.org/guide/introduction.html

vue router

https://router.vuejs.org/zh/introduction.html

vuex

https://vuex.vuejs.org/zh/guide/


### 介绍
Vue 是一个框架和生态系统，涵盖了前端开发所需的大多数常见功能。但是网络是极其多样化的——我们在网络上构建的东西在形式和规模上可能会有很大差异。考虑到这一点，Vue 被设计为灵活且可增量采用。根据你的用例，Vue 可以以不同的方式使用：

无需构建步骤即可增强静态 HTML
作为 Web 组件嵌入到任何页面上
单页应用程序 （SPA）
全栈/服务器端渲染 （SSR）
Jamstack / 静态站点生成 （SSG）
面向桌面、移动、WebGL，甚至终端

一般结构
```angular2html
my-vue-project/
|-- src/
|   |-- assets/
|   |-- components/
|   |-- router/
|   |   |-- index.js
|   |-- views/
|   |   |-- Home.vue
|   |   |-- About.vue
|   |-- App.vue
|   |-- main.js
|-- public/
|   |-- index.html
|-- package.json

```

easybbs客户端前端资源文件结构
```angular2html
├───src/
│   ├───App.vue
│   ├───main.js
│   ├───assets/
│   │   ├───base.scss
│   │   ├───default_cover.png
│   │   ├───logo.svg
│   │   ├───icon/
│   │   │   ├───demo.css
│   │   │   ├───demo_index.html
│   │   │   ├───iconfont.css
│   │   │   ├───iconfont.js
│   │   │   ├───iconfont.json
│   │   │   ├───iconfont.ttf
│   │   │   ├───iconfont.woff
│   │   │   ├───iconfont.woff2
│   ├───components/
│   │   ├───AttachmentSelector.vue
│   │   ├───Avatar.vue
│   │   ├───Cover.vue
│   │   ├───CoverUpload.vue
│   │   ├───DataList.vue
│   │   ├───Dialog.vue
│   │   ├───EditorHtml.vue
│   │   ├───EditorMarkdown.vue
│   │   ├───ImageViewer.vue
│   │   ├───NoData.vue
│   ├───router/
│   │   ├───index.js
│   ├───store/
│   │   ├───index.js
│   ├───utils/
│   │   ├───Confirm.js
│   │   ├───Message.js
│   │   ├───Request.js
│   │   ├───Utils.js
│   │   ├───Verify.js
│   ├───views/
│   │   ├───Error404.vue
│   │   ├───Layout.vue
│   │   ├───LoginAndRegister.vue
│   │   ├───Search.vue
│   │   ├───forum/
│   │   │   ├───ArticleDetail.vue
│   │   │   ├───ArticleList.vue
│   │   │   ├───ArticleListItem.vue
│   │   │   ├───CommentImage.vue
│   │   │   ├───CommentList.vue
│   │   │   ├───CommentListItem.vue
│   │   │   ├───CommentPost.vue
│   │   │   ├───EditPost.vue
│   │   ├───ucenter/
│   │   │   ├───MessageList.vue
│   │   │   ├───Ucenter.vue
│   │   │   ├───UcenterEditUserInfo.vue
│   │   │   ├───UserIntegralRecord.vue
```