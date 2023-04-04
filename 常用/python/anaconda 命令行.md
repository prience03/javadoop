

1. 前言
        Conda是Anaconda中一个强大的包和环境管理工具，可以在Windows的Anaconda Prompt命令行使用，也可以在macOS或者Linux系统的终端窗口(terminal window)的命令行使用。

    本文简单介绍conda的一些常用命令（对于大多数人来说掌握了这些就基本上能够‘生活自理’了吧）命令。当然，本文假定你已经安装了Anaconda，并且在Windows条件下使用Anaconda Prompt或者在Linux下使用terminal window。
   
    本文根据conda-getting-started编译而成，喜欢阅读英文的伙伴们可以直接去读英文说明。
   
    conda命令的一些选项开关有两种指定方式，一种两个连接号“--”后跟选项名全程，一种是一个连接号“-”后跟简称。比如说"-n"和"--name"是等价的。但是要注意有些例外，比如说，“--version”对应的是“-V”（大写的V而不是小写的v）。

2. 管理conda自身
  2.1 查看conda版本

  ```c
  conda --version
  ```

  2.2 查看conda的环境配置

  ```c
  conda config --show
  ```

  运行结果示例（只是截取了最前面一小段） 



2.4 设置镜像
        conda有时候安装软件会非常慢。设置国内镜像的话可以使安装更快捷一些。设置方法如下所示：

#设置清华镜像
```c
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
```



#设置bioconda
```c
conda config --add channels bioconda
conda config --add channels conda-forge
```

#设置搜索时显示通道地址
```
conda config --set show_channel_urls yes

```

2.5 更新conda
将conda自身更新到最新版本，it is recommended to always keep conda updated to the latest version.         

```
conda update conda
```

2.6 更新Anaconda整体
将整个Anaconda都更新到确保稳定性和兼容性的最新版本

```
conda update Anaconda
```

2.7 查询某个命令的帮助 

```
conda create --help
```

3. 管理环境
        Conda允许你创建相互隔离的独立环境，这些环境被称之为虚拟环境

（Virtual Environment），这些环境各自包含属于自己的文件、包以及他们的依存关系，并且不会相互干扰。

        Anaconda有一个缺省的名为base的环境。但是不建议把程序放在base环境中，应该创建不同的虚拟环境分别管理不同的开发项目。这个涉及到一个根本的问题：为什么我们需要虚拟环境呢？举一个简单的例子，想象一下你有多个项目要开发，每个项目中都有一些包要依赖于某个共同的包，但是各自的所需要的版本不一致，有一些需要低版本的，有些需要高版本的。然后你就陷入了众口难调的困境。为不同的项目创建虚拟环境就可以把不同项目隔离开来，各自使用自己所需要的软件环境。

3.1. 创建虚拟环境
        使用conda创建虚拟环境的命令格式为:

```
conda create -n env_name python=3.8
```

​        这表示创建python版本为3.8、名字为env_name的虚拟环境。

​    创建后，env_name文件可以在Anaconda安装目录envs文件下找到。在不指定python版本时，自动创建基于最新python版本的虚拟环境.      

3.2. 创建虚拟环境的同时安装必要的包
        但是并不建议这样做，简化每一条命令的任务在绝大多数时候都是明智的（一个例外是需要反复执行的脚本）

```
conda create -n env_name numpy matplotlib python=3.8

```

3.3 查看有哪些虚拟环境
        以下三条命令都可以。注意最后一个是”--”，而不是“-”.

```
conda env list
conda info -e
conda info --envs
```

​       所显示的列表中，前面带星号“*“的表示当前活动环境。比如说当前我的环境列表：

​     星号的位置表示我现在在base环境下工作。注意，也有不是显示base而显示root的，root是因为是以系统管理身份作业（？待确认）

3.4 激活虚拟环境
        使用如下命令即可激活创建的虚拟环境。

```
conda activate env_name

```

​        此时使用python --version可以检查当前python版本是否为所想要的（即虚拟环境的python版本）。

​    在4.6版本以前需要使用如下命令：

​    Linux:  source activate your_env_name

​    Windows: activate your_env_name

​    但是为什么要停留在过去（4.6以前的版本）呢？毕竟现在至少已经有4.10版本了，所以如果你不是最新版本，运行一下"conda update conda"吧



3.5 退出虚拟环境
        使用如下命令即可退出当前工作的虚拟环境。

```
conda activate
conda deactivate
```

​        有意思的是，以上两条命令只中任一条都会让你回到base environment，它们从不同的角度出发到达了同一个目的地。可以这样理解，activate的缺省值是base，deactivate的缺省值是当前环境，因此它们最终的结果都是回到base

        这个只适用于4.6及以后版本。如果你还在4.6以前的话，参见上一条说明。

3.5 删除虚拟环境
        执行以下命令可以将该指定虚拟环境及其中所安装的包都删除。

```
conda remove --name env_name --all

```

​        如果只删除虚拟环境中的某个或者某些包则是：

```
conda remove --name env_name  package_name

```

3.6 导出环境 
        很多的软件依赖特定的环境，我们可以导出环境，这样方便自己在需要时恢复环境，也可以提供给别人用于创建完全相同的环境。

#获得环境中的所有配置
```
conda env export --name myenv > myenv.yml
```

#重新还原环境
4.
  ```
  conda env create -f  myenv.yml
  ```
  
  包（Package）的管理
  4.1 查询包的安装情况
        查询看当前环境中安装了哪些包

```
conda list
```

​        查询当前Anaconda repository中是否有你想要安装的包

```
conda search package_name

```

​        当然与互联网的连接是执行这个查询操作乃至后续安装的前提条件.

4.2 包的安装和更新
        在当前（虚拟）环境中安装一个包：

```
conda install package_name

```

​       当然也可以如上所述在创建虚拟环境的同时安装包，但是并不建议。安装完一个包后可以执行conda list确认现在列表中是否已经包含了新安装的包。

​    也可以以以下命令安装某个特定版本的包(以下例为安装0.20.3版本的numpy)：

```
conda install numpy=0.20.3

```

​        可以用以下命令将某个包更新到它的最新版本 ：

```
conda update numpy

```

​        安装包的时候可以指定从哪个channel进行安装，比如说，以下命令表示不是从缺省通道，而是从conda_forge安装某个包。

```
conda install pkg_name -c conda_forge

```

4.3 conda卸载包

```
conda uninstall package_name

```

​        这样会将依赖于这个包的所有其它包也同时卸载。

​    如果不想删除依赖其当前要删除的包的其他包：

```
conda uninstall package_name --force

```

​      但是并不建议用这种方式卸载，因为这样会使得你的环境支离破碎，如以下（conda manual  description原文）所述：



​    一个直观的理解就是，如果一个包A被删除了，而依赖于它的包B、C等却没有删除，但是那些包其实也已经不可用了。另一方面，之后你又安装了A的新版本，而不幸的是，B、C却与新版本的A不兼容因此依然是不可用的。

4.4 清理anaconda缓存

```
conda clean -p      # 删除没有用的包 --packages
conda clean -t      # 删除tar打包 --tarballs
conda clean -y -all # 删除所有的安装包及cache(索引缓存、锁定文件、未使用过的包和tar包)
```

5. ## Python版本的管理
     
     除了上面在创建虚环境时可以指定python版本外，Anaconda基环境的python版本也可以根据需要进行更改。

5.1 将版本变更到指定版本

```
conda install python=3.5

```

更新完后可以用以下命令查看变更是否符合预期。

```
python --version

```

5.2 将python版本更新到最新版本
        如果你想将python版本更新到最新版本，可以使用以下命令：

```
conda update python

```
