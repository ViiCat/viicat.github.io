---
layout: post
title: Github配置SSH for Mac
date: 2021-10-12 15:09:49
categories: [GitHub]
tags:
---
## 查看终端是否存在SSH Key
```
$ cd ~/.ssh
$ ls
```
查看是否已经存在 id_rsa.pub 或 id_dsa.pub 文件

## 创建SSH Key
```
$ ssh-keygen -t rsa -C "your_email@example.com"
```
会提示输入两次密码，该密码是push文件时要输的密码，也可不输入直接按回车。

## 添加公钥到远程仓库
查看mac上生成的公钥

```
$ cat ~/.ssh/id_rsa.pub
```
把内容复制出来

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDZRvOw8ZkRxFE+R1JAsi1EwnqUXep/993pkHrmJTttHD3CG1BBX0Z9yxGQOehET0TNBe9A79nOWEVYL8FlRzCErS4xrqBbJE8mjB/IYX+F46laJxHfQ1kzpTd0nezr8uMTQTZfggKesBoOkWsPIBiOh+ZsOsNpeDnw8lXtH6LUzZtah1cd2Gr1jznAcL3VOlASTnpuBTDW0Kpjt3Q3FdKP0LnI82+fngQOUO+LFS4Fu6mksxeox9JDf3ZvBdBZD7zPFS+BjJ9FSKvydqiIoEgwOGTxS3gjqEezOSmv7o+VXe4pFLQDWBx/vJrF+uJsab3R3hJnd6d9j1PKpMPlHGMMDSnH9KbJfrsIr2wCGJqYFqpx5cjn9brVFkJDo5fCZPgOSva40vbZJeOoV3sJ95j/FOks4PZsfptwpdAydsanuPkGayJMukwQXpOMhuerffPKlsN/vbR6uZ6stPdqcRIi3hx/xQ2nntMb3YStyKtr/6D6wTUlXFzfK5Yu+96rD8M= xxxxxx@duckdake.com
```
登录github账户，`头像-> Settings-> SSH and GPG keys-> New SSH key` 然后将上面复制的内容粘贴进"Key"文本域，点击Add key即可完成

验证key是否可用

```
$ ssh -T git@github.com
```
如果输出:`Hi ViiCat! You've successfully authenticated, but GitHub does not provide shell access.`就算设置成功了。