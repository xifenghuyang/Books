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

   

