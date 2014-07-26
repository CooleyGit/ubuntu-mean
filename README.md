ubuntu-mean
===========

Basic setup notes for mean stack install on AWS Ubuntu 14.04. I am assuming you have AWS account and a pem file somewhere on your local. Launch new EC2 instance on AWS you can use the default AWS Ubuntu 14.04 server, all settings can be default except security group. 

####Security group:
```
* SSH            TCP     22     <ip>
* HTTP           TCP     80     <ip>
* All traffic    All     All    <ip>
``` 
*Note: I use these basic settings to get started. You dont need to open all ports. You should be using your computer ip for security.*

####Install Node and npm 
```
sudo apt-get update
sudo apt-get install nodejs
sudo apt-get install npm
```
*Note: Installed from apt-get so it may not be the latest version, alternative install with (Chris Lea PPA)*

####Create a symlink in your path to use the `node` comand
```
sudo ln -s `which nodejs` /usr/local/bin/node
```
*Note: If you install using nvm you dont need to do this*

####Install mongodb
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
sudo apt-get update
sudo apt-get install mongodb-org
```
*[source @ docs.mongodb.org](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/)*

####Install Express
```
sudo npm install -g express
```

>Main install done


##Get project running on server 
*Note: A good Yeoman project to start with is [DaftMonk/generator-angular-fullstack](https://github.com/DaftMonk/generator-angular-fullstack)*

####SCP your project to the ubuntu directory 
```
scp -i ~/.ssh/your-pem-file.pem -r ~/local-project-path ubuntu@0.0.0.0:/home/ubuntu
```
*Note: replace 0.0.0.0 with your ip, you should be running this from your local*

####Run npm in your project root 
```
sudo npm install
```

##Start the server with `node` comand 
```
cd path/to/server/file
node app.js
```
*Note: This will only run while your terminal session is open, use pm2 to keep server running*

##PM2 options

####Install pm2 
```
sudo npm install -g pm2
```
*Note: pm2 will allow you to keep your server running and create clusters*

####Start pm2 
```
sudo pm2 start <server file> -i 4
```
*Note: This example will start 4 clusters*

####Other pm2 options
```
sudo pm2 stop <server file>
sudo pm2 restart <server file>
sudo pm2 delete <server file>
```

####Different ways to launch a pm2 process 
```
pm2 start app.js -i max  # Will start maximum processes depending on available CPUs
pm2 start app.js -i 3    # Will start 3 processes
pm2 start app.js -i max -- -a 23  # Pass arguments after -- to app.js
```
*Note: More options @ [https://www.npmjs.org/package/pm2](https://www.npmjs.org/package/pm2)*



