# 在Ubuntu(优麒麟)上设置多个ssh
 > 我这里设置的是一个在github上用，一个在gitlab上用
 * 生成第一个ssh：ssh-keygen -t rsa -f "~/.ssh/id_rsa_user1" -C "youremail2"
 * 生成第二个ssh： ssh-keygen -t rsa -f "~/.ssh/id_rsa_user2" -C "youremail2"
 * 在.ssh文件夹下新建.config文件，写如下内容：
 
 > Host gitlab.com  // 这里gitlab的域名
 > RSAAuthentication yes
 >IdentityFile ~/.ssh/id_rsa_user1

 > Host github.com  // 这里是github的域名
 > RSAAuthentication yes
 > IdentityFile ~/.ssh/id_rsa_user2
 
 * 秘钥添加到ssh agent中：ssh-add ~/.ssh/id_rsa_user2
  + 如果出现Could not open a connection to your authentication agent的错误，就运行：
   1. ssh-agent bash
   2. ssh-add ~/.ssh/id_rsa_user2
 * 将公钥加入到对应网站的ssh中
 * 验证是否成功：ssh -T git@github.com
  Hi xxxx! You've successfully authenticated, but GitHub does not provide shell access.出现这个就成功了。
  * 如果要提交项目就必须设置git的用户名和邮箱
   1. git config user.name "your user name"
   2. git config user,email "your user email"