FROM python:3

# check: https://chromedriver.storage.googleapis.com/LATEST_RELEASE
ARG DRIVER_VERSION=88.0.4324.96

ENV TZ=Asia/Tokyo
ENV DEBIAN_FRONTEND=noninteractive
ENV LANG ja_JP.UTF-8
ENV PYTHONIOENCODIND utf_8

RUN \
  apt-get update && \
  apt-get install -y curl unzip fonts-ipafont fonts-ipaexfont && \
  # install chrome
  curl -fsSL https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
  echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list && \
  apt-get update && \
  apt-get install -y google-chrome-stable && \
  # setup chrome driver
  curl -O https://chromedriver.storage.googleapis.com/${DRIVER_VERSION}/chromedriver_linux64.zip && \
  unzip chromedriver_linux64.zip && \
  mv chromedriver /usr/local/bin/. && \
  rm -f chromedriver_linux64.zip && \
  # cleanup
  apt-get clean && rm -rf /var/lib/apt/lists/*

ADD requirements.txt /
RUN \
  pip install --upgrade pip && \
  pip install -r /requirements.txt

# Define default command.
CMD ["/bin/bash"]
