# 设置系统环境
FROM ubuntu

# 作者信息
LABEL author=ObjectYan site=https://objectyan.me

# 设置默认的shell为bash
RUN dpkg-reconfigure -p critical dash

# 设置映射文件
VOLUME [ "/AOSP-Mirror" ]

# 设置工作目录
WORKDIR /AOSP-Mirror

# 设置时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo 'Asia/Shanghai' >/etc/timezone

# 修改 source 地址
RUN perl -p -i -e "s/http:\/\/security.ubuntu.com/http:\/\/mirrors.tuna.tsinghua.edu.cn/g" /etc/apt/sources.list
RUN perl -p -i -e "s/http:\/\/archive.ubuntu.com/http:\/\/mirrors.tuna.tsinghua.edu.cn/g" /etc/apt/sources.list

# 更新系统
RUN apt-get update && apt-get -y upgrade

# 安装需要包
RUN apt install --assume-yes git-all python3 curl net-tools
# 设置Python
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 0
# 安装 
RUN apt install --assume-yes git-daemon-sysvinit

# 安装repo
RUN curl https://mirrors.tuna.tsinghua.edu.cn/git/git-repo -o /usr/bin/repo
RUN chmod +x /usr/bin/repo
RUN echo "export REPO_URL='https://mirrors.tuna.tsinghua.edu.cn/git/git-repo'" >> ~/.bashrc

# 设置git信息
RUN git config --global color.ui "auto"
RUN git config --global user.email "objecttozero@sina.com"
RUN git config --global user.name "ObjectYan"

ADD ./aosp-mirror/git-daemon /etc/default/git-daemon

# 设置命令行
CMD [ "service git-daemon start" ]