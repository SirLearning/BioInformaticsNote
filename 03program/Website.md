
# 个人网站

建立本地网站，然后发送出去

框架网站：

- Hexo，可以将Markdown快速生成主题静态文件

- 内容管理系统(CMS)：
	- WordPress：基于PHP和MySQL，要先搞一台服务器

本地环境：

- git

hexo的文件结构：

- public 最终所见网页的所有内容
- node_modules 插件以及hexo所需node.js模块
- _config.yml 站点配置文件，设定一些公开信息等
- package.json 应用程序信息，配置hexo运行所需js包
- scaffolds 模板文件夹，新建文章，会默认包含对应模板内容
- themes 存放主题文件，hexo根据主题生成静态网页（速度贼快）
- source 用于存放用户资源（除 *posts 文件夹，其余命名方式为 “* + 文件名”的文件被忽略）

```
PS D:\2_Tool\hexo-sirl-blog> hexo s %显示网站
INFO  Validating config
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop.
INFO  Catch you later
```

## 主题

## 服务器

阿里云购买服务器

通过git bash进入服务器：

```
ssh -v git@8.130.11.119
ssh -v root@8.130.11.119
```
