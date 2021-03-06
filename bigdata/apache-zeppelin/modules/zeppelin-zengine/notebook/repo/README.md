# Notebook 持久化

```md
Notebook的持久化子系统主要由 NotebookRepo 以及其子类组成。
```
```md
NotebookRepo 持久化层顶层接口，规定了持久化层的基本操作。
NotebookRepoSync 使note在本地系统与远程系统之间同步的实现类。

VFSNotebookRepo 数据存入文件系统的实现
GitNotebookRepo 使用Git对Note进行版本管理的实现
S3NotebookRepo和AzureNotebookRepo，实现向2大云存储系统的持久化Notebook。
ZeppelinHubRepo 是为了向zeppelinhub持久化Notebook而设计的，
zeppelinhub 是一个类似于Github的分享网站，区别在于Github是分享git仓库的，zeppelinhub是分享note的。
```
```md
1. NotebookRepo 是顶层接口，规定了持久化层基本的CRUD接口。 
2. NotebookVersioned定义了Note的版本管理接口，目前其实现类只有 GitNotebookRepo。
  GitNotebookRepo是以JGit库实现的基于本地文件系统的、支持以Note为粒度进行checkin和show log的Note仓库。 
3. VFSNotebookRepo是zeppelin的默认实现类
  （配置参数zeppelin.notebook.storage控制，参见：ZeppelinConfiguration。
  ZEPPELIN_NOTEBOOK_STORAGE("zeppelin.notebook.storage", VFSNotebookRepo.class.getName()),
  使用apache common-vfs 来实现多文件系统支持。 
4. NotebookRepoSync 的初衷是为了让2个NotebookRepo之间进行自动同步修改，
  实现：在本地repo保存修改的同时，让zeppelin自动将修改同步到远程的repo上。 
```
```md
要启用2个repo之间的同步，做如下修改：
在zeppelin-site.xml中修改配置参数zeppelin.notebook.storage，以逗号分隔2个实现类的完整类名
注意顺序，一般是将VFSNotebookRepo作为一个，而S3NotebookRepo或者是AzureNotebookRepo等作为第二个。
zeppelin目前只支持最大2个Repo（maxRepoNum=2作为编译时常量），不能通过配置修改。
```

* [VFSNotebookRepo.java](VFSNotebookRepo.md)

## Reference
* [* Notebook storage options for Apache Zeppelin](https://zeppelin.apache.org/docs/0.7.0/storage/storage.html)