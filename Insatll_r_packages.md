# R包安装及镜像设置

## 安装包

### 本地安装源码包

```R
install.packages("path/to/pkg/pkg_name.tar.gz", repos = NULL, type = "source")
```

Note: 源码编译安装的时候，要将源码压缩成tar.gz格式再安装，zip格式会出奇怪的错误。

### 安装CRAN包

```R
install.packages("pkg_name", lib, repos = getOption("repos"), quiet = FALSE)
```

`lib`: character vector giving the library directories where to install the packages. Recycled as needed. If missing, defaults to the first element of .libPaths().
`repos`: character vector, the base URL(s) of the repositories to use, e.g., the URL of a CRAN mirror such as "https://cloud.r-project.org". For more details on supported URL schemes see url.

`quiet`: logical: if true, reduce the amount of output.

### 安装Bioconductor 包

```R
# 利用BiocManger 
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("pkg_name")


# 利用bioLite (deprecated)
source("https://bioconductor.org/biocLite.R")
biocLite("pkg_name")
# or
install.packages("BiocInstaller")
BiocInstaller::biocLite("pkg_name")  
```

> Note: 
>
> `BioInstaller` and `biocLite`are deprecated use the `BiocManager` cran package instead.
>
> BiocManger can install or update Bioconductor, CRAN, or GitHub packages.

## R包相关操作

```R
# 查看R包安装位置
.libPaths()

# 查看已安装的包
installed.packages()

# 查看包版本
packageVersion("pkg_name")

# 更新包
update.packages("pkg_name")

# 加载包
library("pkg_name")
require("pkg_name")

# 查看加载的包
search()
.packages()

# 移除已加载的包（将包从R运行环境中移除）
detach("package:pkg_name")

# 彻底删除已安装的包：
remove.packages("pkg_name", lib = file.path("path/to/library"))
```

## 镜像设置

### 常用镜像地址

| Name                      | URL                                        | host   | type        |
| ------------------------- | ------------------------------------------ | ------ | ----------- |
| China (Anhui)   [https]   | https://mirrors.ustc.edu.cn/bioc/          | 中科大 | CRAN_mirror |
| China (Anhui)             | http://mirrors.ustc.edu.cn/bioc/           | 中科大 | CRAN_mirror |
| China (Beijing)   [https] | https://mirrors.tuna.tsinghua.edu.cn/CRAN/ | 清华   | BioC_mirror |
| China (Beijing)           | http://mirrors.tuna.tsinghua.edu.cn/CRAN/  | 清华   | BioC_mirror |
|                           |                                            |        |             |

### 镜像设置

```R
# 查看当前镜像
getOption("repos")
options("repos")
getOption("BioC_mirror")
options("BioC_mirror")

# CRAN镜像设置
install.packages("pkg_name", repos = "https://mirrors.ustc.edu.cn/CRAN/")
# or
options(repos = "https://mirrors.ustc.edu.cn/CRAN/")
install.packages("pkg_name")

# BioC镜像设置
biocLite("pkg_name", siteRepos = "http://mirrors.ustc.edu.cn/bioc/")
# or
chooseBioCmirror(graphics = getOption("menu.graphics"), ind = NULL, local.only = FALSE)
# or
options(BioC_mirror = "https://mirrors.tuna.tsinghua.edu.cn/bioconductor")
biocLite("pkg_name")
```

### 常用函数

```R
# 查看R_HOME地址
R.home()

R_HOME/doc/CRAN_mirrors.csv
R_HOME/doc/BioC_mirrors.csv
```

### 将镜像添加到配置文件

Bioconductor 镜像源配置文件之一是 `.Rprofile`

linux:`~/.Rprofile` 

win: `R_HOME/etc/Rprofile.site`

在文末添加如下语句:

```R
options(BioC_mirror = "https://mirrors.tuna.tsinghua.edu.cn/bioconductor")
```

### Useful 参数设置

先判断包是否存在，若不存在则加载包

```R
if (!require("devtools") install.packages("devtools")
```




