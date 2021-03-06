---
title: "Hugo自动化部署"
date: 2022-05-10T17:31:09+08:00
lastmod: 2022-05-10T17:31:09+08:00
draft: false
keywords: ["Hugo", "Github Action", "GitHub Pages"]
description: "使用 Github Action 持续集成工具，自动将博客部署至 GitHub Pages 或 云服务中。"
categories: ["GitHub"]
author: "caviare"
weight: 998
---

使用 Github Action 持续集成工具，自动将博客部署至 GitHub Pages 并且同步至云服务中。

<!--more-->

---


## 前期准备

我们需要一个能够在本地正常运行的由[Hugo](https://gohugo.io/)搭建的博客。


## 自动部署至 GitHub Pages

1. 创建一个 GitHub Pages 仓库。

2. 格式必须为 [你的GitHub名称].github.io，示例如图：

    ![image.png](https://s2.loli.net/2022/05/13/L7GEc5kPHFT2dzt.png)

    **仓库一定要选 Pubilic 公开**

    主干分支的代码被 GitHub Action 用来构建站点， GitHub Action 会自动生成gh-pages分支，并且构建博客最终显示的静态站点内容。 gh-pages的分支才是我们网页显示的内容，我们可以在`[你的GitHub名称].github.io`看到你的博客内容。

3. **如果我们的博客主题是通过`git pull`到`themes/*`文件夹下的我们需要添加`.gitmodules`文件来标注Git子模块，示例如图：**

    ![image.png](https://s2.loli.net/2022/05/12/Int23kSiQ6pw8h4.png)

    我采用的是[even](https://github.com/olOwOlo/hugo-theme-even)主题，通过`git pull`的方式直接拉取至`theme`的目录下的，方便以后更新主题，如果是文件直接放进去的话可以不需要这一步操作。


4. **配置GitHub Action 工作流**

    在仓库根目录创建工作流配置文件，路径为：`.github\workflows\gh-pages.yml`， 

    配置如下：

    ```yml
    name: GitHub Pages

    on:
    push:
        branches:
        - main # Set a branch to deploy
    pull_request:

    jobs:
    deploy:
        runs-on: ubuntu-20.04
        concurrency:
        group: ${{ github.workflow }}-${{ github.ref }}
        steps:
        - uses: actions/checkout@v3
            with:
            submodules: true # Fetch Hugo themes (true OR recursive)
            fetch-depth: 0 # Fetch all history for .GitInfo and .Lastmod

        - name: Setup Hugo
            uses: peaceiris/actions-hugo@v2
            with:
            hugo-version: "latest"
            extended: true

        - name: Build
            run: hugo --minify

        - name: Deploy
            uses: peaceiris/actions-gh-pages@v3
            if: ${{ github.ref == 'refs/heads/main' }}
            with:
            github_token: ${{ secrets.GITHUBTOKEN }}
            publish_dir: ./public
    ```

    如果你的主干分支主干分支不是master 是 main 需要将配置的`refs/heads/mai`修改为`refs/heads/master`

    设置完成后把本地仓库push至github就会可以自动运行 GitHub Action 啦。

    如果脚本运行失败，并且你并没有用到`.gitmodules`这步操作可以试图删除`actions/checkout@v3`这一段配置后再push一遍代码看看。 

    **配置中的`GITHUBTOKEN`你可以把它认为是一个变量，我们需要在仓库的 settings 里找到 Secrets 下的 Actions 然后点击 New repository secret 生成一个名字叫`GITHUBTOKEN`的变量。**

    ![image.png](https://s2.loli.net/2022/05/13/ytfASRbYxp1Faek.png)

    我们可以在这个[github.com/settings/tokens](https://github.com/settings/tokens)页面设置我们的`GITHUBTOKEN`，如下图设置生成完后，记得要将令牌的值复制到`repository secret`中。

   ![1652373719_1_.jpg](https://s2.loli.net/2022/05/13/YAIW9KnXu7iOL2D.png)

    

## 自动部署至服务器

如果你并且还需要将代码同步至服务器，其实逻辑很简单，我们只需要先在服务器中将仓库 git clone 到服务器然后将分支切换至`gh-pages`, 每次触发 Git Action 时追加一个连接ssh至服务器，进入到站点目录执行 git pull 的操作就可以， 配置如下：

```yml
    name: GitHub Pages
    on:
    push:
        branches:
        - main # Set a branch to deploy
    pull_request:

    jobs:
    deploy:
        runs-on: ubuntu-20.04
        concurrency:
        group: ${{ github.workflow }}-${{ github.ref }}
        steps:
        - uses: actions/checkout@v3
            with:
            submodules: true # Fetch Hugo themes (true OR recursive)
            fetch-depth: 0 # Fetch all history for .GitInfo and .Lastmod

        - name: Setup Hugo
            uses: peaceiris/actions-hugo@v2
            with:
            hugo-version: "latest"
            extended: true

        - name: Build
            run: hugo --minify

        - name: Deploy
            uses: peaceiris/actions-gh-pages@v3
            if: ${{ github.ref == 'refs/heads/main' }}
            with:
            github_token: ${{ secrets.GITHUBTOKEN }}
            publish_dir: ./public
        - name: Deploy server
            uses: appleboy/ssh-action@master
            with:
            host: ${{ secrets.HOST }}
            username: ${{ secrets.USERNAME }}
            password: ${{ secrets.PASSWORD }}
            port: ${{ secrets.PORT }}
            script: |
                cd ${{secrets.SITEPATH}}
                git pull
```

`HOST`: 服务器IP地址

`USERNAME`: ssh用户名

`PASSWORD`: 用户密码

`PORT`: ssh端口

`SITEPATH`: 站点目录，绝对路径。

这些变量直接在`repository secret`中设置就可以了。

![image.png](https://s2.loli.net/2022/05/13/dtm8VebqZEjYXDc.png)



