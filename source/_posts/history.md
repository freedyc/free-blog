---
title: Linux history 命令
date: 2021-12-09 23:36:46
tags: linux
comments: true

---

# Linux history 命令

linux 上用来查看历史使用过的命令

## 命令

### 列出最近使用n命令

```bash
history [n]
```

### history [-raw] file

```bash
history -a .bak_history 将当前的历史命令存储到.bak_history
history -c 清楚当前使用的历史命令
history -r 将本地文件存储的历史命令存储到内存中，可以通过 history 查看
history -w 将内存中的历史命令保存到本地文件中

```

默认历史命令写入**~/.bash_history**文件

### 快捷调用历史命令

```bash
!n #调用第一个历史命令
!! #执行上一次使用的命令
!command #从最近命令中查询command开头的命令执行

ctrl + r # 搜索历史记录，如果找到则显示出来

```

## 配置

```bash
export HISTSIZE=1000 # 配置历史命令上限条数
export HISTTIMEFORMAT="%y-%m-%d %H:%M:%S " #配置记录命令使用时间

```