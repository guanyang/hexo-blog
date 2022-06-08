## hexo-blog

### 概览
- 该博客基于`hexo`博客框架创建
- 个人博客网址：https://note.xcloudapi.com
- 个人网站：https://www.xcloudapi.com

### 写博客
- 定位到我们的hexo根目录，执行命令

```
hexo new 'my-first-blog'
```
- hexo会帮我们在_posts下生成相关md文件，我们只需要打开这个文件就可以开始写博客了

### 常用命令

```
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #部署到GitHub
hexo help  # 查看帮助
hexo version  #查看Hexo的版本
```

#### 缩写

```
hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy
```

#### 组合命令

```
hexo s -g #生成并本地预览
hexo d -g #生成并上传
```

### 参考文档
- 参考主题：https://github.com/dusign/hexo-theme-snail
- 官方文档：https://hexo.io/zh-cn/docs/