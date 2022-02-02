FROM php:7.4-cli-alpine

ARG UID=1000
ARG GID=1000
ARG USER_NAME=vscode

# Install packages & set timezone
RUN apk --update --no-cache add \
  git \
  openssh \
  tzdata \
  && cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
  && apk del tzdata \
  && echo "Asia/Tokyo" > /etc/timezone

# Install composer
ENV COMPOSER_HOME=/composer

COPY --from=composer:2.1 /usr/bin/composer /usr/bin/composer

# Copy PHP setting
COPY php.ini /usr/local/etc/php/

# Switch to non-root user
RUN addgroup -g "${GID}" "${USER_NAME}" \
  && adduser -D -s /bin/ash -u "${UID}" -G "${USER_NAME}" "${USER_NAME}"

USER ${USER_NAME}

# Create workspace
WORKDIR /app