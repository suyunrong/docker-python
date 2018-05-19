FROM python:3.6.5
LABEL authors=suyunrong

#=======================================
# Install base package
#=======================================
RUN apt-get update -qqy \
  && apt-get install -qqy \
    tzdata \
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
#pip3 package
#=======================================
COPY requirements.txt /tmp/
RUN pip3 -r /tmp/requirements.txt

CMD ["python3"]