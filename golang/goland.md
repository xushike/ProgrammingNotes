# goland

# 一 概述
goland开发工具的笔记

## 3 常识
### 3.1 快捷键迁移
从vscode迁移过来：
1. 选中下一个匹配，goland是`Find Next/Move to Next Occurrenc`，和vscode区别很大，所以在goland干脆就不用这个快捷键；vscode是`editor.action.addSelectionToNextFindMatch`
2. 选中当前单词，`Extend Selection`
3. 删除一行，`Delete line`
4. 终端，`Tool Windows -> Terminal`
5. 上移下移，`Code -> Move Line Up/Down`
6. 新开一行，`start new line`
7. 删除到行首，`delete to Line Start`

# 二 安装配置
## 4 配置
1. 设置竖线：`show hard wrap guide(configured in code style options)`
2. 配置运行测试的环境：默认类似于dev，配置`GOENV=test`，暂时没看到全局配置的地方，先忽略。
3. 本地有多个go版本时，想切换似乎只需要设置goland的`GOROOT`

# 三 基础

