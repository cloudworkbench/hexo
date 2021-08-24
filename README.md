<img src="https://raw.githubusercontent.com/hexojs/logo/master/hexo-logo-avatar.png" alt="Hexo logo" width="35" height="35" align="right" />

# 通过云开发平台，将Hexo项目快速发布为线上网站

### **背景介绍**

云开发平台是阿里云面向广大开发者提供的免费的云上研发工作平台，可以实现云计算应用开发、部署的完整流程。关于云开发平台的详细介绍：https://help.aliyun.com/product/161245.html。

### **最佳实践**

**1.创建Hexo代码项目**

直接fork本项目到自己的GitHub账号下。本仓库内代码与hexo init生成的默认模版内容一致。

**2.打开云开发平台，完成阿里云账号注册登陆，同意云开发平台服务协议** https://workbench.aliyun.com/application

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/sign.png" width="400">

**3.创建云开发平台-前端部署应用**

3.1 创建前端应用

依次点击「应用列表」「前端应用」「新建前端应用」按钮。首先绑定GitHub帐号，允许云开发平台构建、发布你的GitHub代码为可访问的网站。

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/create_0.png" width="200">

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/oauth.png" width="200">

选择第一步中的代码仓库、主干分支等，并点击下一步。主干分支一般指的是代码的master或main等分支。

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/create_1.png" width="300">

填写基本信息并点击「完成」。稍等片刻创建成功后，将进入到应用部署界面。

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/create_2.png" width="600">

3.2 开发部署配置

3.2.1 填写日常/线上环境的部署配置

按照"?"提示，依次填写部署配置信息。其中：

- 「纯静态网站」需勾选“是”，让云开发平台可以直接将「资源路径」中的本地静态资源，上传到云端供网站使用。
   如有特殊需求，如希望在本地完成hexo generate，或者更多的shell脚本操作，则需要勾选“否”，并在.gitignore中添加/public目录。之后，云开发平台会在部署项目时，自动调用根目录下的build.sh脚本，执行其中的hexo generate，或其它shell脚本指令，完成生成/public目录中静态资源的步骤。而后在部署过程中，将「资源路径」中的本地静态资源，上传到云端供网站使用。

    <img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/config.png" width="300">

- 「资源路径」需填写“./public”，因为Hexo框架生成的静态资源，默认是存放在public目录下的。开发平台会将该目录下的文件完整存储到OSS中，供网站访问使用。

- OSS配置中，需要填写要部署到的OSS Bucket与OSS地域。关于OSS，可打开https://oss.console.aliyun.com/bucket ，开通OSS服务，并创建OSS Bucket。若要用的域名暂无公安部备案信息可用，建议选择中国内地以外的OSS地域创建Bucket，如“美国-硅谷”。开通OSS和创建OSS Bucket不收取用户费用。

    新建OSS Bucket及查看Bucket列表的链接：https://oss.console.aliyun.com/bucket

    新建及查看操作示意图：

    <img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/oss_new.png" width="450">
<br/>
    <img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/oss_list.png" width="450">

3.2.2 填写日常/线上环境的分支管理

按需选择要发布的代码所在的分支，可新建分支（从主干分支分叉）或选择已有分支。建议可以使用新建分支，创建名称更规范的代码分支。

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/branch.png" width="300">

3.3 进行项目的部署和查看

依次点击「部署」「确定」，即可启动日常/线上环境的发布流程。对于每个代码分支，要求先发布日常环境，再发布线上。若不需多套环境，则可以只使用日常环境，或者发布一次日常环境后，仅使用线上环境即可。

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/deploy.png" width="300">

在部署完成后，部署状态会显示为“已部署”。且部署网站的记录和过程，也会被完整记录下来：

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/main.png" width="600">

可点击部署记录的「查看结果」来查看部署到OSS存储中的静态资源。并将资源的链接复制下来，供其它网站等引用访问。

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/result.png" width="400">

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/result_download.png" width="350">

可点击部署记录的「查看日志」查看部署的详细过程，并在部署发生错误时，精确定位学习错误情况。

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/log.png" width="550">

部署操作可以在每次更新博客内容并push后再次进行，实现静态网站内容的按需实时更新。

3.4 将OSS存储中的项目发布为网站链接

发布到OSS存储中的资源，由于相关政策和要求，不能使用「查看结果」中的链接和域名直接访问，需要将*OSS Bucket的访问域名* 和 *自己的域名* 做双向绑定和解析。操作步骤如下：

3.4.1 绑定OSS Bucket的访问域名到自己的域名上

需要在https://oss.console.aliyun.com/bucket 中查看OSS列表，点击进入自己使用的Bucket，选择「传输管理」「绑定域名」，输入自己的域名，点击确定即可。

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/domain_1.png" width="500">

3.4.2 解析自己的域名到OSS Bucket的访问域名上

打开自己域名的DNS解析控制台，使用阿里云域名或其它提供商的域名均可，此处以阿里云为例：

首先，找到自己要解析的域名，添加/修改一条解析记录：

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/cname.png" width="650">

如下图所示，配置CNAME、自己的域名、记录值：

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/cname_2.png" width="400">

记录值查看方法示意图：

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/oss_domain.png" width="600">

3.4.3 部署完成，查看部署结果

最后，稍等片刻，确定使用https://zijian.aliyun.com/ ，或者ping/dig/nslookup等指令可以查找到本域名的解析情况后，访问**域名+静态资源路径**，如 mydomain.com/index.html ， 即可看到网页内容：

<img src="https://ecoboost-readme-image.oss-cn-shanghai.aliyuncs.com/feApp/github/hexo/page.png" width="700">

3.5 （可选）使用CDN加速域名访问，节约流量费用

可点击「部署配置」中的「如何配置CDN加速」，将自己的域名与CDN加速绑定，从而加速网站访问。
