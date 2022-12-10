# mac 安装 ruby

mac 操作系统自带了 ruby。

有两种方式安装其它版本的 ruby：

- 通过 homebrew 安装。
- 通过 rvm （ruby 版本 管理工具）安装，下面介绍这种方式。

## 安装 rvm

官方推荐使用 gpg 来安装 rvm，所以又需要去安装 gpg ，此处我们通过离线的方式安装rvm。

```bash
# 切到用户下载目录
cd ～/Download
# 下载离线包
curl -sSL https://github.com/rvm/rvm/tarball/stable -o rvm-stable.tar.gz
# 创建文件夹
mkdir rvm && cd rvm
# 解包
tar --strip-components=1 -xzf ../rvm-stable.tar.gz
# 安装 
./install --auto-dotfiles
# 加载
source ~/.rvm/scripts/rvm
```

## 安装 ruby

```bash
# 查询 ruby的版本
rvm list known
# 下载指定的版本
rvm install 2.7.5
# 将系统的ruby切换为下载的版本
rvm use 2.7.5  --default
```