# my_bucket
自建的scoop bucket仓库，用于在新系统中快速部署软件
# 步骤
- 网络环境

首先解决科学上网的前提，或者使用国内源替换
- 安装scoop

首先设置默认安装位置

设置scoop环境变量
首先在文件资源管理器内新建目录，然后将下面命令中的目录修改为新建好的目录。

用户目录

    $env:SCOOP='D:\Scoop'

    [Environment]::SetEnvironmentVariable('SCOOP',$env:SCOOP,'User')
全局目录

    $env:SCOOP_GLOBAL='D:\ScoopGlobalApps'

    [Environment]::SetEnvironmentVariable('SCOOP_GLOBAL',$env:SCOOP_GLOBAL,'User')
这里设置环境变量第三个参数User表示用户级别，Machine表示系统级别。Machine没权限的话，可以手动去环境变量设置。
- 安装命令（下面两个命令等效）

    iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
    iwr-useb get.scoop.sh|iex

如果网络环境不合适的话上面命令执行是错误的。
- 添加源

        scoop bucket add extras
        #官方维护的源，有大量软件
        #添加并测试自己的源
        scoop bucket add my-bucket https://github.com/is-whale/my_bucket
        
        #测试
        # 安装 hello 这个 App
        scoop install hello
        #运行 hello
        hello
如果正常，会看到 Hello, < Windows 用户名>!

TODO：添加常用软件的json文件,并且添加目录

一键安装软件命令

    scoop update
    scoop install my-bucket/neteasymusic weichat

其他信息
Scoop 常用命令
scoop help #查看帮助
scoop help <某个命令> # 具体查看某个命令的帮助
 
scoop install <app>   # 安装 APP
scoop uinstall <app>  # 卸载 APP
 
scoop list  # 列出已安装的 APP
scoop search # 搜索 APP
scoop status # 检查哪些软件有更新
 
scoop update # 更新 Scoop 自身
scoop update appName1 appName2 # 更新某些app
scoop update *  # 更新所有 app （前提是需要在apps目录下操作）
 
scoop bucket known #通过此命令列出已知所有 bucket（软件源）
scoop bucket add bucketName #添加某个 bucket
 
scoop cache rm <app> # 移除某个app的缓存
安装卸载软件
# 安装之前，通过 search 搜索 APP, 确定软件名称
scoop search  xxx
 
# 安装 APP
scoop install AppName
 
# 安装特定版本的 APP；语法 AppName@[version]，示例
scoop install git@2.23.0.windows.1
 
# 卸载 APP 
scoop uninstall #卸载 APP
更新软件
包含：如何禁用更新

scoop update # 更新 Scoop 自身
 
scoop update appName1 appName2 # 更新某些app
 
# 更新所有 app （可能需要在apps目录下操作）
scoop update *
 
# 禁止某程序更新
scoop hold <app>
# 允许某程序更新
scoop unhold <app>
清除缓存与旧版本
# 查看所有以下载的缓存信息
scoop cache show
 
# 清除指定程序的下载缓存
scoop cache rm <app>
 
# 清除所有缓存
scoop cache rm *
 
# 删除某软件的旧版本
scoop cleanup <app>
 
# 删除全局安装的某软件的旧版本
scoop cleanup <app> -g
 
# 删除过期的下载缓存
scoop cleanup <app> -k
别名
⚠️️ 注意：请在 Powershell 中运行下面的命令

# 可用操作
scoop alias add|list|rm [<args>]
 
## 添加别名，格式：
scoop alias add <name> <command> <description>
 
# 示例：（注意：必须在 Powershell中运行）
scoop alias add st 'scoop status' '检查更新'
# 检查已添加的别名
scoop alias list -v
 
Name Command      Summary
---- -------      -------
st   scoop status 检查更新
 
# 测试已添加的别名 st
scoop st
 
 
# 另一个示例：
scoop alias add rm 'scoop uninstall $args[0]' '卸载某 app'
在同一程序的不同版本之间切换
使用命令：

scoop reset [app]@[version]
示例：

scoop reset idea-ultimate-eap@201.6668.13
 
scoop reset idea-ultimate-eap@201.6073.9
 
# 切换到最新版本
scoop reset idea-ultimate-eap
对应版本的程序需要已经安装于本地系统中；所以在你清除某个软件的旧版本时考虑一下自己是否还会再次使用到此旧版本。

另外 idea-ultimate-eap 切换过程可能需要更长时间。

其它命令
# 显示某个app的信息
scoop info <app>
 
# 在浏览器中打开某app的主页
scoop home <app>
 
# 比如
scoop home git
添加软件源 Bucket
Scoop 可安装的软件信息存储在 Bucket（翻译为：桶）中，也可以称其为软件源。Scoop 默认的 Bucket 为 main ；官方维护的另一个 Bucket 为 extras，我们需要手动添加。

# bucket的用法
scoop bucket add|list|known|rm [<args>]
添加 extras :

scoop bucket add extras
我们也可以添加第三方 bucket ，示例：

scoop bucket add dorado https://github.com/h404bi/dorado
并且明确指定安装此 bucket （软件源）中的的程序：

scoop install dorado/<app_name>
# 下面是dorado中特有的软件，测试其是否添加成功
scoop search trash