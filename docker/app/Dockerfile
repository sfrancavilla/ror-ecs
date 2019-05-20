# 1.Retrieve the ruby image
FROM ruby:2.4.1

# 2.Install basic required libs
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs 

# 3.Install bundler
RUN gem install bundler --version "1.15.3"

# 4.Set an environment variable for the Rails app root folder
ENV RAILS_ROOT /var/www/ror-ecs

# 5.Create the working directory
RUN mkdir -p $RAILS_ROOT 

# 6.Set working directory
WORKDIR $RAILS_ROOT

# 7.Set production env variables and enabling the option to serve static files
ENV RAILS_ENV='production'
ENV RACK_ENV='production' 
ENV RAILS_SERVE_STATIC_FILES=true

# 8.Add Gemfile
COPY Gemfile Gemfile
COPY Gemfile.lock Gemfile.lock

# 9.Install gems. -j $(nproc) runs bundle with to total amount of CPU cores/threads available
RUN bundle install -j $(nproc)

# 10.Add Rails project files
COPY . .

# 11.Expose port 3000 to be available for NGINX reverse proxy
EXPOSE 3000

# 12.Start the main process with Puma
CMD ["bundle", "exec", "puma", "-C", "config/puma.rb"]