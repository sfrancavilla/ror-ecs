# 1.Retrieve the nginx base image
FROM nginx

# 2.Install some dependencies
RUN apt-get update -qq && apt-get -y install apache2-utils

# 3.Set env variable where NGINX should look for project files
ENV RAILS_ROOT /var/www/ror-ecs

# 4.Set working directory
WORKDIR $RAILS_ROOT

# 5.Create log directory
RUN mkdir log

# 6.Copy over static assets
COPY public public/

# 7.Copy Nginx config template
COPY /docker/web/nginx/nginx.conf /tmp/app.conf

# 8.Expose port 80 for public access to your app
EXPOSE 80

# 9.Copy our script in the main app folder
COPY docker/web/nginx/start.sh ./

# 10.Permission 755 allows the execute permission for all users to run the script
RUN chmod 755 ./start.sh

# 11.Execute the script
CMD ["./start.sh"]