FROM mariadb:10.2-bionic

# Make bash to accept Japanese inputs
RUN apt-get update \
  && apt-get install -y locales \
  && locale-gen ja_JP.UTF-8 \
  && localedef -f UTF-8 -i ja_JP ja_JP.utf8 \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Set timezone
ENV TZ=Asia/Tokyo

# Set locale
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8

# Copy MariaDB setting
RUN mkdir /logs
COPY my.cnf /etc/mysql/conf.d/

# Switch to non-root user
USER mysql