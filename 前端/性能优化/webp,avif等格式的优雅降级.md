# WebP介绍

> 欢迎转载，转载请标明文章出处来自[字节架构前端] [WebP](https://link.juejin.cn?target=https%3A%2F%2Fdevelopers.google.com%2Fspeed%2Fwebp "https://developers.google.com/speed/webp") 是 Google 推出的一种同时提供了有损和无损两种压缩方式的图片格式，优势体现在其优秀的图像压缩算法，能够带来更小的图片体积，同时拥有更高的的图像质量。根据官方说明，WebP 在无损压缩的情况下能比 PNG 减少26%的体积，有损压缩的情况能比 JPEG 减少25%-34%的体积。

下图可以看出，相对于传统的图片格式，WebP 格式存在浏览器兼容性方面的问题。本文通过工程化的手段来实现 WebP 格式的自适应加载。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/057db265fd2342c9814abbf6fe0eaea9~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)
# 传统做法

为了在前端项目里用上 WebP 格式，并且兼容不支持该格式的浏览器，通常的做法是判断浏览器支持性，引入 WebP 图片或其他通用格式的图片。针对HTML、JS、CSS 三种引入图片的场景，有以下几种处理方式：

## HTML

借助 标签自适应加载的特性，如下，WebP 格式放在 标签，用JPEG、PNG等通用格式做兜底。

```html
<picture>
  <source srcSet="https://p3-imagex.byteimg.com/imagex-rc/preview.jpg~tplv-19tz3ytenx-147.webp" type="image/webp" />
  <img decoding="async" loading="lazy" src="https://p3-imagex.byteimg.com/imagex-rc/preview.jpg~tplv-19tz3ytenx-147.jpeg" />
</picture>

```
