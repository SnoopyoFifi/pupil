# Shell-Vi-SSH

## `Linux`常用命令

  - [`Linux`命令大全](http://code.ziqiangxuetang.com/linux/linux-command-manual.html)

  - [`Linux` 命令大全搜索](http://man.linuxde.net/)

  > 处理文件目录常用命令

    - pwd (Print Working Di-ectory) 查看当前目录

    - cd (Change Directory) 切换目录，如 cd /etc

    - ls (List) 查看当前目录下内容，如 ls -al

    - mkdir (Make Directory) 创建目录，如 mkdir blog

    - touch 创建文件，如 touch index.html

    - cat 查看文件全部内容，如 cat index.html

    - less 查看文件，如more /etc/passwd、less /etc/passwd

    - rm (remove) 删除文件，如 rm index.html、rm -rf  blog

    - rmdir (Remove Directory) 删除文件夹，只能删除空文件夹，不常用

    - mv (move) 移动文件或重命名，如 mv index.html ./demo/index.html

    - cp (copy) 复制文件，cp index.html ./demo/index.html

    - tab 自动补全，连按两次会将所有匹配内容显示出来

    - \>和 >>重定向，如echo hello world! > README.md，>覆盖 >>追加

    - | 管道符可以将多个命令连接使用，上一次（命令）的执行结果当成下一次（命令）的参数。

    - grep 匹配内容，一般结合管道符使用


  > 打开`pdf/html`文件

    - `firefox http://www.google.com` : 打开网站用 `firefox` 命令；
    
    - `evince  xx.pdf` : 打开pdf时，用 `evince` 命名；


## `vi`/`vim` 的使用

  - [vi/vim使用](http://code.ziqiangxuetang.com/linux/linux-vim.html)

  - `vim`的三种模式

    **一般模式**：(命令模式)

    以 vi 打开一个档案就直接进入一般模式了(这是默认的模式)。
    在这个模式中， 你可以使用『上下左右』按键来移动光标，你可以使用『删除字符』或『删除整行』来处理档案内容， 也可以使用『复制、贴上』来处理你的文件数据。

    **编辑模式**：(插入模式)

    在一般模式中可以进行删除、复制、贴上等等的动作，但是却无法编辑文件内容的！ 
    要等到你按下『i, I, o, O, a, A, r, R』等任何一个字母之后才会进入编辑模式。
    注意了！通常在 Linux 中，按下这些按键时，在画面的左下方会出现『INSERT 或 REPLACE 』的字样，此时才可以进行编辑。.
    而如果要回到一般模式时， 则必须要按下『Esc』这个按键即可退出编辑模式。

    **指令列命令模式**：(底行模式)

    在一般模式当中，输入『 : / ? 』三个中的任何一个按钮，就可以将光标移动到最底下那一行。
    在这个模式当中， 可以提供你『搜寻资料』的动作，而读取、存盘、大量取代字符、离开 vi 、显示行号等等的动作则是在此模式中达成的！

    ![vi的三种模式切换](./images/vim_model.png)

  - 使用vi/vim编辑器

    - 打开/创建文件， vi 文件路径

    - 底行模式 :w保存，:w filenme另存为

    - 底行模式 :q退出

    - 底行模式 :wq保存并退出

    - 底行模式 :e! 撤销更改，返回到上一次保存的状态

    - 底行模式 :q! 不保存强制退出

    - 底行模式 :set nu 设置行号

    - 命令模式 ZZ（大写）保存并退出

    - 命令模式 u辙销操作，可多次使用

    - 命令模式 dd删除当前行

    - 命令模式 yy复制当前行

    - 命令模式 p 粘贴内容

    - 命令模式 ctrl+f向前翻页

    - 命令模式 ctrl+b向后翻页

    - 命令模式 i进入编辑模式，当前光标处插入

    - 命令模式 a进入编辑模式，当前光标后插入

    - 命令模式 A进入编辑模式，光标移动到行尾

    - 命令模式 o进入编辑模式，当前行下面插入新行

    - 命令模式 O进入编辑模式，当前行上面插入新行


## `SSH`网络协议

  > SSH是一种网络协议，用于计算机之间的加密登录。SSH只是一种协议，存在多种实现，既有商业实现，也有开源实现。本文针对的是OpenSSH，它是自由软件，应用非常广泛。

  > 如果要在Windows系统中使用SSH，会用到另一种软件PuTTY，Git客户端集成了SSH。

  - `格式：ssh user@host`  
  
    - `user` 代表真实存在的用户； 
    
    - `host` 代表要登录的远程计算机。
  
  - 加密技术
    - 分别是<u>对称性加密</u>和<u>非对称性加密</u>，SSH属于后者。

    - 对称加密算法在加密和解密时使用的是同一个密钥； 

    - 而非对称加密算法需要两个密钥来进行加密和解密，这两个秘钥分别是公开密钥（public key，简称公钥）和私有密钥（private key，简称私钥）。


  - 工作原理
    > 公钥和私钥是成对出现，
    > 
    > 可以通过`ssh-keygen -t rsa`来创建，
    > 
    > 既可以通过密钥来加密数据，也可以通过私钥来加密数据，如果是以公钥进行的数据加密，只能与之相对应的私钥才可以解密，
    > 
    > 相反如果以私钥进行的数据加密，则只能与之对应的公钥才可以将数据进行解密，这样就可以提高信息传递的安全性。

  - 免密码登录（待定）
    
    > 我们可以将本地机器上的公钥保存到特定的远程计算机上，这样当我们再次登录访问这台远程计算机时就可以实现免密码登录了。

    - ssh-keygen -t rsa会创建公钥和密钥（默认在用户目录/.ssh目录下）

    - ssh-copy-id user@host添加到对应远程主机的用户目录/.ssh目录下

    - 也可以登录远程主机，进入到用户目录/.ssh目录下手动创建authorized_keys文件，并将自已的公钥粘入该文件。
