FROM ruby:latest

RUN apt-get update && apt-get install -y \
    curl \
    build-essential \
    libpq-dev && \
    apt-get update && \
    gem install rails

WORKDIR /backend
COPY Gemfile /backend/Gemfile
RUN bundle install
COPY . /backend

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

# Configure the main process to run when running the image
CMD ["rails", "server", "-b", "0.0.0.0"]''