# AutoApiSecret-加密版
# 置顶 #

* 本项目是建立在[原教程](https://blog.432100.xyz/index.php/archives/50/)可以正确调用api的**假设**上的，核心是paran/黑幕大佬的py脚本。
* 本项目只是提供一个自动、免费、无需额外设备的脚本运行方式，换句话说，**借用github的电脑/服务器来干活**。（因为原教程需要服务器/超长时间运转的设备，大部分人都不具备，本项目应运而生）
* 本项目运行依赖**github action**服务，此功能github固有而**非私人提供**的服务器，且整个运行过程只涉及你与github。
* 请务必先阅读理解[原教程](https://blog.432100.xyz/index.php/archives/50/)的**原理说明、设计理念**。
* **不保证一定能续期！不保证一定能续期！不保证一定能续期**！或者说，**只是增大续订可能性**。过期前、后30天都可能续期！！！
* 若理解并接受上述说明，请接着操作；**若否，请点击浏览器右上角 X 。**

### 项目说明 ###

* 利用github action实现**定时自动调用api**，保持E5开发活跃。
* **免费，不需要额外设备/服务器**，部署完不用管啦。
* 加密版，隐藏应用id+机密，保护账号安全。

--------------------------------------------------------------

### 步骤 ###

* 第一步，获取应用id、机密、refresh_token 3样东西，以方便接下来的操作。
  登录[Microsoft Azure](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade),找到应用注册并且新注册一个应用
  <img src="https://raw.githubusercontent.com/Wyatt323/E5API/main/img/%E7%AC%AC%E4%B8%80%E6%AD%A5-%E6%89%BE%E5%88%B0%E5%BA%94%E7%94%A8%E6%B3%A8%E5%86%8C.png"/>
  
  注册应用是的注意事项
  <img src="https://raw.githubusercontent.com/Wyatt323/E5API/main/img/%E7%AC%AC%E4%B8%80%E6%AD%A5-%E6%B3%A8%E5%86%8C%E5%BA%94%E7%94%A8.png"/>
  
  注册成功后复制id
  <img src="https://raw.githubusercontent.com/Wyatt323/E5API/main/img/%E7%AC%AC%E4%B8%80%E6%AD%A5-%E5%A4%8D%E5%88%B6id.png"/>
  
  创建机密
  <img src="https://raw.githubusercontent.com/Wyatt323/E5API/main/img/%E7%AC%AC%E4%B8%80%E6%AD%A5-%E5%88%9B%E5%BB%BA%E6%9C%BA%E5%AF%86.png"/>
  
  复制机密
  <img src="https://raw.githubusercontent.com/Wyatt323/E5API/main/img/%E7%AC%AC%E4%B8%80%E6%AD%A5-%E5%A4%8D%E5%88%B6%E6%9C%BA%E5%AF%86%E5%80%BC.png"/>
  
  添加api权限
  <img src="https://raw.githubusercontent.com/Wyatt323/E5API/main/img/%E7%AC%AC%E4%B8%80%E6%AD%A5-%E6%B7%BB%E5%8A%A0api%E6%9D%83%E9%99%90.png"/>
  
  Api权限如下
  <img src="https://raw.githubusercontent.com/Wyatt323/E5API/main/img/%E7%AC%AC%E4%B8%80%E6%AD%A5-Api%E6%9D%83%E9%99%90.png"/>
  
  api授权成功如下
  <img src="https://raw.githubusercontent.com/Wyatt323/E5API/main/img/%E7%AC%AC%E4%B8%80%E6%AD%A5-api%E6%8E%88%E6%9D%83%E6%88%90%E5%8A%9F.png"/>
  
  获取refresh_token
  首先下载[Rclone](https://rclone.org/downloads/),下载完成后解压缩
  在eclone.exe的文件夹中按住shift+右键，打开Powershell，然后输入start cmd打开cmd
  在cmd中输入
  ```shell
  rclone authorize "onedrive" "你的应用ID" "你的机密值"
  ```
  回车后弹出浏览器，登录你刚才创建此应用的账号，提示success后返回cmd窗口找到refresh_token，并复制双引号中的内容
  <img src="https://raw.githubusercontent.com/Wyatt323/E5API/main/img/%E7%AC%AC%E4%B8%80%E6%AD%A5-%E8%8E%B7%E5%8F%96refresh_token.png"/>
  
  
* 第二步，fork[本仓库](https://github.com/Wyatt323/E5AutoApi),后序操作都在你自己fork后的仓库中使用

* 第三步，依次点击上栏Setting > Secrets > Actions > new repository secret，新建两个secret如下图：CONFIG_ID、CONFIG_KEY。
  内容分别如下: ( 把你的应用id改成你的应用id , 你的应用机密改成你的机密，单引号不要动 )
  CONFIG_ID
  ```shell
  id=r'你的应用id'
  ```
  <img src="https://raw.githubusercontent.com/Wyatt323/E5API/main/img/%E7%AC%AC%E4%B8%89%E6%AD%A5-%E5%88%9B%E5%BB%BAsecret1.png"/>

  CONFIG_KEY
  ```shell
  secret=r'你的应用机密'
  ```    
  <img src="https://raw.githubusercontent.com/Wyatt323/E5API/main/img/%E7%AC%AC%E4%B8%89%E6%AD%A5-%E5%88%9B%E5%BB%BAsecret2.png"/>

* 第四步，进入你的个人设置页面(右上角头像 Settings，不是仓库里的 Settings)，选择 Developer settings > Personal access tokens > Generate new token
  
  设置名字为GITHUB_TOKEN , 然后勾选 repo , admin:repo_hook , workflow 等选项，最后点击Generate token即可。 

* 第五步，点击右上角星星/star立马调用一次，再点击上面的Action就能看到每次的运行日志，看看运行状况

（必需点进去Test Api看下，api有没有调用到位，有没有出错。外面的Auto Api打勾只能说明运行是正常的，我们还需要确认10个api调用成功了，就像图里的一样。如果少了几个api，要么是注册应用的时候赋予api权限没弄好；要么是没登录激活onedrive，登录激活一下）

  <img src="https://raw.githubusercontent.com/Wyatt323/E5API/main/img/action%E6%88%90%E5%8A%9F.png"/>

* 第六步，没出错的话，就搞定啦！！再看看下面的定时次数要不要修改，不打算改就忽略。

  **然后第二天回来确认下是否自动运行了（ation里是否多出来几个）**,是的话就不用管了，完结。

  我设定的每3小时自动运行一次，每次调用3轮（点击右上角星星/star也可以立马调用一次），你们自行斟酌修改（我也不知道保持活跃要调用多少次、多久）：

  * 定时自动启动修改地方：（在.github/workflow/AutoApiSecret.yml文件里，自行百度cron定时任务格式，最短每5分钟一次）

  <img src="https://raw.githubusercontent.com/Wyatt323/E5API/main/img/%E4%BF%AE%E6%94%B9%E5%AE%9A%E6%97%B6.png"/>

------------------------------------------------------------

### 题外话 ###

> Api调用
>   你们可以自己去graph浏览器看一下，学着自己修改要调用什么api(最重要的是调用outlook、onedrive)
>   https://developer.microsoft.com/zh-CN/graph/graph-explorer/preview

### GithubAction介绍 ###

提供的虚拟环境：

· 2-core CPU
· 7 GB RAM 内存
· 14 GB SSD 硬盘空间

使用限制：

* 每个仓库只能同时支持20个 workflow 并行。
* 每小时可以调用1000次 GitHub API 。
* 每个 job 最多可以执行6个小时。
* 免费版的用户最大支持20个 job 并发执行，macOS 最大只支持5个。
* 私有仓库每月累计使用时间为2000分钟，超过后$ 0.008/分钟，公共仓库则无限制。

（我们这里用的公共仓库，按理，你们可以设定无限循环调用，然后6小时启动一次，保证24小时全天候调用）

