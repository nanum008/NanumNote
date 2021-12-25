# 一、配置

## 1、全局配置

### 配置全局用户名和邮箱地址

```shell
git config --global  user.name "这里换上你的用户名"
git config --global user.email "这里换上你的邮箱"
```

### SSH密钥生成

```shell
ssh-keygen -t rsa -C "这里换上你的邮箱"
```

执行命令后需要进行3次或4次确认：

1. 确认秘钥的保存路径（如果不需要改路径则直接回车）；
2. 如果上一步指定的保存路径下已经有秘钥文件，则需要确认是否覆盖（如果之前的秘钥不再需要则输入yes覆盖，如需要保留则手动拷贝到其他目录后再覆盖）；
3. 创建密码（如果不需要密码则直接回车生成密钥）；
4. 确认密码；

### 查看全局配置详情

```shell
1、git config --global --list
-------------------------------------------
2、git config --global -l
```



## 2、当前项目配置

### 查看当前项目的配置详情

- 命令

```shell
git config --list
```

- 示例

  ![image-20211225170358634](C:\Users\nanum008\AppData\Roaming\Typora\typora-user-images\image-20211225170358634.png)
