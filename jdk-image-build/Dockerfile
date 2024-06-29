# 基础镜像
FROM ubuntu:24.04
# 维护者信息
MAINTAINER p7i <pengdahai216@126.com>
# 跳过时区选择（必须执行，否则后续构建镜像时会卡死到时区选择）
ENV DEBIAN_FRONTEND=noninteractive
# 编码格式
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
# 拷贝文件到容器(自动解压,解压完目录为jdk-21.0.2)
ADD ./jdk-21_linux-x64_bin.tar.gz /usr/local/
# 拷贝文件到容器(自动解压)
RUN mkdir /usr/local/arthas
ADD ./arthas-bin.zip /usr/local/arthas/
# 设置JAVA_HOME
ENV JAVA_HOME /usr/local/jdk-21.0.3
ENV JRE_HOME ${JAVA_HOME}/jre
ENV PATH $PATH:$JAVA_HOME/bin
RUN java -version
# 指定用户
USER root
# 设置时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo 'Asia/Shanghai' >/etc/timezone
RUN  apt-get clean
# 安装运行环境，比如一些第三方工具或者Java服务程序所依赖的包 安装unzip
# 安装dejavu-sans-fonts fontconfig 解决验证码Could not initialize class sun.awt.X11FontManager ttf-mscorefonts-installer
RUN apt-get update \
    && apt-get install unzip \
    && apt-get install aptitude -y\
    && apt-get install ttf-mscorefonts-installer -y\
    && apt-get install fontconfig -y
# 解压arthas.zip
RUN unzip /usr/local/arthas/arthas-bin.zip -d /usr/local/arthas
RUN rm -rf /usr/local/arthas/arthas-bin.zip