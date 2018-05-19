FROM python:3.6.5
LABEL authors=suyunrong

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

#=======================================
#pip3 package
#=======================================
COPY requirements.txt /tmp/
RUN pip3 install -r /tmp/requirements.txt

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]