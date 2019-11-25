# hexo - personal website
此仓库用于更换电脑后快速配置自己的Hexo，从而实现跨物理平台维护个人博客。
核心内容是恢复软件环境（git, node.js, npm, hexo）和恢复博客配置（node_modules，public ，db.json）

一、恢复环境
①安装git
sudo apt-get install git
②设置git全局邮箱和用户名
git config --global user.name "yourgithubname"
git config --global user.email "yourgithubemail"
③设置ssh key
ssh-keygen -t rsa -C "youremail"
#生成后填到github和coding上 #(optional - coding平台)
    #验证是否成功(optional)
    ssh -T git@github.com
    ssh -T git@git.coding.net     #(optional - coding平台)
④安装nodejs , npm包管理器
sudo apt-get install nodejs
sudo apt-get install npm
⑤安装hexo
sudo npm install hexo-cli -g
⑥把此工程 clone 到合适位置 
git clone git@github.com:kajiter/hexo.git 

二、恢复配置
⑦必须 cd 到 config.yml 所在的路径下（cd MyBlog/clBlog）
npm install 
npm install hexo-deployer-git --save
⑧生成，调试/部署：
#generate
hexo g 
#server
hexo s
#deploy
hexo d

三、完成部署，开始创作
⑨可以开始写你的新博客了
hexo new NewBlogName

四、git 命令复习
git status
git log
git log --pretty=oneline  以图形式查看所有操作
git reset --hard  (6位id值)  回退到某一ID对应的版本（既可以是过去，也可以是未来）

git pull
git pull --rebase origin master

git add .
git commit –m "xxxx"
git push 


