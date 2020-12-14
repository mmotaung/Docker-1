#docker build -t ft-rails:on-build .
#docker build -t ex02 ./app
#docker run --name ex02 --rm -p 3000:3000 ex02

FROM ruby

RUN mkdir -p /opt/
WORKDIR /opt/

RUN gem install rails bundler
RUN gem install rails

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    sqlite3 \
    nodejs \
    yarn \
    git

RUN rails new app
WORKDIR /opt/app/

RUN bundle update && bundle install

ONBUILD RUN rake db:migrate
ONBUILD RUN rake db:seed
