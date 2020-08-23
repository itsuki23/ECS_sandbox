FROM ruby:2.5.1

RUN apt-get update && \
    apt-get install -y nodejs mysql-client vim nginx supervisor libssl-dev

# RUN ln -sf /dev/stdout /var/log/nginx/access.log \
#     && ln -sf /dev/stderr /var/log/nginx/error.log

COPY ./_rails/ /var/www/rails/
# COPY ./src/Gemfile /app/Gemfile
# COPY ./src/Gemfile.lock /app/Gemfile.lock

# bundle install
WORKDIR /var/www/rails/
RUN bundle install
# RUN bundle install --path vendor/bundle

# nginx
RUN groupadd nginx
RUN useradd -g nginx nginx
ADD ./nginx/nginx.conf /etc/nginx/nginx.conf

# setting superviser
COPY ./supervisor/app.conf /etc/supervisor/conf.d/app.conf
# EXPOSE 3000

# link logs
# RUN ln -sf /dev/stdout /var/log/nginx/access.log
# RUN ln -sf /dev/stderr /var/log/nginx/error.log

# Service to run
CMD [ "/usr/bin/supervisord" ]

############################################################
# コマンド実行はルートで
# docker build -t <tag_name> -f dev/app/Dockerfile .
