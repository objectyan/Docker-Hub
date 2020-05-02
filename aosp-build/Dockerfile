# 设置系统环境
FROM ubuntu:18.04

# 作者信息
LABEL author=ObjectYan site=https://objectyan.me

# 设置默认的shell为bash
RUN dpkg-reconfigure -p critical dash

# 设置映射文件
VOLUME [ "/AOSP" ]

# 设置工作目录
WORKDIR /AOSP

# 修改 source 地址
RUN perl -p -i -e "s/http:\/\/security.ubuntu.com/http:\/\/mirrors.tuna.tsinghua.edu.cn/g" /etc/apt/sources.list
RUN perl -p -i -e "s/http:\/\/archive.ubuntu.com/http:\/\/mirrors.tuna.tsinghua.edu.cn/g" /etc/apt/sources.list

# 更新系统
RUN apt-get update && apt-get -y upgrade

# 安装JDK
RUN apt install --assume-yes openjdk-8-jdk && update-alternatives --config java && update-alternatives --config javac

# 安装需要包
RUN apt install --assume-yes git python3 git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip
# 设置Python
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 0

# 安装repo
RUN curl https://mirrors.tuna.tsinghua.edu.cn/git/git-repo -o /usr/bin/repo
RUN chmod +x /usr/bin/repo
RUN echo "export REPO_URL='https://mirrors.tuna.tsinghua.edu.cn/git/git-repo'" >> ~/.bashrc

# 导入GPG
ADD ./aosp-build/AOSP_PUB.asc /tmp/AOSP_PUB.asc
RUN gpg --import /tmp/AOSP_PUB.asc
RUN rm -rf /tmp/AOSP_PUB.asc

# 设置git信息
RUN git config --global color.ui "auto"
RUN git config --global user.email "objecttozero@sina.com"
RUN git config --global user.name "ObjectYan"
RUN git config --global http.postBuffer 2000000000

# 设置命令行
CMD [ "/bin/bash" ]