

# Node

## `node`安装
  - [下载地址](https://nodejs.org/en/download/)
     - 注意：安装过程中务必勾选`Add to PATH`选项，将`node.js`添加至环境变量

## 环境配置

> ```
> 主要配置的是`npm`安装的全局模块所在的路径，以及缓存(cache)的路径；
> 如果不配置在执行类似`npm install express [-g] `的安装语句时，会将安装的模块安装到`【C:\Users\用户名\AppData\Roaming\npm】`路径中，占C盘空间。
> ```

- 将**全局模块**所在路径和**缓存路径**放在`node.js`安装的文件夹中，则在我安装的文件夹`【D:\Program Files\nodejs】`下创建两个文件夹【node_global】及【node_cache】；

- 然后命令行中输入下列两个命令即可：

  ```
  npm config set prefix "D:\Program Files\nodejs\node_global"
  npm config set cache "D:\Program Files\nodejs\node_cache"
  ```

## `node`版本管理 `Gnvm`

[Gnvm](https://github.com/kenshin/gnvm)

## `node`包管理

[ndm](https://github.com/720kb/ndm)



## 关于版本号

### 版本格式
	1. 主版本号：做了不兼容`API`修改；
	2. 次版本号：做了向下兼容的功能性新增；
	3. 修订号：做了向下兼容的问题修正。

	先行版本号及版本编译信息可以加到"主版本号.次版本号.修订号"的后面，作为延伸。

### 语义化版本控制
	1. XYZ(主版本号.次版本号.修订号)修复问题单不影响`API`时，递增修订号；
	2. `API`保持向下兼容的新增及修改时，递增次版本号；
	3. 进行不向下兼容的修改时，递增主版本号。