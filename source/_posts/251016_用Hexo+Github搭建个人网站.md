---
title: 用 Hexo + Github 搭建个人网站
categories:
  - Software
tags:
  - Hexo
  - Github
  - Website
---

- 本文将指导你搭建你的第一个网站。
- 示例系统：Windows 10 专业工作站版 22H2
- ~~喜报：2025年10月15日，Windows 10 终于失去了 Microsoft 的支持，完成了其成为一个优秀操作系统的最后一步。~~
## 环境配置
### 软件安装
- 下载并安装 [Node.js](https://nodejs.org/en/download) ，自带 npm (Node Package Manager) ：
![npm 下载页面](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510171545543.png)
- 下载并安装 [Git](https://git-scm.com/downloads) ：
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221642815.png)
回到桌面点击右键，点击 **Open Git Bash Here**。
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221642844.png)
依次输入下列各行代码：
```bash
node --version
npm -v
git -v
```
如果均弹出版本号信息，则安装成功。
- 安装 **hexo**，继续输入下列代码：
```bash
npm install hexo-cli -g
```
安装完成后输入代码校验：
```bash
hexo -v
```
- 安装 [Webstorm](https://www.jetbrains.com/webstorm/) ：
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221642915.png)
这是一个包含终端，设计、编辑网站，编辑、上传博客等功能的全能 IDE。之后对网站的所有操作都在这里进行。
### 文件夹初始化
在 D 盘或其他数据盘中新建文件夹，名称 **hexo_blog** （随意取名），未来所有的网站文件都会储存在这里。打开 hexo_blog 文件夹，文件夹空白处点击右键再次打开 **Git Bash**，输入代码对当前文件夹初始化：
```bash
hexo init 
```
这个操作将会从 **Github** 拷贝文件，所以必要时可以连接 VPN。若成功初始化则提示：
```bash
INFO  Start blogging with Hexo!
```
会发现文件夹多出来很多内容：
- public 最终所见网站的所有内容
- node_modules 所有插件以及模块
- _config.yml 站点配置文件，在这里更改网站主题
- package.json 配置 hexo 运行所需 js 包
- scaffolds 模板文件夹，包含对应模板内容
- themes 主题文件，下载的主题在这里，hexo 官网提供 [427 个主题](https://hexo.io/themes/)
- source 存放用户资源，博客正文、图片、头像等等
## 网站配置
### 本地网站
在 **Webstorm** 内打开 hexo_blog 文件夹，打开左下角的 Terminal（终端）
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221643242.png)
之后所有的终端命令都可以在这里执行，输入 hexo 命令：
```bash
hexo s
```
[查看更多的 hexo 命令](https://hexo.io/docs/commands)。 这里的`hexo s`是`hexo server`的简写，类似的也可以用`hexo g`代替`hexo generate`。
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221644419.png)
点击生成的网站，这就是一个简单的本地网站，默认是 hexo 内置主题 **landscape** ：
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221644154.png)
### 更换主题
如果不喜欢可以去 hexo 官网 [下载其他主题](https://hexo.io/themes/)。
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221644220.png)
例如我们这里选择第二个主题 Webstack，点击标题进入主题的 Github 页面，下拉找到 README，按照给出的命令回到 Webstorm 安装即可。
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221645428.png)
安装完主题后，在 Webstorm 左侧找到 themes 文件夹，展开可以看到下载好的主题，如果找不到则重新回去查看 Readme，看作者把他放哪去了：
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221645434.png)
之后安装 **pug** 以及 **stylus** 的渲染器：
```bash
npm install hexo-renderer-pug hexo-renderer-stylus --save
```
打开 _config.yml 文件，这是站点配置文件，拉到最下面：
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221646350.png)
这里的 theme 项可以更改不同的主题：
```bash
theme : landscape
```
把 landscape 改为 webstack，下载新主题后还可能会有 _config.主题名.yml 文件，这是主题配置文件，主题配置文件的部分设置会覆盖站点配置文件。主题相当于框架，按照 Readme 这个指导书来改造主题变成你喜欢的样子。
### 建立图床
所谓图床，就是将博客中的所有的图片都存储到某个网络空间，这样他人在阅览博客时也会访问这些网络空间从而显示图片。这里用 Github + PicGO 建立图床。在 Github 建立一个公开仓库存放图片，用 PicGO 软件能够方便地将本地图片上传到 Github 并生成 Markdown 格式的图片链接。
#### Github
创建 Github 账户，点击头像，选择第三个选项 **Repositories**：
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221646364.png)
点击 **New** 新建仓库，仓库名字可以设为 blogimage，可见性选择 Public 公开，不然他人无法访问，添加 README，这会自动创建一个 Banch 分支：
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221646568.png)
然后点击 Create Repository。自动进入仓库的 Code 页面：
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221647952.png)
进入与 Code 平行的 Settings 页面，左侧菜单栏下滑到底，点击 Developer Settings 创建 Personal Access Tokens (Classic)，注意这里要勾选所有 repo 选项，其他的不勾选，点击 Generate token 后，记得额外保存 token ，因为这个页面关闭后将不再展示 token ，丢失 token 后只能删除仓库新建一个了。
#### PicGO
Token 用于 PicGO 的访问，[官网下载PicGO](https://github.com/Molunerfinn/PicGo/releases)。
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221647623.png)
配置左侧的 Github 图床，仓库名填写`Github账号名/仓库名`，分支一般是 main，Token 就是上文生成的，存储路径不必填写，自定义域名填写：
```bash
https://cdn.jsdelivr.net/gh/Github账号名/仓库名
```
之后打开 PicGo 设置，确认 PicGo Server 的设置：
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510171950636.png)
其他的设置就按自己喜好来。设置完后可以自己尝试上传一张图片测试，如果上传失败，可以打开 PicGo 设置 -> **设置日志文件** -> 点击打开，来查看日志
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510171954717.png)
拉到最下面，会有报错代码，有比如 409，411，423 等等，Google 一下报错原因就很容易解决。
### 在线网站
Github 提供了 Github Pages 功能，可以免费建立 Github 网页，这里可以直接看官方教程：[Quickstart for GitHub Pages](https://docs.github.com/en/pages/quickstart) 。
以及创建一个 SSH Key ，如果你之前并没有使用过 Git ：[Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)。
### 建立连接
网站编辑，创作博客等等操作都是在我们自己的电脑上进行的，要把这些改动上传到 Github ，然后 Github 生成在线网站，别人就可以访问了。我们再次在 Github 中建立一个新仓库用于管理我们上传过去的代码。然后打开 Webstorm 链接这个仓库， Git -> Manage Remotes：
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510172026678.png)
第一次连接时可能不会出现 Git 选项，而是显示 VCS ，我们将这个项目 Share to Github 。最终来到这个这个页面：
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510172133421.png)
点击左上角加号新建链接：
```bash
git@github.com:Github账户名/Github账户名.github.io.git
```
之后打开 _config.yml ，拉到最下面配置部署：
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510172122084.png)
分支都需要按照自己的实际情况来填写，默认是main，也可能是master或者其他自定义分支，需要自己查看 Github 仓库的实际分支名称。
## 网站上线
OK，网站部署已完成，在终端依次输入：
```bash
hexo clean
hexo g
hexo s
hexo d
```
本地预览后按 Ctrl + C 关闭。输入`hexo d`后若提示：
```bash
INFO  Deploy done: git
```
则部署完成，在浏览器网址处输入`Github账户名.github.io`，回车，就进入你自己的网站啦。不过由于 Github 在国内访问速度较慢，如果你想在国内有不错的访问体验则还需要另一番操作，租用国内的服务器、购买国内域名、ICP备案等等，这就需要另找教程了。
## 上传博客
### 文本编辑
博客一般是用Markdown标记语言写的，你可以自己选择一款Markdown Editor，比如笔者用的就是 VSCode ，下载后添加扩展 Markdown All in One:
![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510172152757.png)
然后用 VSCode 打开 source 文件夹，就能愉快地用 VSCode 编辑所有博客了。按住`Ctrl + Shift + P`就可以打开实时预览窗口。
此外，为了中文、英文联排的美观性，这里有一个自动加空格的项目：[为什么我就是能这样娴熟地加上空格呢？](https://zizhengwu.github.io/daft-auto-spacing/)
### 添加图片
我们上传图片用的 PicGo，PicGo 有一个从剪切板上传的选项，一般 Windows 截屏后，都会将截屏复制到剪切板，这里介绍一个比 Windows 截屏更好用的截屏工具： [Snipaste](https://www.snipaste.com/) 。能够方便地进行截屏、标注，配合 PicGo 直接形成了完美工作流，例如我将`Alt + 1`设置为 Snipaste 截屏，`Ctrl + Shift + P `设置为 PicGo 剪切板上传，PicGo 上传后自动复制Markdown图片链接。
- 所以我需要添加截屏图片时：
  - `Alt + 1`->`Ctrl + Shift + P `->`Ctrl + V`
  - 选定区域截屏加标注->自动上传->插入的Markdown图片。
- 如果需要上传本地图片，则选中图片：
  - `Ctrl + C`->`Ctrl + Shift + P `->`Ctrl + V`
### 再次部署
编辑好新的`.md`文件后，在本地编译预览，确认没问题就可以重新部署，push 到 Github 上了，即便 Github 已经接受了新的改动，网站上的更新依旧会延迟几分钟。