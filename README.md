## 参考链接

[github](https://github.com/sjwayrhz/webdav)  
[docker hub](https://hub.docker.com/repository/docker/sjwayrhz/webdav/general)

## 使用方法

在`.github/workflows/action.yml`中可以定义触发条件  

```
on:
  workflow_dispatch:
  push:
    tags:
      - '*'
```

workflow_dispatch: 手动执行，Push: 当推送test*标签的时候执行

打test*标签方法

```
Windows
以test为开头时间戳的tag
git tag "test-$(Get-Date -Format 'yyyyMMddHHmmss')"
删除本地test开头的tag
git tag | ? { $_ -like "test*" } | % { git tag -d $_ }
删除远程具体某个分支
git push origin --delete ${TAG}

Linux
git tag "test-$(date +%Y%m%d%H%M%S)"
```

### 步骤一：上传文件到google drive

获取共享连接，常规访问权限需要设置为知道链接的任何人，举例下面4个文件，每个1GB左右

```
https://drive.google.com/file/d/1KjXLEcIZ23KfURvNM4vw01yKWFP0ZZ4z/view?usp=sharing
https://drive.google.com/file/d/1TSh-ZehXXsRkb2vyhNh1BeCmZGHk9YyB/view?usp=sharing
https://drive.google.com/file/d/1TwjNwpVMsZBYtUus4psQsbDUGYQNPrJB/view?usp=sharing
https://drive.google.com/file/d/1aKobTb0q9UOerYD1jg-R463zfFTxTdkk/view?usp=sharing
```

### 步骤二：更新index.yml

- 将步骤一生成的4个链接复制到 tasks/index.yml中的 urls;
- 并且把希望生成docker镜像的tag，tasks/index.yml中的 tag;
- 再在tasks/README.md中追加预期产生在dockerhub中的镜像链接

### 步骤三： 使用git push更新

此时，可以把新版本代码推送到github

## 追踪

去github action追踪进度，或者去dockerhub追踪新生成的镜像
