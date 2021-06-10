# hexo - personal website
### 此仓库用于更换电脑后快速配置自己的Hexo，从而实现跨物理平台维护个人博客。核心内容是恢复软件环境（git, node.js, npm, hexo）和恢复博客配置（node_modules，public ，db.json）
---

**一、恢复环境**

①安装git
```
sudo apt-get install git
```

②设置git全局邮箱和用户名
```
git config --global user.name "yourgithubname"
git config --global user.email "yourgithubemail"
```

③设置ssh key
```
ssh-keygen -t rsa -C "youremail"
#生成后填到github和coding上         #(optional - coding平台)
    #(optional 验证是否成功)
    ssh -T git@github.com
    ssh -T git@git.coding.net    #(optional - coding平台)
```
④安装nodejs , npm包管理器
```
sudo apt-get install nodejs
sudo apt-get install npm
```

⑤安装hexo
```
sudo npm install hexo-cli -g
```

⑥把此工程 clone 到合适位置
```
git clone git@github.com:kajiter/hexo.git
```
---
**二、恢复配置**

⑦必须 cd 到 config.yml 所在的路径下,在本机中为 ```/Users/CL/Documents/github/MyBlog```
```
(cd github/MyBlog)
npm install 
npm install hexo-deployer-git --save
```
⑧生成，调试/部署：
```
#generate
hexo g 
#server
hexo s
#deploy
hexo d
```
先部署完文章，再进行 git操作
---
**三、完成部署，开始创作**

⑨可以开始写你的新博客了
```
hexo new NewBlogName
```
新文章在 ```/MyBlog/source/``` 路径下, 默认为 markdown 编辑
---
**四、git 命令复习**

```
git status
git log
git log --pretty=oneline  以图形式查看所有操作
git reset --hard  (6位id值)  回退到某一ID对应的版本（既可以是过去，也可以是未来）

git pull
git pull --rebase origin master


git add .
git commit –m "xxxx"
git push 
```

五、升级依赖库 npm
升级命令
```
# npm install --global npm
npm install -g npm

```

若报错```npm WARN  checkPermissions Missing write access to /usr/local/lib/node_modules```则为权限不够

解决方案: 命令前加sudo，然后输入密码执行，这是解决权限问题的通用办法，需要记忆
```
sudo npm install --global npm

```
六、升级 node.js
```
第一步，先查看本机node.js版本：
node -v

第二步，清除node.js的cache：
sudo npm cache clean -f

第三步，安装 n 工具，这个工具是专门用来管理node.js版本的，别怀疑这个工具的名字，是他是他就是他，他的名字就是 "n"
sudo npm install -g n

第四步，安装稳定版本的node.js
sudo n stable

第五步，再次查看本机的node.js版本：
node -v

第六步，顺带更新npm到最新版
sudo npm install -g npm

第七步，验证node 和 npm 都已更新好
node -v

npm -v

```

六、升级 Hexo

```
hexo version

npm install -g hexo

hexo v

```

---
