# 设置系统环境
FROM centos:8

# 作者信息
LABEL author=ObjectYan site=https://objectyan.me

# 修改 source 地址
RUN sed -i "s/mirrorlist/#mirrorlist/g" /etc/yum.repos.d/CentOS-Base.repo
RUN sed -i "s/#baseurl=http:\/\/mirror.centos.org\/\$contentdir/baseurl=https:\/\/mirrors.tuna.tsinghua.edu.cn\/centos/g" /etc/yum.repos.d/CentOS-Base.repo
RUN sed -i "s/mirrorlist/#mirrorlist/g" /etc/yum.repos.d/CentOS-AppStream.repo
RUN sed -i "s/#baseurl=http:\/\/mirror.centos.org\/\$contentdir/baseurl=https:\/\/mirrors.tuna.tsinghua.edu.cn\/centos/g" /etc/yum.repos.d/CentOS-AppStream.repo
RUN sed -i "s/mirrorlist/#mirrorlist/g" /etc/yum.repos.d/CentOS-PowerTools.repo
RUN sed -i "s/#baseurl=http:\/\/mirror.centos.org\/\$contentdir/baseurl=https:\/\/mirrors.tuna.tsinghua.edu.cn\/centos/g" /etc/yum.repos.d/CentOS-PowerTools.repo
RUN sed -i "s/mirrorlist/#mirrorlist/g" /etc/yum.repos.d/CentOS-Extras.repo
RUN sed -i "s/#baseurl=http:\/\/mirror.centos.org\/\$contentdir/baseurl=https:\/\/mirrors.tuna.tsinghua.edu.cn\/centos/g" /etc/yum.repos.d/CentOS-Extras.repo
RUN yum makecache

# 更新系统
RUN yum update -y

# 设置git信息
RUN yum install git -y
RUN git config --global color.ui "auto"
RUN git config --global user.email "objecttozero@sina.com"
RUN git config --global user.name "ObjectYan"
RUN git config --global http.postBuffer 2000000000

# 安装repo
RUN mkdir -p ~/.bin
RUN echo "PATH='${HOME}/.bin:${PATH}'" >> ~/.bashrc
RUN curl https://mirrors.tuna.tsinghua.edu.cn/git/git-repo -o ~/.bin/repo
RUN chmod a+rx ~/.bin/repo
RUN echo "export REPO_URL='https://mirrors.tuna.tsinghua.edu.cn/git/git-repo'" >> ~/.bashrc

# 安装支持环境
RUN yum install -y python36 git-core gawk make wget tar bzip2 gzip unzip perl patch diffutils diffstat git cpp gcc gcc-c++ glibc-devel chrpath socat SDL-devel xterm curl
RUN ln -s /usr/bin/python3 /usr/bin/python

# 设置映射目录、工作目录
VOLUME [ "/AGL" ]
WORKDIR /AGL

# 下载代码
# RUN repo init -u https://git.automotivelinux.org/AGL/AGL-repo