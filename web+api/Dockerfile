FROM ruby:latest

RUN apt-get update && apt-get install -y \
    curl \
    build-essential \
    libpq-dev &&\
    curl -sL https://deb.nodesource.com/setup_lts.x | bash - && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y nodejs yarn && \
    gem install rails sqlite3

WORKDIR /crudApp
COPY Gemfile /crudApp/Gemfile
COPY Gemfile.lock /crudApp/Gemfile.lock
RUN bundle install
COPY . /crudApp

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

# Configure the main process to run when running the image
CMD ["rails", "server", "-b", "0.0.0.0"]