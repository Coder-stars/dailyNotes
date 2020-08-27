## git日常遇到的问题总结

>  git branch 分支名 ---新建分支（不切换当前分支 在新分支名名称之前加上-b表示新建并切换到新分支）

>  git add -i 交互式的添加文件到缓存区

### git commit的种类

``` bash
fix：Bug问题修复

improvement： 对现有功能的改进

docs ：文档改动（eg：md文件）

style： 代码格式的变动（注：不是样式，是指代码的空格、缩进、换行、标点符号等）

refactor： 重构

perf： 性能优化（performance）

test： 测试文件更新

build： 构建系统或者包依赖更新（eg: gulp、npm、broccoli）

ci： CL配置，脚本文件等更新（eg：Travis持续集成服务、）

chore： 非src或者测试文件的更新

revert： commit 回滚 ```
```



----



