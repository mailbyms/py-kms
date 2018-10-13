# History
py-kms is a port of node-kms by [markedsword](http://forums.mydigitallife.info/members/183074-markedsword), which is a port of either the C#, C++, or .NET implementations of KMSEmulator, of which the original version was written by [CODYQX4](http://forums.mydigitallife.info/members/89933-CODYQX4) and is derived from the reverse-engineered code of Microsoft's official KMS.

# Features
- Responds to V4, V5, and V6 KMS requests.
- Supports activating Windows 7/8/8.1/10/2008R2/2012/2012R2/2016 and Office 2010/2013/2016.
- It's written in Python2.

# Dependencies
- Python 2.7.x or Python 2.6.x with the "argparse" module installed.
- If the "pytz" module is installed, the "Request Time" in the verbose output will be converted into local time. Otherwise, it will be in UTC.

# Usage
- To start the server, execute `python server.py [listen_address] [port]`. The default listening address is `0.0.0.0` (all interfaces) and the default port is `1688`.
- To run the client, use `python client.py server_address [port]`. The default port is `1688`.

安装py-kms
yum install python-argparse    #安装依赖
git clone https://github.com/matsuz/py-kms    #下载py-kms（或者https://github.com/myanaloglife/py-kms）
cd py-kms
python server.py
显示下面代表启动正常

TCP server listening at 0.0.0.0 on port 1688
这时候就安装完成了，已经使用命令激活了，但为了让kms服务长时间在后台运行，还需要下面设置一下。
返回py-kms文件夹上层目录，然后输入下面命令

cp -r py-kms /usr/local/
yum install python-setuptools
easy_install supervisor    #安装supervisor
echo_supervisord_conf > /etc/supervisord.conf
编辑supervisord.conf该文件，将下面配置代码放到最后

[program:pykms]
command=python /usr/local/py-kms/server.py
autorestart=true
user=root
最后输入运行命令

supervisord
