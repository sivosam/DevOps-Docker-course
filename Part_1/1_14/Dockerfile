FROM ruby:2.6.0
WORKDIR /usr/src/app
RUN apt-get update
RUN apt-get install -y git
RUN apt-get install -y nodejs
RUN git clone https://github.com/docker-hy/rails-example-project.git .
RUN gem install bundler
RUN bundle install
EXPOSE 3000
RUN rails db:migrate
CMD rails s
