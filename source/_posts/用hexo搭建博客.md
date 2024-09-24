---
title: 用hexo搭建博客
date: 2020-7-15
categories: []
---

cnm搭了一晚上现在是15日0：07

基本参考资料为

https://www.cnblogs.com/SUNYZBlog/p/10772712.html

还算行

和这篇又配合了一下看的（顺带一提我更推荐这篇，代码比较正确，但图例少，上面那篇有的地方有错误，但是图例丰富

https://www.jianshu.com/p/09875c4a629c

我安装中遇到的问题（详细请展开

 <!-- more -->

1. 各种的 不是内部或外部文件

   这种情况是没添加全局变量，搜一下如何添加xxx的全局变量就可以了。

   由于我很久之前就装过一次，所以软件都是现成的，安装上的问题不太懂

   比如hexo用nmp就是装不上，最后我用现成的凑活了。。。

2. 安装卡住，半天没有下一条显示

   多半是网络问题，换源解决。

   ```markdown
   npm config set registry https://registry.npm.taobao.org
   ```

   这是什么淘宝源，我看大部分都说让换成这个。

   输入完之后他啥反应没有，直接输下一个指令就行（nmp npm install -g hexo-cli）

3. publisher无法打开 id_rsa.pub、

   用记事本打开就行

4. hexo d失败

   ##### ①bash： dev/tty no such device or address

   原因是修改delpoy时，repo那行，不用https，改为ssh

   #####  ②Permanently added the RSA host key for IP address 'xxx' to the list of known hosts.

   这是个warning，可以忽略。或者把这个ip加到host里

   ##### ③Could not read from remote repository 

   说是因为ssh没在github上配置，但我确实配过了，而且前面的测试也成功了。

   我尝试用终端运行ssh-keygent，但显示缺少msys-1.0.dll，下载之后按网上的各种方法添加也还是缺失该文件。

   然后我尝试其他解决办法，试了一上午，都没用。

   最后我决定用git bush里试试，这回成功了，然后我新建了一个ssh，删掉之前的ssh，然后再按步骤走了一遍，问题解决了。

   

以上基本配置完成。





