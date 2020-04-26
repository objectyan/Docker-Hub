# 设置系统环境
FROM ubuntu:latest

# 作者信息
LABEL author=ObjectYan site=https://objectyan.me

# 设置映射文件
VOLUME [ "/AOSP" ]

# 设置工作目录
WORKDIR /AOSP

# 修改 source 地址
RUN perl -p -i -e "s/http:\/\/security.ubuntu.com/http:\/\/mirrors.aliyun.com/g" /etc/apt/sources.list
RUN perl -p -i -e "s/http:\/\/archive.ubuntu.com/http:\/\/mirrors.aliyun.com/g" /etc/apt/sources.list

# 更新系统
RUN apt update

# 安装repo
RUN apt install --assume-yes repo
RUN echo "export REPO_URL='https://github.com/GerritCodeReview/git-repo.git'" >> ~/.bashrc

# 安装JDK
RUN apt install --assume-yes openjdk-8-jdk && update-alternatives --config java && update-alternatives --config javac

# 安装需要包
RUN apt install --assume-yes git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip

# 导入GPG
ADD AOSP_PUB.asc /tmp/AOSP_PUB.asc
RUN gpg --import /tmp/AOSP_PUB.asc
RUN rm -rf /tmp/AOSP_PUB.asc

# 设置git信息
RUN git config --global color.ui "auto"
RUN git config --global user.email "objecttozero@sina.com"
RUN git config --global user.name "ObjectYan"

# 下载AOSP代码
RUN repo init -u https://aosp.tuna.tsinghua.edu.cn/platform/manifest -b android-10.0.0_r30

# 设置命令行
CMD [ "/bin/bash" ]