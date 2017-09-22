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
