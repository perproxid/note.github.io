---
title: jekyll_command
date: 2023-03-26 15:41:12 +0800
categories: [ubuntu, jekyll_command]
tags: [jekyll]     # TAG names should always be lowercase
toc: true
math: true
mermaid: true
pin: false  # pin one or more posts to the top of the home page and the fixed posts are sorted in reverse order according to their release date
img_path: /assets/2023/
---

Abstract: This post will instruct you how to use [**git**] command, [**bundle**] command to run jekyll project, and push your command to remote masters.&emsp;&emsp;&emsp;&emsp;&emsp;

## download project contents

`git clone "https://网址"`

## update ruby dependence

### 切换rubygem源
`bundle config mirror.https://rubygems.org https://gems.ruby-china.com`
### 更新bundle依赖包
```
bundle update
bundle install
bundle add github-pages
bundle add webrick
```
### 运行jekyll
`bundle exec jekyll serve`
### 预览项目页面
`http://127.0.0.1:4000/`

## local project upload to remote

`git add 文件名` 将修改/新创建文件添加  
`git add path/subpath` 将修改/新创建文件夹添加  
`git commit -m "some_mesage"` 确认添加  
`git status` 查询状态  
`git remote -v`  查询远程链接  
`git remote remove origin`  删除远程链接  
`git remote add origin ssh` 添加远程链接   
`git push -u origin master/main` push本地修改


