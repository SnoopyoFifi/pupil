# 插件安装

> 安装 `package control`

1. 使用Ctrl + `打开Sublime Text控制台。

2. [package controll](https://packagecontrol.io/installation#st3) 复制下段代码 </br>

  ```
   import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp =  sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( ' http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please  try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
  ```

3. 等待`package control` 安装完成，使用`Ctrl+Shift+P` 打开命令面板， 输入`pc` 出现`Package Control` 等待片刻，就可以搜索各种插件进行安装了。

4. 补充：

     - 删除插件：`Ctrl+Shift+P`调出命令面板，输入`remove`，调出`Remove Package`选项并回车，选择要删除的插件；

     - 更新插件：`Ctrl+Shift+P`调出命令面板，`upgrade package`。


5. 同步/备份`Sublime Text`配置  
  - [使用`git`结合`github`同步配置](https://segmentfault.com/q/1010000005980661?_ea=972415)
  - 首先需要同步的是`C:\Users\Administrator\AppData\Roaming\Sublime Text 3\Packages\User`目录中的文件夹。
  - 然后在该文件夹下使用`git`同步
    + `git init`初始化仓库

    + 生成`.gitignore`文件

      ```
        Package Control.last-run
        Package Control.ca-list
        Package Control.ca-bundle
        Package Control.system-ca-bundle
        Package Control.cache/
        Package Control.ca-certs/
        encoding_cache.json
      ```

    + 提交远程仓库

      ```
      git add .
      git ci -m "sublime-setting"
      git remote add origin [git 仓库地址]
      git push origin master
      ```

    + 其他设备同步配置 

      ```
      cd [packages folder]
      cp [packages folder]/User [package folser]/User_old  // 删除现有的`user`，新建一个空的`user`文件夹
      git clone https://github.com/SnoopyoFifi/sublime-syncing.git User
      ```

    + 通过以上操作，在任何一台设备有新的改动，只需要将改动提交到远程仓库即可。这样在不同平台的设备之间就可以同步sublime配置和插件了。