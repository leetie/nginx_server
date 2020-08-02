Just a simple test app to try hosting an nginx webserver locally with the [passenger](https://phusionpassenger.com) gem. The tutorial and setup guide can be found [here](https://www.phusionpassenger.com/library/walkthroughs/deploy/ruby/ownserver/nginx/oss/install_language_runtime.html). 

There were some issues that I had to figure out along the way, and some things that I broke - but I worked them out. 
The first thing after the initial setup was that using curl to try and access my server was not working. This was due to the fact that I was not port forwarding the HTTP requests coming into my router (the thing I was actually curling instead of my webserver), which was resolved in my router settings. 

After forwarding HTTP requests to the server, I was getting 500 errors and I checked out the logs. It was due to changing the ownership of all the application's files while I was troubleshooting earlier by running 
```shell
sudo chown -R www-data:www-data /var/www/testapp
```
This was remedied by changing ownership back to the proper place with 
```shell
 sudo chown -R my_username:www-data /var/www/testapp
```
I did the usual 
```shell
bundle install; yarn-install --check-files; rails db:setup
```
also, which may have played a role, but I am not certain. 

The help pages that I used were 
	https://askubuntu.com/questions/676434/port-80-connection-refused
	https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-18-04
	https://www.digitalocean.com/community/questions/port-80-failed-connection-refused
