# git命令

# 放到暂存区
`$ git add <file>`

# 查看状态
`$ git status`

# 取消暂存
`$ git rm --cached <file>`

# 提交
`$ git commit -a -m 'a comment'`

# 查看提交日志
`$ git log`

# 分支
- 查看分支
  `$ git branch`

- 创建分支
  `$ git branch <分支>`

- 提交分支
  `$ git push origin <分支>`

- 切换分支
  `$ git checkout <分支>`

- 新建分支并切换
  `$ git checkout -b <分支>`

- 合并分支
  `$ git checkout master`
  `$ git merge <分支>`

- 删除分支
  `$ git branch -d <分支>`

- 拉取远程分支到本地
  `$ git checkout -b <本地分支名> origin/<远程分支名>`

# 标签

- 打标签

  `$ git tag -a v1.4 -m '附注内容'`

- 推送标签到远程仓库

  > 推送单个标签
  >
  > `$ git push origin v1.0.0`

  >推送所有标签
  >
  >`$ git push --tags` 或 `$ git push origin --tags`

