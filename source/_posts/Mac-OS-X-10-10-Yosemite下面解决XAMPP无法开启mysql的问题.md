title: "Mac OS X 10.10 Yosemite下面解决XAMPP无法开启mysql的问题"
coverHideInPost: true
coverImage: cover.png
date: 2015-05-19 13:25:06
tags:
- MacOX
categories:
- Programming
---

在xampp安装目录下找到xampp,
这个文件默认路径是: 
   /Applications/XAMPP/xamppfiles/xampp
用文本编辑器打开, 搜索:
{% codeblock %}
   $XAMPP_ROOT/bin/mysql.server start > /dev/null &
{% endcodeblock %}
在那一行前面添加: 
{% codeblock %}
unset DYLD_LIBRARY_PATH
{% endcodeblock %}
保存退出, 重新打开xampp, 开启MySQL。
