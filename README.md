# jotang-recruit-2026-git
我的git学习
一.关于创建
1. mkdir my-git-test
2. cd my-git-test
3. touch index.html
4. echo "hello git" > index.html当时这一步的时候出错了，忘记在echo后面空格了
5. git init建立仓库
6. git status查看状态（Esc+:q!返回）
7. git add将文件放入暂存区
（了解了git有工作区，暂存区，历史提交）
8. git commit -m "我的第一次尝试"(第一次的时候-m没有加，失败了)

二.关于回滚
git log检查
git restore .可以回滚所有文件
1. 在工作区的改动：git diff查看修改内容，按q返回
                  git restore index.html 回滚 
2. 在暂存区的改动：git restore --staged   （stage是在暂存区的意思）任何 git restore从工作区回滚
3. 在提交历史的改动：
git reset --hard HEAD~1将提交历史，暂存区，工作区的改动全部回滚。    
git reset --mixed 默认git reset 将提交历史和暂存区回滚
git reset --soft 只回滚提交历史的改动
4.在提交历史中改动保留改动记录
git revert HEAD 创建一个新的commmit抵消原来的commit
进入Vim界面用：wq返回

三.使用gitignore忽略文件
1. 创建个人学习笔记 vim notes.txt
2. vim .gitigore 在gitignore中把想忽略的文件名填入,想忽略的文件就不会再被跟踪
3. git add .gitignore
4. git commit -m " 添加.gitignore"

四.分支
1. 需要分支的原因：master/main分支如果新添没做好的功能会不稳定
2. 创建分支：git branch feature/功能名称 （feature/可去）
3. 转换到新建分支 git switch feature/功能名称
4. 简便 git switch -c feature/功能名称 
       git checkout -b feature/功能名称 （创建并转换）
5. 合并分支 git branch
        git merge feature/功能名称
6. 删除分支 git branch -d
7. 解决冲突  在vim或者vscode解决后再 git commit
多个合并，第一次合并不需要git commit因为master是直接快进fast-forward过去的，第二次合并需要git commit,没有冲突时git会自己commit
8. rebase给分支换地基，git rebase master 分支换地基的时候是每个节点依次换，遇到冲突，解决冲突后，git add index.html 然后git rebase --continue 
9. stash 没有进入提交的（工作区＋暂存区）都会进入stash
在问题解决之后用git stash pop将stash的内容取回工作区
不适用于同时处理多个分支
10. worktree：每一个worktree都有自己的工作区和暂存区，但是所有的worktree共同用一个提交历史
git  worktree add -b feature/stats ../名称 master（名称为新的worktree名称）
..是父级目录（当前文件夹的上一级文件夹）
查看worktree先 git config --global core.quotePath false转译成中文
再 git worktree list 不转译出现的是八进制
用 git branch 查看分支时，分支前*代表当前所在分支，+代表其他worktree里的分支
完成后，先切换到master，合并然后删掉feature/stats分支
然后切换到cd ../新的worktree名称
git worktree remove ../新的worktree名称
优势：共享和并行 
