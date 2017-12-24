# DealWithPythonOnMac


｛删除Mac OS系统自带的Python 2.7｝
备注：我的macOS版本是10.10.5 Yosemite.

［第一步：删除Python 2.7的Framework.］
Step 1. Remove the Python 2.7 framework

sudo rm -rf /Library/Frameworks/Python.framework/Versions/2.7
如果以上命令无效，则尝试如下命令（系统自带Python的默认路径）
sudo rm -rf /System/Library/Frameworks/Python.framework/Versions/2.7

［第二步：删除Python 2.7的应用程序目录。］
Step 2. Remove the Python 2.7 applications directory

sudo rm -rf "/Applications/Python 2.7"

［第三步：删除Python的快捷方式。］
Step 3. Remove the symbolic links in /usr/local/bin that point to this Python version.

查看/usr/local/bin下所有与Python 2.7有关的快捷方式
ls -l /usr/local/bin | grep '../Library/Frameworks/Python.framework/Versions/2.7'
删除快捷方式的命令
cd /usr/local/bin/
ls -l /usr/local/bin | grep '../Library/Frameworks/Python.framework/Versions/2.7' | awk '{print $9}' | tr -d @ | xargs rm
如果以上删除命令无效，则尝试以下命令
查看
sudo find /usr/local/bin -lname '../../../Library/Frameworks/Python.framework/Versions/2.7/*'
删除
sudo find /usr/local/bin -lname '../../../Library/Frameworks/Python.framework/Versions/2.7/*' -delete

同样的方式，查看并删除/usr/bin下所有与Python 2.7有关的快捷方式（此处省略）

［第四步：删除shell profile文件中与Python 2.7有关的环境变量设置］
Step 4. If necessary, edit your shell profile file(s) to remove adding /Library/Frameworks/Python.framework/Versions/2.7 to your PATH environment file. 
Depending on which shell you use, any of the following files may have been modified: ~/.bash_login, ~/.bash_profile, ~/.cshrc, ~/.profile, ~/.tcshrc, and/or ~/.zprofile.

我这里修改的是~/.bash_profile文件。

［补充：新增指向Python 3.6的快捷方式］
sudo ln -s /Library/Frameworks/Python.framework/Versions/3.6/bin/python3.6 /usr/local/bin/python

