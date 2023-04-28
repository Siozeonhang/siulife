---
title: "11111111111111111111111"
datePublished: Fri Apr 28 2023 17:20:25 GMT+0000 (Coordinated Universal Time)
cuid: clh0tkt9r000009mhdsdf0a2j
slug: 11111111111111111111111

---

# **创建 github 仓库，存放博客代码和内容**

## **0\. 创建代码仓库，可以选择私有的或公开**

![image.png](https://midqiu.deno.dev/images/2665960666-637b427a9553e_fix732.png align="left")

项目按照你的需要填你自己起的名字。 可以选择`Private`，也可以选`Public`，选择`Public`的话，别人就能看到你的代码仓库里面的内容，注意不要放些敏感内容。

## **1\. 配置博客相关信息**

> 一个小技巧：在github 的仓库主页，按句号`.`对应的按键，可以用github的在线编辑器打开此仓库，可以直接在线编辑提交到代码仓库。

在项目根目录下创建一个名为`main.tsx`的文件，文件内容如下（根据需要改成你的相关信息）：

```plaintext
import blog from "https://deno.land/x/blog/blog.tsx";

blog({
  author: "Dino",
  title: "My Blog",
  description: "The blog description.",
  avatar: "https://deno-avatar.deno.dev/avatar/83a531.svg",
  avatarClass: "rounded-full",
  links: [
    { title: "Email", url: "mailto:bot@deno.com" },
    { title: "GitHub", url: "https://github.com/denobot" },
    { title: "Twitter", url: "https://twitter.com/denobot" },
  ],
  lang: "zh",
});
```

更多详细设置，看 [deno\_blog 文档](https://deno.land/x/blog)

## **2\. 创建博客内容**

创建文件夹`posts`，注意，这个文件夹名字固定是这个;然后在文件夹中创建第一篇博客，比如这里创建了一个名为`hello_world.md`，的文件作为第一篇博客(注意：文件名称不要有空格和中文)，内容如下：

```plaintext
---
title: 第一篇博客
publish_date: 2022-11-20
tags: ['hello-world']
---

这是我的第一篇博客！这里是博客内容
```

将内容推送到 github 的代码仓库中。

# **在Deno Deploy 平台创建项目，并绑定github 上的仓库**

1. 选择 `Sign Up`注册或 `Sign In`登录。按提示使用github账号登录就行了。
    
2. 进入到管理台，点击 New Project 按钮创建新的项目。
    
3. 依次选择，对应的代码仓库-分支-构建方式（Automatic）-入口文件（main.tsx），并设置**name**，然后点击 `Link`按钮创建项目。
    

> 注意：如果**name**是aaa，那么最终的博客的访问域名是 [`https://aaa.deno.dev`；可以到设置里面修改。当然你可以在设置中配置绑定自己的域名如](https://aaa.deno.dev；可以到设置里面修改。当然你可以在设置中配置绑定自己的域名如) [aaa.com](http://aaa.com) 等。这里就不做说明了。

![image.png](https://midqiu.deno.dev/images/3856422827-637b453460be7_fix732.png align="left")

# **更新、新增博客**

在`posts`文件下，新增一篇`.md`结尾的文件，内容格式参考上面的例子。（我们这个博客系统会自动扫描`posts`文件夹里面的md文件解析成博客内容的。）

更新博客的话，就修改相应的 `.md`文件的内容。

然后将改动推送到github 的代码仓库里，等个十几秒，Deno Deploy会自动构建成功，刷新博客地址就能看到新的内容了。

# **其他**

下面是网站在国内的测速：

![image.png](https://midqiu.deno.dev/images/1696267530-637b49e93260e_fix732.png align="left")

此教程使用的 Deno 官方出的 blog 库，优点是简单，默认主题简洁好看。此外，Deno官方还写了一篇如何将 最流行的博客系统 `Hugo` 部署到Deno Deploy上的文章，`Hugo`功能更强大一些，不过部署起来要稍微麻烦一点，感兴趣的可以看[这里](https://deno.com/blog/hugo-blog-with-deno-deploy)