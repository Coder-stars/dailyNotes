> [最强参考](https://git-scm.com/book/zh/v2)

 ## git日常遇到的问题总结

>  git branch 分支名 ---新建分支（不切换当前分支 在新分支名名称之前加上-b表示新建并切换到新分支）

>  git add -i 交互式的添加文件到缓存区

 ### git commit的种类

``` bash
fix：Bug问题修复
feat:新功能(feature)
improvement： 对现有功能的改进
upgrade:升级
docs ：文档改动（eg：md文件）
init 初始化
style： 代码格式的变动（注：不是样式，是指代码的空格、缩进、换行、标点符号等）

refactor： 重构

perf： 性能优化（performance）

test： 测试文件更新

build： 构建系统或者包依赖更新（eg: gulp、npm、broccoli）

ci： CL配置，脚本文件等更新（eg：Travis持续集成服务、）

chore： 非src或者测试文件的更新

revert： commit 回滚 
```

​	

## git stash

```bash
git stash:
用法：git stash list [<选项>]
  或：git stash show [<选项>] [<stash>]
  或：git stash drop [-q|--quiet] [<stash>]
  或：git stash ( pop | apply ) [--index] [-q|--quiet] [<stash>]
  或：git stash branch <分支名> [<stash>]
  或：git stash clear
  或：git stash [push [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet]
          [-u|--include-untracked] [-a|--all] [-m|--message <消息>]
          [--pathspec-from-file=<file> [--pathspec-file-nul]]
          [--] [<路径规格>...]]
  或：git stash save [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet]
          [-u|--include-untracked] [-a|--all] [<消息>]
```

 [参考场景](https://www.cnblogs.com/tocy/p/git-stash-reference.html)

> List  显示所有的缓存

### commit之后如何撤销

``` 使用git reset --soft head^进行回退操作撤销commit```

