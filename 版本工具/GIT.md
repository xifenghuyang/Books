# GIT

## 1. 项目上传

1）新个人办公环境添加ssh密钥

```bash
ssh-keygen ...
```

2) 拷贝公钥到github setting密钥管理中，本地连接测试

```bash
ssh -T git@github
// Hi XXXX! You've successfully authenticated, but GitHub doshell access.
```

3) github仓库创建项目

4）本地文件夹初始化并配置远端

```bash
git init
git add .
git commit -m "first"
git remote add origin [ssh_url]
git pull --rebase origin master
git push origin master
```

## 2.其他命令

1. 查看已有git配置

   ```bash
   git config --list
   ```
### 3.检出必要目录
```
$ mkdir druid
$ cd druid  
$ git init // 初始化空仓库
$ git remote add -f origin https://github.com/alibaba/druid.git // 关联远程地址 ，这一步不要终止执行，不然下面操作无效
$ git config core.sparsecheckout true // 开启Sparse Checkout模式
$ echo "doc" >> .git/info/sparse-checkout // 设置需Check Out的文件。直接从项目目录下开始
$ git pull origin master // Check Out
```
   

