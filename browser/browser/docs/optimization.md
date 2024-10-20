## 资源优化

### URL资源 ：
如第三方库CDN调用以及高像素图片等URL资源，也就是负担，
如果URL资源加载速度慢，特别是获取超时会使得浏览器加载过10000ms以上
通过开发者工具排查即可

## 前端代码
减少HTTP请求：
合并CSS和JS文件，减少单独的文件请求。
使用雪碧图（CSS sprites）合并多个小图标。
启用浏览器缓存。
压缩和优化资源：
使用Gzip压缩HTML、CSS和JS文件。
优化图片大小，使用WebP等高效格式。
移除不必要的空格、注释和代码。
使用CDN加速：
将静态资源部署到CDN上，利用边缘节点加速资源加载。
代码优化：
避免使用过多的内联CSS和JS。
优化选择器性能，避免使用过于复杂的CSS选择器。
精简DOM操作，减少重绘和回流。
异步加载：
使用异步加载（如<script async>或<script defer>）来加载脚本，避免阻塞页面渲染。
利用Web Workers处理耗时任务，不阻塞主线程。
响应式设计：
使用媒体查询和百分比布局实现响应式网站设计。
优化移动端体验，如视口设置、触摸友好元素等。
预加载和预取技术：
使用<link rel="preload">预加载关键资源。
利用<link rel="prefetch">预取可能需要的资源。
懒加载：
对图片、视频等媒体内容实施懒加载，仅在用户需要时加载。
Web字体优化：
选择适当的字体格式，减少字体文件大小。
使用font-display属性控制字体的加载行为。
性能监控和分析：
使用性能分析工具（如Chrome DevTools、Lighthouse等）监控网站性能。
分析并解决性能瓶颈。
安全性增强：
使用HTTPS协议加密通信。
防止跨站脚本攻击（XSS）和跨站请求伪造（CSRF）。
SEO优化：
优化页面标题、描述和关键词。
使用语义化的HTML标签。
提高网站的加载速度，因为搜索引擎会考虑这一因素


