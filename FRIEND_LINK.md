# 友链交换说明

### 格式
```yaml
-
  name: # 你如何称呼
  title: # 博客名称, 用于展示
  site: # 博客链接
  desc: # 博客描述
  email: # 你的邮箱(可选, 因为我的仓库是公开的, 你的邮箱也会被其他查看该仓库的人发现)
  # 以下配置暂时被忽略
  avatar: # 头像链接, 用于展示
  # 你可以通过注释来描述自己
```

### 流程
1. fork我的[博客仓库](https://github.com/ruan4261/ruan4261.github.io/), github现在好像是支持在线修改的, 可以用gitpod之类的修改然后直接pr
2. 将你的信息根据上述格式append到`/src/_data/_friendlink.yml`文件中
3. 向我的博客仓库的master分支提交pull request
4. 请注意及时在您的友链页面加上我哦^. ^

### 我的信息
```yaml
- 
  name: ruan4261 # 我在绝大部分平台上的账号都为ruan4261, 但很显然它并不能很好地被读出来, 所以你可以称呼我为 时雨「しぐれ」,　全名为　林时雨「はやししぐれ」
  title: ruan4261's blog
  site: https://4261.ink
  desc: この現実世界には穴がある。そして……ドーナツにも。
  email: i@4261.ink
  avatar: https://4261.ink/images/avatar.png
  # 江苏人, 祖籍部分山西, 喜欢面食, 喝醋在行, 碳酸禁止
  # Java工程师, 工作经验2020年起, 学历短板, 目前base南京, 主板上市ToB软件公司, 有在寻找互联网行业的机会(比较想做敏捷开发, 或通用计算等)
  # 爱好动画, 游戏(gal), 写代码
```
