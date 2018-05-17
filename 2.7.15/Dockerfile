FROM python:2.7.15
LABEL authors=suyunrong

#=======================================
# Set Coding
#=======================================
ENV LANG C.UTF-8

#=======================================
# Install base package
#=======================================
RUN apt-get update -qqy \
  && apt-get install -qqy \
    tzdata \
    openssh-server \
  && rm -rf /var/lib/apt/lists/* \
    /var/cache/apt/* \
    /tmp/* \
    /var/tmp/*

#=======================================
# Set timezone
#=======================================
ENV TZ "Asia/Shanghai"
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
  && echo $TZ > /etc/TZ

#=======================================
# Config sshd
#=======================================
RUN mkdir /var/run/sshd \
  && mkdir /root/.ssh \
  && echo 'root:123456' |chpasswd \
  && sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config \
  && sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
#  && /etc/init.d/sshd start

EXPOSE 22

#CMD["python3"]
CMD ["/usr/sbin/sshd", "-D"]