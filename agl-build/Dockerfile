# 设置系统环境
FROM ubuntu:18.04

# 作者信息
LABEL author=ObjectYan site=https://objectyan.me

# 设置时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo 'Asia/Shanghai' >/etc/timezone

# 修改 source 地址
RUN perl -p -i -e "s/http:\/\/security.ubuntu.com/http:\/\/mirrors.tuna.tsinghua.edu.cn/g" /etc/apt/sources.list
RUN perl -p -i -e "s/http:\/\/archive.ubuntu.com/http:\/\/mirrors.tuna.tsinghua.edu.cn/g" /etc/apt/sources.list

# 更新系统
RUN apt-get update && apt-get -y upgrade

# 安装支持环境
RUN apt install --assume-yes git build-essential chrpath curl diffstat gcc-multilib gawk git-core libsdl1.2-dev texinfo unzip wget xterm bzip2 dosfstools mtools parted syslinux tree

# 安装repo
RUN curl https://mirrors.tuna.tsinghua.edu.cn/git/git-repo -o /usr/bin/repo
RUN chmod +x /usr/bin/repo
RUN echo "export REPO_URL='https://mirrors.tuna.tsinghua.edu.cn/git/git-repo'" >> ~/.bashrc

# 设置git信息
RUN git config --global color.ui "auto"
RUN git config --global user.email "objecttozero@sina.com"
RUN git config --global user.name "ObjectYan"

# 设置映射目录、工作目录
VOLUME [ "/AGL" ]
WORKDIR /AGL

# 下载代码
# RUN repo init -u https://git.automotivelinux.org/AGL/AGL-repo